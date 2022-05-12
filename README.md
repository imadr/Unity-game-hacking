# Unity Game Hacking Guide

This is a small guide for extracting and modifying assets or code from games made with the Unity engine. Feel free to contribute.

1. [Unity game folder structure](#unity-game-folder-structure)
2. [Extracting and editing code](#extracting-and-editing-code)
3. [Extracting assets](#extracting-assets)
4. [Hacking memory](#hacking-memory)


## Unity game folder structure

```
│  *.exe
└──*_Data
   │  globalgamemanagers
   │  globalgamemanagers.assets
   │  level0
   │  level0.resS
      ...
   |  levelN
   |  levelN.resS
   |  resources.assets
   |  resources.assets.resS
   |  resources.resource
   │  sharedassets0.assets
   │  sharedassets0.assets.resS
      ...
   |  sharedassetsN.assets
   |  sharedassetsN.assets.resS
   ├──Managed
   │    Assembly-CSharp.dll
   │    Assembly-UnityScript.dll
   │    Mono.Security.dll
   │    mscorlib.dll
   │    System.Core.dll
   │    System.dll
   │    UnityEngine.dll
   │    UnityEngine.dll.mdb
   │    UnityEngine.Networking.dll
   │    UnityEngine.UI.dll
   ├──Mono
   │  │  mono.dll
   │  └──etc
   │     └──mono
   │        │  browscap.ini
   │        │  config
   │        ├──1.0
   │        │     DefaultWsdlHelpGenerator.aspx
   │        │     machine.config
   │        ├──2.0
   │        │  │  DefaultWsdlHelpGenerator.aspx
   │        │  │  machine.config
   │        │  │  settings.map
   │        │  │  web.config
   │        │  └──Browsers
   │        │        Compat.browser
   │        └──mconfig
   │              config.xml
   └──Resources
        unity default resources
        unity_builtin_extra
```

File/Directory | Description
--- | ---
*.exe | Executable file of the game
`*_Data` | Data folder containing the game resources
level0-levelN | Files containing game scenes data, each scene has its own file
sharedassets0-sharedassetsN | Game assets are split into sharedassets and .resS files (sharedassets.assets.split0 - ..splitN on platforms like Android/iOS)
resources.assets | Raw Assets found in the project resources folders and their dependencies are stored in this file (as well as raw audio files, even if outside of Resources folder in Unity, AudioClips with references to .resource and info such as audio size/offset still stored inside .assets)
`Managed` | Folder containing unity DLLs
Assembly-CSharp.dll | DLL file containing compiled C# files
Assembly-UnityScript.dll | DLL file containing compiled UnityScript files

With ``*`` : The name of the main executable (.exe).


## Extracting and editing code

C# and UnityScript files are compiled into the Assembly-CSharp.dll and Assembly-UnityScript.dll DLLs respectively, which can be found inside the `Managed` folder.

DLLs can be decompiled using ILSpy, dnSpy, DotPeek or JustAssembly which allow modifying and recompiling assembly files.

If DLLs are missing from the managed directory, try dumping them using MegaDumper tool.

Tool | Decription
--- | ---
[ILSpy](https://github.com/icsharpcode/ILSpy) | Cross-platform .NET Decompiler with support for PDB generation, ReadyToRun, Metadata (&more).
[DotPeek](https://www.jetbrains.com/decompiler/) | JetBrains DotPeek is a free .NET Decompiler and Assembly Browser.
[dnSpyEx](https://github.com/dnSpyEx/dnSpy) | Unofficial revival of the well known .NET debugger and assembly editor, dnSpy. <br /> **Fork of ``dnSpy``.**
[Telerik JustAssembly](https://www.telerik.com/justassembly) | Decompile and Compare .NET Assemblies. Binary Code Diff. Method Diff.
[Cpp2IL](https://github.com/SamboyCoding/Cpp2IL) | Work-in-progress tool to reverse unity's IL2CPP toolchain.
[Il2CppDumper](https://github.com/Perfare/Il2CppDumper) | Unity il2cpp reverse engineer. 
[dnSpy](https://github.com/dnSpy/dnSpy) <br /> ![No Longer Maintained](https://img.shields.io/badge/No%20Longer%20Maintained-red.svg) | dnSpy is a debugger and .NET assembly editor. You can use it to edit and debug assemblies even if you don't have any source code available. <br /> **Working but you can use ``dnSpyEx`` instead.**
[MegaDumper](https://github.com/CodeCracker-Tools/MegaDumper)  <br /> ![No Longer Maintained](https://img.shields.io/badge/No%20Longer%20Maintained-red.svg) | Dump native and .NET assemblies.


## Extracting assets

Assets are stored in the .assets and .resS files.
Content of these files can be unpacked with one of these tools :

Tool | Description
--- | ---
[AssetRipper](https://github.com/AssetRipper/AssetRipper) | AssetRipper is a tool for extracting assets from serialized files (CAB-*, *.assets, *.sharedAssets, etc.) and assets bundles (*.unity3d, *.bundle, etc.) and converting them into the native Unity engine format. <br /> **Fork of ``uTinyRipper``.**
[Unity Assets Bundle Extractor](https://github.com/SeriousCache/UABE) | UABE is an editor for 3.4+/4/5/2017-2021.3 .assets and AssetBundle files. It can create standalone mod installers from changes to .assets and/or bundles.
[QuickBMS](https://aluigi.altervista.org/quickbms.htm) with [this script](https://aluigi.altervista.org/bms/unity.bms) or [this one for webplayer](https://aluigi.altervista.org/bms/unity3d_webplayer.bms) | universal script based files extractor and reimporter. QuickBMS supports tons of games and file formats, archives, encryptions, compressions, obfuscations and other algorithms.
[DevXUnityUnpacker](https://devxdevelopment.com/Unpacker) | A (paid) tool with a friendly GUI meant for restoring unity projects by inputting the built game/app including a previewer for individual files as image, hex, text etc.
[uTinyRipper](https://github.com/mafaca/UtinyRipper) <br /> ![No Longer Maintained](https://img.shields.io/badge/No%20Longer%20Maintained-red.svg) | uTinyRipper is a tool for extracting assets from serialized files (CAB-\*, \*.assets, \*.sharedAssets, etc.) and assets bundles (\*.unity3d, \*.assetbundle, etc.) and conveting them into native Engine format. <br /> **Use ``AssetRipper`` Instead**
[Unity Studio / AssetStudio](https://github.com/RaduMC/AssetStudio) <br /> ![No Longer Maintained](https://img.shields.io/badge/No%20Longer%20Maintained-red.svg) | AssetStudio is an independent tool for exploring, extracting and exporting assets.
[Unity Assets Explorer](https://zenhax.com/viewtopic.php?t=36) <br /> ![No Longer Maintained](https://img.shields.io/badge/No%20Longer%20Maintained-red.svg) | Unity Assets Explorer is used to view the contents of Assets-files (Unity 3D engine). Allows you to: Extract all files, extract one file (from context menu), convert tex-files into a picture format DDS (on extraction), import the changed DDS-images to the archive.

> **Do not use UnityEX**, it is most likely a virus.

### DDS files :

The [DDS](https://en.wikipedia.org/wiki/DirectDraw_Surface) files can be opened/converted/edited with the following tools :

Tool | Tutorial
--- | ---
[Ninja Ripper](https://ninjaripper.com/) | Extract (rip) 3D scenes from games and explore them in 3D editor (Blender, 3D Max, Noesis). <br /> [An old guide](http://cgig.ru/en/2012/10/ho-to-use-ninja-ripper/) on how to use Ninja Ripper. <br /> The official [YouTube Channel](https://www.youtube.com/channel/UCgT-ET20KlC4AcECNtW9gyw) can be usefull for latest video tutorial.
[RenderDoc](https://renderdoc.org/) | [Tutorial](https://www.youtube.com/watch?v=yPLxCm3SyPU) on how to use RenderDoc.
[NVIDIA Texture Tools Exporter](https://developer.nvidia.com/nvidia-texture-tools-exporter) | The NVIDIA Texture Tools Exporter allows users to create highly compressed texture files - that stay small both on disk and in memory - directly from image sources using NVIDIA’s CUDA-accelerated Texture Tools 3.0 compressor technology. <br /> **Can be used as a standalone software or as an Adobe Photoshop Plugin**.
[Intel® Graphics Performance Analyzers](https://www.intel.com/content/www/us/en/developer/tools/graphics-performance-analyzers/overview.html) | Improve your game's performance by quickly identifying problem areas. <br /> [Tutorial](https://forum.xentax.com/viewtopic.php?t=12262) on how to use the Intel Graphics Analyzers to extract graphics.
[Gimp Plugin](https://code.google.com/archive/p/gimp-dds/downloads) | This is a plugin for GIMP version 2.8.x. It allows you to load and save images in the Direct Draw Surface (DDS) format.
[3D Ripper DX](http://www.deep-shadows.com/hax/3DRipperDX.htm) | This soft doesn't support 64 bits binaries.


## Hacking memory

Cheat engine have a feature called [Dissect mono](https://wiki.cheatengine.org/index.php?title=Mono) that can help hacking game's memory. This [video series](https://www.youtube.com/playlist?list=PLNffuWEygffbue0tvx7IusDmfAthqmgS7) about using cheat engine is really useful.
