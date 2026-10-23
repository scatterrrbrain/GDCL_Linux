# Grim Dawn Community League setup guide for linux gamers

- Updated 2026-10-24, ready for Season 8.

This guide will focus on setting up GDCL S8 launcher as a non-steam game in Steam.

<img width="1271" height="559" alt="GDCL_Steam_preview" src="https://github.com/user-attachments/assets/eef9f2f6-bfa2-478f-b4ef-b6f8c813967c" />

# Pre-requisites
Download the Community League Launcher from the [GDCL website][https://www.grimdawnleague.com/#/about]. 
Make sure to read the about page for general instructions and check out the 
GDCL [discord][https://discord.gg/n94PcmV] if you have questions etc.

## 1. Unzip the GDCommunityLauncher.zip into your Grim Dawn installation folder
- You can easily find this by right clicking on your Grim Dawn steam icon and
navigating to
```
Manage -> Browse Local Files
```
<img width="480" height="405" alt="browselocalfiles" src="https://github.com/user-attachments/assets/eb551ee8-7731-49dc-814f-a012fe7a49f4" />

- The default installation path is something like
```
~/.local/share/Steam/steamapps/common/Grim Dawn/
```

- Make sure the unzipped launcher files 'GDCommunityLauncher.exe' etc. are in
the same folder as your Grim Dawn.exe!

## 2. Add 'GDCommunityLauncher.exe' as a non-steam game in Steam

- You can either do this manually, or by using my [GDCL_Steam][https://github.com/scatterrrbrain/GDCL_Steam] bootstrapper.
Note that the bootstrapper is currently experimental!

### Manual

<img width="1907" height="1009" alt="nonsteamgame" src="https://github.com/user-attachments/assets/64457ee6-d1cd-4ebd-9316-a989fff0f18e" />

- Navigate to bottom left of your Steam game library.
  ```
  -> 'Add a Game' -> 'Add a Non-Steam Game' -> 'Browse'
  ```  

- Navigate to your Grim Dawn installation folder and select 'GDCommunityLauncher.exe'

- Click 'Add Selected Programs'

<img width="695" height="642" alt="nonsteambrowse" src="https://github.com/user-attachments/assets/e97b8bec-5539-4312-a934-4c729f0cb213" />

### Bootstrapper
- Read the bootstrapper documentation! This handles a lot of the tedious steps (if it works...).

## Game and Proton setup
- Navigate to the Steam properties page of the newly added 'GDCommunityLauncher.exe' "game"
in your Steam Game Library.

### Shortcut
- You can rename the shortcut used by Steam. For example 
```
'GDCommunityLauncher.exe' -> 'Grim Dawn Community League' .
```

- You can set the small side-panel icon used by Steam by clicking the blank box.

- Do not change the 'TARGET' and 'START IN' fields, they should be set to your 
'GDCommunityLauncher.exe' and 'Grim Dawn' paths respectively.

<img width="836" height="594" alt="GD_shortcut" src="https://github.com/user-attachments/assets/ff178833-3146-4a91-8697-3624dee03ccb" />

### Launch Options
- Set the launch options used by GDCommunityLauncher.exe. These are separate from your Grim Dawn
launch options, so make sure to copy them here, in case you're using some.

- Launch options follow (roughly speaking) the form
```
global_opt_1 ... global_opt_n %command% game_option_1 ... game_option_n
```
where each option is separated by a space.

- Good sources of information are [ProtonDB][https://www.protondb.com/app/219990] and the [CachyOS wiki][https://wiki.cachyos.org/configuration/gaming/]

- My current launch options for example are
```
PROTON_ENABLE_WAYLAND=1 taskset -c 1-11 mangohud game-performance %command%
```
but since these can be very system dependant, you shouldn't just copy these blindly.

### Compatability
<img width="834" height="595" alt="gdcompat" src="https://github.com/user-attachments/assets/5ceeb06b-37c0-4acb-af20-264438b154c6" />

- Select the compatability tool you want to use for GDCL.

- Updates can break these every now and then so change if necessary.

- Might be system dependant.

- Can install/manage these with ProtonUp-Qt. Might have to restart Steam to show up.

#### Some working Proton versions as of 2026-10-24:
- proton-cachyos-11.0-20261015
- GE-Proton11-7
- Proton Experimental
- Proton Stable

### Controller
- TODO

### Customization
- Set up custom artwork used on the Steam page and icons.

- Check the repo for some art for S8!

- The bootstrapper should handle most of this.

<img width="902" height="979" alt="GD_art" src="https://github.com/user-attachments/assets/118a89ad-e2df-464f-8f27-fd2e698b0032" />

## Setting Migration
- Steam games ran with Proton get (some of) their settings stored under their respective Proton
prefix paths. These are kind of like small windows filesystems living in your Steam compatdata folder.

- Adding GDCL as Non-Steam game unfortunately creates it's own proton prefix, which means that the
settings are not shared with your base GD and GDCL installations by default.

- This can be solved by manual copying or by using a script provided with the bootstrapper.

### Manual Setting Migration
- Base GD settings are located (by default at least) in
```
~/.local/share/Steam/steamapps/compatdata/219990/pfx/drive_c/users/steamuser/Documents/My Games/Grim Dawn/Settings/
```
which should contain the files "options.txt" and "keybinds.txt".

- The newly added GDCL launcher gets a (somewhat) randomly created path under
```
~/.local/share/Steam/steamapps/compatdata/<GDCL_ID>
```
where 'GDCL_ID' is the appid number generated by Steam when the game is launched using Proton.

- To make sure that the correct folder structure is created, make sure to first launch GDCL using Steam Proton
*ALL THE WAY UP TO THE GRIM DAWN MAIN MENU*. 

- This should create a new directory in "~/.local/share/Steam/steamapps/compatdata/<GDCL_ID>", where GDCL_ID is
the new appid for GDCL. This can be confusing/annoying, but the correct folder should be the 
*MOST RECENTLY MODIFIED/CREATED ONE*, so sorting can help here. 

- You can also use linux search commands like "find"/"fd" etc.

- Now navigate the new folder all the way to "./pfx/drive_c/users/steamuser/Documents/My Games/Grim Dawn/Settings/",
so that the path for your GDCL settings is
```
~/.local/share/Steam/steamapps/compatdata/<GDCL_ID>/pfx/drive_c/users/steamuser/Documents/My Games/Grim Dawn/Settings/

```
and copy the old settings here!.

- If the "Documents/My Games/" directory doesn't exist, you're either in the wrong ID folder, or haven't launched the game
into the Grim Dawn main menu through the launcher yet.

### Bootstrapper
- Follow the instructions and run a script. That's it. Unless it's broken.


## Questions/comments etc. welcome!
- Discord: scatterrr_
