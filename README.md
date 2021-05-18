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
    |   resources.assets
    |   resources.assets.resS
    |   resources.resource
    │   sharedassets0.assets
    │   sharedassets0.assets.resS
        ...
    |   sharedassetsN.assets
    |   sharedassetsN.assets.resS
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
sharedassets0-sharedassetsN | Game assets are split into sharedassets and .resS files (sharedassets.assets.split0 - ..splitN on platforms like Android/iOS)
resources.assets | Raw Assets found in the project resources folders and their dependencies are stored in this file (as well as raw audio files, even if outside of Resources folder in Unity, AudioClips with references to .resource and info such as audio size/offset still stored inside .assets)
Managed | Folder containing unity DLLs
Assembly-CSharp.dll | DLL file containing compiled C# files
Assembly-UnityScript.dll | DLL file containing compiled UnityScript files

## Extracting and editing code

C# and UnityScript files are compiled into the Assembly-CSharp.dll and Assembly-UnityScript.dll DLLs respectively, which can be found inside the Managed folder.

DLLs can be decompiled using [ILSpy](http://ilspy.net/) or [dnSpy](https://github.com/0xd4d/dnSpy) which allow modifying and recompiling assembly files.

If DLLs are missing from the managed directory, try dumping them using [Il2CppDumper](https://github.com/Perfare/Il2CppDumper) or [MegaDumper](https://github.com/CodeCracker-Tools/MegaDumper)

## Extracting assets

Assets are stored in the .assets and .resS files. Content of these files can be unpacked with one of these tools :

Tool | Description
--- | ---
[UtinyRipper](https://github.com/mafaca/UtinyRipper) | uTinyRipper is a tool for extracting assets from serialized files (CAB-*, *.assets, *.sharedAssets, etc.) and assets bundles (*.unity3d, *.assetbundle, etc.) and conveting them into native Engine format.
[Asset Studio](https://github.com/RaduMC/UnityStudio) | AssetStudio is a tool for exploring, extracting and exporting assets from Unity games and apps.
[Unity Assets Advanced Editor](https://github.com/Igor55x/UAAE) | UAAE is an advanced tool that based on UABE, but improves its functions.
[Unity Assets Bundle Extractor](https://github.com/DerPopo/UABE) | UABE is a tool that allow modification of assets file and extraction of assets in usable formats (png/tga for textures, obj for meshes).
[Unity Assets Explorer](http://zenhax.com/viewtopic.php?f=9&t=36) | Can extract textures to .DDS format, meshes to .43 format.
[QuickBMS](http://aluigi.altervista.org/quickbms.htm) with [this script](http://aluigi.altervista.org/bms/unity.bms) or [this one for webplayer](http://aluigi.org/papers/bms/unity3d_webplayer.bms) |
[DevXUnityUnpacker](https://devxdevelopment.com/Unpacker) | A (paid) tool with a friendly GUI meant for restoring unity projects by inputting the built game/app including a previewer for individual files as image, hex, text etc.
[UnityEX](https://yadi.sk/d/m3vFWoQ3j62Cr) | Tool for extracting/converting files from .assets bundles and replacing files (Mostly used for replacing textures).


#### DDS files :

The [DDS](https://en.wikipedia.org/wiki/DirectDraw_Surface) files can be opened/converted/edited with this [gimp plugin](http://registry.gimp.org/node/70) or this [photoshop plugin](https://developer.nvidia.com/nvidia-texture-tools-adobe-photoshop).

#### Another way of extracting meshes and textures :

Use [3D Ripper DX](http://www.deep-shadows.com/hax/3DRipperDX.htm) (doesn't support 64 bits binaries) or [Ninja Ripper](http://cgig.ru/en/2012/10/ho-to-use-ninja-ripper/).

Alternatives:
Tool | Tutorial
--- | ---
[RenderDoc](https://renderdoc.org/) | [Tutorial](https://www.youtube.com/watch?v=yPLxCm3SyPU) on how to use RenderDoc.
[Intel® Graphics Performance Analyzers](https://software.intel.com/content/www/us/en/develop/tools/graphics-performance-analyzers.html) | [Tutorial](https://forum.xentax.com/viewtopic.php?t=12262) on how to use the Intel Graphics Analyzers to extract graphics.

## Hacking memory

Cheat engine have a feature called [Dissect mono](https://wiki.cheatengine.org/index.php?title=Mono) that can help hacking game's memory. This [video series](https://www.youtube.com/playlist?list=PLNffuWEygffbue0tvx7IusDmfAthqmgS7) about using cheat engine is really useful.
