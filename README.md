This is a small guide for extracting and modifying assets or code from games made with the Unity engine. Feel free to contribute.

1. [Unity game folder structure](#unity-game-folder-structure)
2. [Extracting and editing code](#extracting-and-editing-code)
3. [Extracting assets](#extracting-assets)
4. [Hacking memory](#hacking-memory)

## Unity game folder structure

```
│   *.exe
└───*_Data
    │   globalgamemanagers
    │   globalgamemanagers.assets
    │   level0
    │   level0.resS
        ...
    |   levelN
    |   levelN.resS
    │   sharedassets0.assets
    │   sharedassets0.assets.resS
        ...
    |   sharedassetsN.assets
    |   sharedassetsN.assets.resS
    |   resources.assets
    ├───Managed
    │       Assembly-CSharp.dll
    │       Assembly-UnityScript.dll
    │       Mono.Security.dll
    │       mscorlib.dll
    │       System.Core.dll
    │       System.dll
    │       UnityEngine.dll
    │       UnityEngine.dll.mdb
    │       UnityEngine.Networking.dll
    │       UnityEngine.UI.dll
    ├───Mono
    │   │   mono.dll
    │   └───etc
    │       └───mono
    │           │   browscap.ini
    │           │   config
    │           ├───1.0
    │           │       DefaultWsdlHelpGenerator.aspx
    │           │       machine.config
    │           ├───2.0
    │           │   │   DefaultWsdlHelpGenerator.aspx
    │           │   │   machine.config
    │           │   │   settings.map
    │           │   │   web.config
    │           │   └───Browsers
    │           │           Compat.browser
    │           └───mconfig
    │                   config.xml
    └───Resources
            unity default resources
            unity_builtin_extra
```

\* : Name chosen during building

File/Directory | Description
--- | ---
*.exe | Executable file of the game
*_Data | Data folder containing the game resources
level0-levelN | Files containing game scenes data, each scene has its own file
sharedassets0-sharedassetsN | Game assets are split into sharedassets and .resS files
resources.assets | Assets found in the project resources folders and their dependencies are stored in this file
Managed | Folder containing unity DLLs
Assembly-CSharp.dll | DLL file containing compiled C# files
Assembly-UnityScript.dll | DLL file containing compiled UnityScript files

## Extracting and editing code

C# and UnityScript files are compiled into the Assembly-CSharp.dll and Assembly-UnityScript.dll DLLs respectively, which can be found inside the Managed folder.

DLLs can be decompiled using [ILSpy](http://ilspy.net/) or [dnSpy](https://github.com/0xd4d/dnSpy) which allow modifying and recompiling assembly files.

If DLLs are missing from the managed directory, try dumping them using this tool [MegaDumper](https://github.com/CodeCracker-Tools/MegaDumper)

## Extracting assets

Assets are stored in the .assets and .resS files. Content of these files can be unpacked with one of these tools :

Tool | Description
--- | ---
[UtinyRipper](https://github.com/mafaca/UtinyRipper) | uTinyRipper is a tool for extracting assets from serialized files (CAB-*, *.assets, *.sharedAssets, etc.) and assets bundles (*.unity3d, *.assetbundle, etc.) and conveting them into native Engine format.
[Unity Studio](https://github.com/RaduMC/UnityStudio) | A tool for exploring, extracting and exporting assets from Unity games and apps.
[Unity Assets Bundle Extractor](https://7daystodie.com/forums/showthread.php?22675-Unity-Assets-Bundle-Extractor) | UABE is a tool that allow modification of assets file and extraction of assets in usable formats (png/tga for textures, obj for meshes).
[Unity Assets Explorer](http://zenhax.com/viewtopic.php?f=9&t=36) | Can extract textures to .DDS format, meshes to .43 format.
[QuickBMS](http://aluigi.altervista.org/quickbms.htm) with [this script](http://aluigi.altervista.org/bms/unity.bms) or [this one for webplayer](http://aluigi.org/papers/bms/unity3d_webplayer.bms) |

#### DDS files :

The [DDS](https://en.wikipedia.org/wiki/DirectDraw_Surface) files can be opened/converted/edited with this [gimp plugin](http://registry.gimp.org/node/70) or this [photoshop plugin](https://developer.nvidia.com/nvidia-texture-tools-adobe-photoshop).

#### Another way of extracting meshes and textures :

Use [3D Ripper DX](http://www.deep-shadows.com/hax/3DRipperDX.htm) (doesn't support 64 bits binaries) or [Ninja Ripper](http://cgig.ru/en/2012/10/ho-to-use-ninja-ripper/).

## Hacking memory

Cheat engine have a feature called [Dissect mono](https://wiki.cheatengine.org/index.php?title=Mono) that can help hacking game's memory. This [video series](https://www.youtube.com/playlist?list=PLNffuWEygffbue0tvx7IusDmfAthqmgS7) about using cheat engine is really useful.
