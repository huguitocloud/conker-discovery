# Conker's Bad Fur Day N64 Random Huguito's Discoveries Documentation

General:

1- Using hexadecimal hack, you can port/inject respective binary stuff into ROM if are exact same size.

1.1 - For smaller binaries, you need to fill empty space with zeros ( 00 )

------(cutscenes audios, cutscenes code, ingame audios).

1.2 - Unfornately you can't set respective bigger binary files, unless you know how to trick

------the size of the videogame's ROM and prevent its corruption.

1.3 - Example: Port uncensored cutscenes from ECTS builds [mod from gamebanana](https://gamebanana.com/mods/702099)


Related to Cutscenes:

1 - Cutscenes can play audios, but doesn't control the audios time. Maybe the audio time are hardcoded

----like in Playstation 2 versions of Grand Theft Auto 3D saga.

2 - Cutscenes has specific hex pattern code about playing its cutscenes audios.

2.1 - Hex pattern to play audios in cutscene code are something like 0B ?? ?? ?? 00 00 00 00

------So the 3 random values references to audios ID.

------Example: 0B 1E 00 B2 00 00 00 00 is Total War Multiplayer intro cutscene ( 1E 00 B2 )

3 - You can compile and decompile cutscenes using GEDecompressor (Only use old version, not new). [tool here](https://github.com/jombo23/N64-Tools)


Related to Cutscenes Audios:

1- This game has an ingenious lipsync system inside the cutscene audios. It controls the Conker's yaw.

----So, the only way to move the Conker's mouth, is looking carefully into cutscenes audios.

----Investigation about this fact by KIMBJO

1.1 - Other characters of the game are not lipsync-trick dependent.

------Only Conker has this specific feature.

2 - You can play cutscenes audios in VLC Player, if you trick respective files using hexadecimal hacks.

----Try to replace all detected 00 to 10. [More documentation about the trick here](https://www.audiokinetic.com/en/community/blog/video-game-sound-archiving-part-2/)

----Then, try to remove all random values with this specific hexadecimal pattern: 4C 3A ?? ?? ?? ?? ?? ?? ??.

----It means, you need to remove the last 7 values and keep the first 4C and 3A values.


