# Conker's Bad Fur Day N64 Random Huguito's Discoveries Documentation

## General:

1- Using hexadecimal hack, you can port/inject respective binary stuff into ROM if are exact same size.

1.1 - For smaller binaries, you need to fill empty space with zeros ( 00 )

------(cutscenes audios, cutscenes code, ingame audios).

1.2 - Unfornately you can't set respective bigger binary files, unless you know how to trick

------the size of the videogame's ROM and prevent its corruption.

1.3 - Example: Port uncensored cutscenes from ECTS builds [mod from gamebanana](https://gamebanana.com/mods/702099)


## Related to Cutscenes:

1 - Cutscenes can play audios, but doesn't control the audios time. Maybe the audio time are hardcoded

----like in Playstation 2 versions of Grand Theft Auto 3D saga.

2 - Cutscenes has specific hex pattern code about playing its cutscenes audios.

2.1 - Hex pattern to play audios in cutscene code are something like 0B ?? ?? ?? 00 00 00 00

------So the 3 random values references to audios ID.

------Example: 0B 1E 00 B2 00 00 00 00 is Total War Multiplayer intro cutscene ( 1E 00 B2 )

3 - Maybe you could inject code related to play audios in cutscenes, if you paste a pattern like this:

----FF 00 __ __ __ __ __ __ FE 00 D8 F1 __ __ __ __

----FD 00 00 00 __ __ __ __ __ __ 00 __ 00 00 00 00

----__ __ 00 __ 00 00 00 __ 0B ?? ?? ?? 00 00 00 00 (The 0B ?? ?? ?? is the audio ID as explained)

3 - You can compile and decompile cutscenes using GEDecompressor (Only use old version, not new). [tool here](https://github.com/jombo23/N64-Tools)


## Related to Cutscenes Audios:

1- This game has an ingenious lipsync system inside the cutscene audios. It controls the Conker's yaw.

----So, the only way to move the Conker's mouth, is looking carefully into cutscenes audios.

----Investigation about this fact by KIMBJO

1.1 - Other characters of the game are not lipsync-trick dependent.

------Only Conker has this specific feature.

2 - You can play cutscenes audios in VLC Player, if you trick respective files using hexadecimal hacks.

----Try to replace all detected 00 to 10. [More documentation about the trick here](https://www.audiokinetic.com/en/community/blog/video-game-sound-archiving-part-2/)

----Then, try to remove all random values with this specific hexadecimal pattern: 4C 3A ?? ?? ?? ?? ?? ?? ??.

----It means, you need to remove the last 7 values and keep the first 4C and 3A values.

## Cutscenes information 09-10-2026:

Some decompiled cutscenes has these common pattern (Be careful, may vary depending of cutscene and how they are made.) All patterns usually works as a 8 bytes code (8 values).

- Block prefix F5, F4 - It usually controls camera angles. F5 could start the cycle of the camera, F4 finishes the camera vectors or camera path. Also F4 usually works like a NPC or entities coordinates
Example:
F5 CC FE 01 17 21 00 00 --starting camera
F4 CD FE 1C 17 33 00 00 --finishing camera final path

Could be mixed in hexadecimal block in this order.
F5 CC FE 10 17 21 00 58 F4 CD FE 1C 17 33 00 58

F5 starts the camera cycle.
CC and CD controls axes (X, Y, depending the map or level), [range of 00 to FF, hexadecimal values]. Be careful to touch these values incorrectly, some cutscenes crash the game (like Sunflower cutscene or any singleplayer cutscene)
10 and 1C controls the heigh of the camera (axis Z) [range of 00 to FF, hexadecimal values],
58 (last byte of each 8bytes line) controls the style or angles of the camera. 58 means the camera has diagonal style (Like Tarantino movies, 70s movies, Batman old TV series camera angles). 00 value turn off this feature or this specific angle.

Example of cutscene related to tediz Total War intro:
F5 CC FE 1C 17 21 00 00 F4 CD FE 1F 17 33 00 00

<img width="338" height="240" alt="Image" src="https://github.com/user-attachments/assets/e64d58c6-25ed-4037-b610-4c173072b757" />

The F4 prefix could move entities like table, props, npcs...
F4 48 FD 01 17 3B 00 00 --- 01 axis means the object is touching the floor or clipping the floor depending if it's big! [range of 00 to FF, hexadecimal values]

As i said, camera code may vary. For example, Pikachu uncensored cutscene has other camera code. Doesn't have the F5 or F4 prefix but works similar. (Still investigating about it works)

00 00 04 E8 00 00 00 58 --- 58 represents the diagonal camera angle
Example of uncensored cutscene related to Pikachu - Camera focusing Rock bodyguard

<img width="338" height="240" alt="Image" src="https://github.com/user-attachments/assets/7837f3df-7947-4723-8779-f0d02bb1f596" />

00 00 04 38 00 00 00 18 --- 18 represents medium shot camera
Example of uncensored cutscene related to Pikachu - Camera focusing Conker

<img width="338" height="240" alt="Image" src="https://github.com/user-attachments/assets/dfbf8eba-61f8-4f52-8de7-35a5fbc787ff" />


- Block prefix 02 - usually controls animations!

Example of Tediz:
02 00 00 2B 01 00 00 00

2B is animation hexadecimal ID. Could change it to any hex value. In this example, the tediz will make a speech animation (Adolf Tediz); you can change it if you want a idle animation 2F, or 4A to playing a guitar! [range of 00 to FF, hexadecimal values]

02 00 00 2F 01 00 00 00 -- Idle (Usually works into any npc like Conker, Don Weaso....)
02 00 00 2B 01 00 00 00 -- Tediz talking (Adolf Tediz use this specific ID)
02 00 00 4A 01 00 00 00 -- Tediz animation playing guitar?
02 00 00 1F 00 00 00 00 -- Tediz crounching into the floor
02 00 00 4B 00 00 00 00 -- Tediz crazy animation idle
02 00 00 4D 00 00 00 00 -- Tediz crazy animation idle medic room cutscene (Into the character!! tatatatata...)
02 00 00 47 00 00 00 00 -- Tediz talking as a medic (from medic room cutscene)

01 represents if animation is not going to loop and changing after another animation command.

Another example:
02 50 00 2F 00 00 00 00

50 represents a permanent loop animation, and won't change if another animation code exists. Be careful here.
2F represents animation ID. 2F is idle.
If you set 01 or any value after 2F, animation freezes. Be careful here.
Example: 02 50 00 2F 01 00 00 00

- Block prefix 0B - controls cutscene audios! And you can paste into another code freely if you know what you're doing.

Example
0B 31 01 5C 00 00 00 00

The second, third and fourth bytes represents the audio ID. So we need to know the correct cutscene ID audios.

31 01 5C - Medic INTO THE CHARACTER TATATATATAPAPAPAPA...
00 01 17 - Pikachu uncensored audio
00 01 18 - After Pikachu cutscene (Don Weaso telling conker about a little job)




