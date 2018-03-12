
# Skyrim Modding & Optimization Guide 2018

v1.0.0  
_by Ciathyza, 2018/01/26_  
Origin: [github.com/ciathyza/skyrim-optimization-guide-2018](https://github.com/ciathyza/skyrim-optimization-guide-2018)

### Table of Contents
  1. Introduction
  2. System Preparation & Optimization
  3. Software & Tools
  4. Ini File Optimization
  5. Essential Bug fixes & Patches
  6. Graphics Modding & Optimization
  7. Modding Tips
  8. Essential Mods
  9. Troubleshooting
  10. Useful Links

---

### 1. Introduction

This document is designed to provide a complete and comprehensive guide for modding and optimizing Skyrim LE (Legendary Edition) by going into great detail of tweaking the game to provide a visually high-end and rich dynamic gameplay while still running stable and at a fluid framerate.

The aim of this guide is to provide a reliable walkthrough to create a base mod setup that consists of an ENB, tweaked for gameplay but visually pleasing, texture and mesh replacements, UI tweaks, weather mods, animations, and various gameplay-enhancing mods. This base setup can then be used to build on and add secondary mods, such as companions, houses, quests, etc.

This guide assumes a fairly good grasp of handling and understanding Windows-related file operations ans being familiar with Mod Organizer.

#### Why Skyrim LE?

#### Hardware Reference

As a reference, this guide is based on the following system (measured with [www.userbenchmark.com](http://www.userbenchmark.com)):

  - CPU: Intel Core i7-7700K @ 4.2GHz
  - GPU: Zotac GTX 1080
  - SSD: Transcend TS1TSSD370S 1TB
  - SSD: Samsung 850 Evo 1TB
  - HDD: WD Black 1TB
  - RAM: Corsair Vengeance LPX DDR4 3000 C15 2x16GB
  - MBD: Asus MAXIMUS IX HERO
  - OS: Windows 10 64bit
  - UserBenchmarks: Game 119%, Desk 105%, Work 88%

---

### 2. System Preparation & Optimization

---

### 3. Software & Tools

The following list provides an overview of the most important tools used for modding Skyrim.

#### 3.1 Skyrim Script Extender (SKSE)

Needless to say that you need this since many mods will require SKSE. Download the zipped version from [skse.silverlock.org](http://www.userbenchmark.com), unzip and copy the following files into your Skyrim install folder (e.g. `C:\Program Files (x86)\Steam\steamapps\common\Skyrim`).

```
skse_1_9_32.dll
skse_loader.exe
skse_steam_loader.dll
```

Install the SKSE `Script` folder incl. contents with Mod Organizer (see below) into a dedicated mod entry. **Do this step after you've installed Mod Organizer (We install SKSE before MO so that MO automatically picks up the SKSE loader)!** Simply zip the Scripts folder and then install it with Mod Organizer (Install a new mod from an archive) into a new mod entry named `SKSE` or something similar.

#### 3.2 Mod Organizer

Do yourself a favor and save a lot of headache while modding Skyrim by using **Mod Organizer** as your mod manager. As a matter of fact this guide assumes that you're using Mod Organizer. Contrary to what some guides and users will tell you Mod Organizer isn't hard to understand or hard to use. The important concept to understand with Mod Organizer is that it virtualizes the `Data` folder of Skyrim. What this means is that Mod Organizer stores all installed mods separately, each in its own folder and when Skyrim is launched via Mod Organizer it creates a 'virtual' file structure that resembles the `Data` folder as if all mods were installed physically into it. The advantage is that no files are ever physically overwritten and your Skyrim install folder never gets modified by Mod Organizer which makes modding non-destructive. Mod Organizer will 'override' (not 'overwrite') mod files that are lower in the load order with same-named files that are higher in the load order and thanks to the non-destructiveness you are able to move mods around in the load order without any loss of files. This makes it much easier to experiment with different load orders. This is the biggest advantage of Mod Organizer but by far not the only.

By using the latest version of Mod Organizer (at the time of this writing v2.1.1) you are also able to use one Mod Organizer installation to properly manage all your Bethesda RPGs (Skyrim, Skyrim SE, Fallout 4, Oblivion, Fallout New Vegas) so you don't have to fumble around with multiple, standalone Mod Organizer installs.

##### Download

Get the latest version of Mod Organizer at [github.com/LePresidente/modorganizer/releases](https://github.com/LePresidente/modorganizer/releases)

Download the installer .exe and install it wherever you normally install your program files. Since Mod Organizer 2 is 64bit it will go into `C:\Program Files\ModOrganizer` by default.

##### USVFS

**Optional but recommended**: you might want to join the `ModOrganizerDevs` chat channel on Discord ([discordapp.com/invite/JdQvBtn](https://discordapp.com/invite/JdQvBtn)). Not only can you get modding-related help from other users there but the `#builds` room provides a download link to the latest USVFS beta version and that's the one you want to use unless there is a final non-beta available in the future.

USVFS is the file system component that Mod Organizer uses for its file virtualization. If you download the latest version of USVFS (e.g. link named `usvfs 0.3.1-beta5`) you need to unpack the files and manually copy them to your Mod Organizer installation directory. The files needs are:

```
usvfs_proxy_x64.exe
usvfs_proxy_x86.exe
usvfs_x64.dll
usvfs_x86.dll
```
You can delete the old `usvfs_proxy.exe`/`usvfs.dll` afterwards.

##### SKSE Launch Argument

If you've installed SKSE before Mod Organizer then MO should have picked it up automatically and created an SKSE entry under *Launchable Executables* (the blue/green gears icon) for you. If you use the Skyrim Steam version you should add the `-forcesteamloader` argument to the SKSE launch entry:

  1. Click on "Configure the executables..." button (green/blue gears icon).
  2. Select SKSE.
  3. Add `-forcesteamloader` in argument field.
  4. Click on 'modify'.
  5. Close.

##### Mod Organizer Tips

  - **Unpacking BSAs**: In Mod Organizer's plugin settings you can enable the BSA Unpacker. This allows you to see which files of the mod are conflicting (override or being overridden) with other mods and you can more easily decide which mod should take preference, ignore certain files, etc. HOWEVER: loading loose files instead of BSAs has shown to be not only slower but also makes loading unstable in some cases. Therefore I recommend to leave BSAs packed if a mod comes with a BSA. Only mods that override existing asset files use unpacked files, everything else can safely stay inside a BSA archive.
  - **Virtual File Access**: Configure your favorite file manager (e.g. [Directory Opus](https://www.gpsoft.com.au/)) to launch via Mod Organizer. This gives you access to the file structure of the *Data* folder as Skyrim will see it when launched. It enables you to browse the asset files that are ultimately used by the game. Then You could for example use a [DDS viewer](https://resource.dopus.com/t/simple-dds-viewer-plugin/2515) to check the textures, etc. Note that this won't work with the Windows Explorer as that Windows process is already running in memory by default so Mod Organizer can't hook its virtualized file system to it. You need an app that is launched and that quits later on.
  - **Mod Files Location**: As hinted before, Mod Organizer stores downloaded/installed mods separately from the Skyrim installation directory. The default location for all your Mod Organizer Skyrim-related files is at `C:\Users\yourusername\AppData\Local\ModOrganizer\Skyrim`. Mod Organizer allows you to store these files in a different location **but it is recommended to have all installed mods on the same physical hard disk on which your Skyrim is installed**. If you store your installed mods on a different drive Skyrim will have to access files from two different drives which will decrease load performance.

#### 3.3 LOOT

LOOT is a tool used to sort the load order of ESP files. It uses a master list with information about many published mods to arrange the files into a (hopefully) conflict-free order. It does a fairly good job at ordering your files but depending on the mods you install there might be exceptions where you still have to order manually afterwards. In my experience I found that I always have to order several mods manually and/or tell LOOT that it should place a specific mod after some others so know that you can't blindly rely on it. In addition LOOT is very useful to let you know of mods that need to be cleaned with TESEdit.

Download LOOT from [github.com/loot/loot/releases](https://github.com/loot/loot/releases/)

Install it and then add an executable link in Mod Organizer so that you can launch LOOT via Mod Organizer and it 'sees' the virtualized mod files.

*Note*: Mod Organizer ships with its own LOOT integration but it's better to use the standalone LOOT because it is updated more frequently.

#### 3.4 TES5Edit

TES5Edit is used to clean ESP files and can also be used to make other modifications to ESP files. Download it from [www.nexusmods.com/skyrim/mods/25859](https://www.nexusmods.com/skyrim/mods/25859), install it and add a link in Mod Organizer just like you did with LOOT.

#### 3.5 Wrye Bash

While Wrye Bash can be used for a lot of mod-related purposes, the main reason for our use is to create bashed patches which are required by some mods. Download it from [www.nexusmods.com/skyrim/mods/1840](https://www.nexusmods.com/skyrim/mods/1840), install it and add a link in Mod Organizer just like you did with LOOT.

#### 3.6 Merge Plugins

Another tool at our disposal, Merge Plugins is used to merge ESP files together as a workaround to the 256 ESP limit that Skyrim's engine has. By merging multiple compatible ESPs together we can exceed this limit. Download it from [www.nexusmods.com/skyrim/mods/69905](https://www.nexusmods.com/skyrim/mods/69905), install it and add a link in Mod Organizer just like you did with LOOT.

#### 3.7 Save Game Script Cleaner

A tool that can help with savegame cleaning in case you want to remove or update mods while actually playing Skyrim for a change ;). Download it from [www.nexusmods.com/skyrim/mods/52363](https://www.nexusmods.com/skyrim/mods/52363), install it and add a link in Mod Organizer just like you did with LOOT.

#### 3.8 ENB And Reshade Manager

This tool can be used to backup and restore all ENB-related files from the Skyrim folder and create presets to easily switch ENBs. A real time saver!
Download it from [www.nexusmods.com/skyrimspecialedition/mods/4143](https://www.nexusmods.com/skyrimspecialedition/mods/4143) and install it. No need to run it via Mod Organizer since MO doesn't manage files that are located directly in the Skyrim root folder.

#### 3.9 Bethini

A tool that creates clean ini files that are up-to-date with the latest knowledge about Skyrim's ini settings. It's recommended to create fresh ini files with this tool and then adapt them to your preference (disable the game controller for example). Download at [www.nexusmods.com/skyrim/mods/69787](https://www.nexusmods.com/skyrim/mods/69787).

---

### 4. Ini File Optimization

#### 4.1 Skyrim.ini

```
[Display]
fSunShadowUpdateTime=1
fSunUpdateThreshold=0.05
```

  - `fSunShadowUpdateTime`: Determines the time in seconds at which the sun position is updated which in turn causes the shadow to move.
  - `fSunUpdateThreshold`: Determines the time between sun-shadow transitions. A value of 0.05 is equal to 1 second, so a value of 1 equals 20 seconds and a value of 0.005 equals 100 milliseconds. Increasing this also increases the distance the shadows will move during the transition.

#### 4.2 Skyrimprefs.ini

```
[Display]
iBlurDeferredShadowMask=16
iMaxAnisotropy=0
iMaxDecalsPerFrame=400
iMaxSkinDecalsPerFrame=100
iMultiSample=0
iShadowFilter=4
iShadowMapResolution=8192
```


#### 4.3 SKSE.ini

Find SKSE.ini by going into Mod Organizer, double-click your SKSE mod (as mentioned in 3.1), Filetree tab, under *SKSE/SKSE.ini*. If the file isn't there, create it. Make sure the file reflects the following settings:

```
[Display]
iTintTextureResolution=2048

[General]
ClearInvalidRegistrations=1
EnableDiagnostics=1
```

  - `iTintTextureResolution`: Set this to `2048`. If you get pixelated lips on your character, either delete this line or find the size of your used tint map texture and update the value here.
  - `ClearInvalidRegistrations`: When turned on SKSE tries to clean unused scripts which is good! Set this to `1`.
  - `EnableDiagnostics`: If set to `1` SKSE shows missing ESPs when a savegame is loaded.
  - `DefaultHeapInitialAllocMB` and `ScrapHeapSizeMB` are obsolete since **meh321's Crash fixes mod** (more below) completely replaces the SKSE memory patch. Therefore these two values should be removed from *SKSE.ini*.

---

### 5. Essential Bug Fixes & Patches

#### 5.1 Crash Fixes Mod & SKSE Plugin Preloader

If you were cursing at your heavily modded Skyrim crashing approx. every 30 minutes there is finally a cure for you! These two amazing tweaks will likely fix most of your Skyrim LE crashes. The Crash Fixes mod eliminates 99.9% of crashes for me and it will most likely for you!

  - [Crash Fixes by meh321](https://www.nexusmods.com/skyrim/mods/72725/?)
  - [SKSE Plugin Preloader](https://www.nexusmods.com/skyrim/mods/75795/?)

##### Installation
  1. Extract **SKSE Plugin Preloader**, copy `d3dx9_42.dll` into your Skyrim folder (where `TESV.exe` is located).
  2. Install **Crash fixes by meh321** with Mod Organizer.
  3. In Mod Organizer check if you have a file named `CrashFixPlugin_preload.txt` in `SKSE\Plugins` (besides `CrashFixPlugin.ini` and `CrashFixPlugin.dll`), if not, create it (can be an empty file).
  4. Open `CrashFixPlugin.ini`, and set `UseOSAllocators` to `1`. Save the file.
  5. Done!

The Crash fixes mod fixes many of the bugs, see the mod's website and `CrashFixPlugin.ini` for details. The SKSE Plugin Preloader makes sure that mods are loaded before game initialization for which it finds the `_preload.txt` file.

---

### 6. Graphics Modding & Optimization

#### 6.1 Graphics Driver Settings

These settings are for Nvidia users. As I don't use a AMD card I cannot provide any settings for these. Sorry for that!

Go to your Nvidia graphics card driver settings (right-click on desktop, choose Nvidia Control Panel) and under 3D settings choose the application-specific settings for Skyrim (tesv.exe). The following table tells you about the recommended settings.

| Nvidia Setting                                      | Recommended Value       |
|:----------------------------------------------------|:------------------------|
| Ambient Occlusion                                   | Off                     |
| Anisotropic Filtering                               | 8x                      |
| Antialiasing - FXAA                                 | Not supported           |
| Antialiasing - Gamma correction                     | On                      |
| Antialiasing - Mode                                 | Application-controlled  |
| Antialiasing - Setting                              | Use global setting      |
| Antialiasing - Transparency                         | 8x (supersample)        |
| CUDA - GPUs                                         | Use global setting      |
| Maximum pre-rendered frames                         | Application-controlled  |
| Monitor Technology                                  | Fixed Refresh           |
| Multi-Frame Sampled AA (MFAA)                       | On                      |
| OpenGL rendering GPU                                | Auto-select             |
| Power management mode                               | Optimal power           |
| Preferred refresh rate                              | Application-controlled  |
| Shader Cache                                        | On                      |
| Texture filtering - Anisotropic sample optimization | Off                     |
| Texture filtering - Negative LOD bias               | Clamp                   |
| Texture filtering - Quality                         | High quality            |
| Texture filtering - Trilinear optimization          | On                      |
| Threaded optimization                               | On                      |
| Triple buffering                                    | Off                     |
| Vertical sync                                       | On                      |
| Virtual Reality pre-rendered frames                 | Application-controlled  |

##### For G-Sync Users

If you have a G-Sync capable monitor it's recommend to use G-Sync and vertical sync together because it will solve any performance limitations introduced by VSync. It is recommended to use both. Read [this guide](https://www.blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/14/) to see why. To use G-Sync with Skyrim you need to make the following tweaks:

In Skyrim.ini, disable vertical sync:
```
iPresentInterval=0
```

In enblocal.ini, disable vertical sync and FPS limiter:
```
EnableVSync=false
EnableFPSLimit=false
```

In Nvidia graphics card driver settings change these settings accordingly:

| Nvidia Setting                                      | Recommended Value       |
|:----------------------------------------------------|:------------------------|
| Monitor Technology                                  | GSync                   |
| Vertical sync                                       | On                      |

After this you should still limit the framerate to 57 FPS but since ENB's FPS limiter has proven not to be very reliable for me I recommend to use the FPS limiter from [Nvidia Inspector](https://www.guru3d.com/files-details/nvidia-inspector-download.html) instead. So download and run Nvidia Inspector, go into the Driver Profile Settings, select the profile for `Elder Scrolls V: Skyrim` and look for a setting named `Frame Rate Limiter`. Set it to a value around 57. Setting it to 57 instead of 60 will reduce input lag (at least if the game is running at full FPS).

After these tweaks Skyrim should run properly with GSync and in-game physics should not go bonkers either. Your monitor will now refresh the image according to what FPS the game is currently running at, thus eliminating tearing and any performance drawbacks introduced by VSync solely.

#### 6.2 Monitor Calibration

#### 6.3 ENB

The goal of this section is to install Rudy ENB and tweak it for optimal quality and performance on your system. Additionally we will replace the ENB's DoF (Depth of Field) with that of RealVision ENB. The reason for this is that while Rudy ENB's DoF looks great it's not well suited for gameplay. The DoF uses a center point to determine whether to apply DoF or not and it generally is only good for screen archery but not for constant camera movement. RealVision's DoF on the other works very well even with a lot of camera movement.

Rudy ENB is a good allround ENB that's very tweakable and delivers an excellent image with beautiful colors and sharpness of textures. It's also relatively performant and modern and has support for various weather and lighting mods.

#### 6.4 Texture & Mesh Replacers

#### 6.5 LODs

LODs (Level Of Detail) are textures that are smaller and more resource-friendly than their full size counterparts and which are rendered by the game engine instead of hires textures when a textured object is far away from the player and texture detail isn't important because the object is in the distance. The difference between LODs and mipmaps is that LODs are actually not only lowres textures but also simplified meshes on which the textures are applied. Skyrim uses LODs for all large objects like rocks, trees, ground, houses, etc. to reduce the burden on the GPU. LODs can be generated with different levels of resolution and quality and this section walks you through generating the best-posssible LODs that wont eat up too much of your available VRAM. We will use three different tools to accomplish this: TES5LODGen, TexGen, and DynDOLOD and we set up these tools in Mod Organizer so that re-generating LODs will take the least amount of efforts because you will need to re-generate LODs from time to time after you installed new texture packs or mods like houses or city improvements, etc.

First get the tools and install them in a location where you keep all your modding tools.

  - [TES5LODGen](https://www.nexusmods.com/skyrim/mods/62698)
  - [DynDOLOD](https://www.nexusmods.com/skyrim/mods/59721) (TextGen is included. Also download the **DynDOLOD Resources** package over Mod Organizer!)

After that you want to create three empty mods in Mod Organizer (right-click on left list and chose 'Create Empty Mod'). Respectively name them:

  - TES5LODGen Generated LODs
  - TexGen Generated Files
  - DynDOLOD Generated LODs

Next you link the three tools to Mod Organizer so that you can launch them over MO and so they place generated files right into the empty mods you've just created.

---

### 7. Modding Tips

#### 7.1 Mod Installation Best Practices

If you want to eliminate mod conflicts and game issues you must be pragmatic when installing mods. The approach described here recommends to install mods in a certain order, one by one, testing them early, and fix issues early. This means that you download and install the most essential mods first and after that start to install other mods following a certain order and test them in-game before installing new mods. As you keep (mostly) relying on LOOT to sort your mod order you will see that it's easier to see changes in the mod order with few new mods rather than after installing multiple mods and have LOOT order it all over the place, screwing up mods that do require manual ordering. Luckily you are using Mod Organizer so you can change the mod order non-destructively at any time but you should still proceed with care because with many mods installed all at once and not checking for issues in between it will be very difficult to figure out which mod causes problems later.

Here are some general rules that should be followed for a clean and smooth running mod setup:

  - Don't unpack BSAs when installing mods! It's generally better for performance and stability to load assets from BSAs. Only unpack if you absolutely want files from BSAs to override loose files!
  - If a mod contains doc files (readmes, screenshots, etc.) create a folder named _Docs_ and move these files into it. Then set the Docs folder as hidden (MO will add the extension _.mohidden_ to it). Do the same with _Source_ folders. This will have MO ignore all these mod-unrelated files.
  - You can install additional ESP files for a mod and set them as optional in MO if they are not required or if you need them later as a dependency for another mod.

##### Installation Order

  1. Modder Resources
  2. Bugfixes & Patches
  3. 


#### 7.2 General Load Order

It's a good idea to define a categorical mod order in Mod Organizer to prevent chaos from ruling your mod list. However due to the nature of Skyrim mods (assets & ESP files) it's not always possible to follow a strict order since you will have to move textures and ESPs around to suit your mod overrides but you can set up a 'rough' order that follows some mod categories. For example you want texture replacers late in your mod order and mods that only contain SKSE plugins can be anywhere since they don't adhere to a specific load ordering. Here is a categorical order that I'm following for the mod entries in the left pane in Mod Organizer:

```
Official Update
Official DLCs (TESEdit-Cleaned)
---------------------------------------
Unofficial Patches
---------------------------------------
Essential (Mod Resources, Bug fixes)
---------------------------------------
New Lands
Areas
Cities
Mercantile
Player Houses
---------------------------------------
Creatures
NPCs
Followers
---------------------------------------
Items & Weapons
Clothing & Armor
---------------------------------------
Textures & Models
Weather
User Interface
Audio
---------------------------------------
Animations
Character Customization
---------------------------------------
Crafting
Quests
Gameplay
---------------------------------------
Top Priority
---------------------------------------
LOD
---------------------------------------
Generated (FNIS, SKSE Configs, etc.)
```

Note that you still have to make some exceptions for specific mods. Several of my mods don't work or look right unless I place them on a higher priority than they would be in their respective category so I order them under *Top Priority*.

---

### 8. Essential Mods

---

### 9. Troubleshooting

  - **Issue**: The lips on my character's skin are pixelated.
  **Solution**: Find the texture used for the lips tint mask and check its texture size. Edit *SKSE.ini* and set `iTintTextureResolution` to the size (e.g. 1024, 2048, etc).

  - **Issue**: Skyrim takes screenshots whenever I press the <key>End</key> key (In particular frustrating if you're a left-hander using the End key as your 'Use' key).
  **Solution**: You most likely have an ENB installed that contains a file named *injector.ini*. It is there where this obnoxious keyboard shortcut hides. You might want to remove all the keyboard assignments defined in this file:

```
[injector]
;toggle shader keycode
key_toggle =

;make screenshot keycode
key_screenshot =

;reload shader files keycode
key_reload =
```

---

### 10. Useful Links
