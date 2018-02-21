
# Skyrim Optimization Guide 2018

v1.0.0  
_by Ciathyza, 2018/01/26_  
Origin: [github.com/ciathyza/skyrim-optimization-guide-2018](https://github.com/ciathyza/skyrim-optimization-guide-2018)

### Table of Contents
  1. Introduction
  2. System Preparation & Optimization
  3. Software & Tools
  4. Graphics Driver Settings
  5. Ini File Optimization
  6. Essential Bug fixes & Patches
  7. Graphics Modding & Optimization
  8. Modding Tips
  9. Essential Mods
  10. Troubleshooting
  11. Useful Links

---

### 1. Introduction

This document is designed to provide a complete and comprehensive guide for modding and optimizing Skyrim LE (Legendary Edition) that goes into great detail of tweaking the game to provide a stable and visually high-end gameplay which still runs at a fluid framerate.

This guide assumes a fairly good grasp of handling and understanding Windows-related file operations.

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

  - **Unpack BSAs**: In Mod Organizer's plugin settings you can enable the BSA Unpacker. I recommend this and have Mod Organizer unpack any BSAs when a mod is being installed. This allows you to see which files of the mod are conflicting (override or being overridden) with other mods and you can more easily decide which mod should take preference, ignore certain files, etc.
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

---

### 4. Graphics Driver Settings

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
| Maximum pre-rendered frames                         | 1                       |
| Monitor Technology                                  | Fixed Refresh           |
| Multi-Frame Sampled AA (MFAA)                       | On                      |
| OpenGL rendering GPU                                | Auto-select             |
| Power management mode                               | Optimal power           |
| Preferred refresh rate                              | Application-controlled  |
| Shader Cache                                        | Use global setting (On) |
| Texture filtering - Anisotropic sample optimization | Off                     |
| Texture filtering - Negative LOD bias               | Clamp                   |
| Texture filtering - Quality                         | High quality            |
| Texture filtering - Trilinear optimization          | On                      |
| Threaded optimization                               | On                      |
| Triple buffering                                    | On                      |
| Vertical sync                                       | On                      |
| Virtual Reality pre-rendered frames                 | 1                       |

### 5. Ini File Optimization

#### 5.1 Skyrim.ini

```
[Display]
fSunShadowUpdateTime=1
fSunUpdateThreshold=0.05
```

  - `fSunShadowUpdateTime`: Determines the time in seconds at which the sun position is updated which in turn causes the shadow to move.
  - `fSunUpdateThreshold`: Determines the time between sun-shadow transitions. A value of 0.05 is equal to 1 second, so a value of 1 equals 20 seconds and a value of 0.005 equals 100 milliseconds. Increasing this also increases the distance the shadows will move during the transition.

#### 5.2 Skyrimprefs.ini

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


#### 5.3 SKSE.ini

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

### 6. Essential Bug Fixes & Patches

#### 6.1 Crash Fixes Mod & SKSE Plugin Preloader

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

### 7. Graphics Modding & Optimization

#### ENB

---

### 8. Modding Tips

#### General Load Order

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

### 9. Essential Mods

---

### 10. Troubleshooting

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

### 11. Useful Links
