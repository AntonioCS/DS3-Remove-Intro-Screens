# What is this?
The No-Logo mod is a modification for **Darksouls** **1** & **3** and **Sekiro** that completely removes the intro logo screens from the game.
These are the logos normally shown when first starting the game and after saving and quitting the game, every time.

# Installing
Extract **DINPUT8.dll** to the game directory. 	
 -  E.g. for sekiro.exe: "C:\Program Files (x86)\Steam\steamapps\common\Sekiro\"
 -  E.g. for DARKSOULS.exe: "C:\Program Files (x86)\Steam\steamapps\common\Dark Souls Prepare to Die Edition\DATA\"
 - E.g. for DarkSoulsIII.exe: "C:\Program Files (x86)\Steam\steamapps\common\DARK SOULS III\Game\"

# Compiling
This uses cmake. 
You will also need [minhook](https://github.com/TsudaKageyu/minhook) lib "installed" in your machine as a static lib.
You can obtain  [minhook](https://github.com/TsudaKageyu/minhook) via vcpkg by doing the following in the cli:
`vcpkg install minhook --triplet x64-windows-static`
(*note*: there were some [issues](https://github.com/microsoft/vcpkg/issues/12043) with this lib, but I believe the issues will be corrected quickly)

after all is installed create a `build` directory, `cd` into it and perform:
```
cmake .. -DCMAKE_TOOLCHAIN_FILE="C:/vcpkg/scripts/buildsystems/vcpkg.cmake" -DVCPKG_TARGET_TRIPLET="x64-windows-static"
```
You should now have a `.sln` file in the `build` directory (if you are using visual studio)


# Supported Versions
**Sekiro**
- v1.02

**Darksouls 1**
- v1.0.2.0
- debug version

**DarkSouls 3**
- v1.15
- v1.14
- v1.13
- v1.12
- v1.11
- v1.10
- v1.09
- v1.08
- v1.04

# Help

Q: The intro logo screens are still showing
A: Either the modified DINPUT8.dll is not in the correct directory or you are playing an unsupported version of the game.

# Source
All credit goes to the original [Author](https://github.com/bladecoding/DarkSouls3RemoveIntroScreens).
I just made some simple modifications.
