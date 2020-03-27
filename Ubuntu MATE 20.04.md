- Battery/power saving; check if TLP and/or Powertop are as relevant as they were
- System76 drivers for keyboard backlight?

- Wiped internal SSD and installed Ubuntu MATE 20.04
- `sudo apt update`; `sudo apt upgrade`
- `sudo apt install tlp tlp-rdw powertop`; `sudo powertop` and leave running to monitor battery. 5ish W while idle
- *The touchpad is annoyingly slow when moving finger quickly, and too fast when moving finger slowly. Look into this*
- `sudo apt install build-essential git x11proto-core-dev libx11-dev libxt-dev libxfixes-dev libxi-dev`  
- `git config --global user.email "mdmayfield@users.noreply.github.com"`; `git config --global user.name "Matt Mayfield"`
- Make and install xbanish:
  - `mkdir ~/Developer`; `cd ~/Developer`; `git clone https://github.com/mdmayfield/xbanish.git`; `cd xbanish`
  - `make` xbanish then `sudo cp xbanish /usr/local/bin/`
  - To run: `xbanish -i Shift -i Control -i mod1 -i mod4 &`
  - Add a Startup Application to execute that command minus the &
- Create ~/.config/gtk-3.0/settings.ini and add `[Settings]` (\n) `gtk-primary-button-warps-slider = false` because of the .... sadly, *sadly* misguided and confused people at GTK3
- Turn off Super key to open menu in preparation for keyboard layout shenanigans:
`gsettings set org.mate.mate-menu hot-key ''`
`gsettings set com.solus-project.brisk-menu hot-key ''`
- Install extra codecs, fonts: `sudo apt install libavcodec-extra unrar`; `sudo apt install ttf-mscorefonts-installer`; `sudo apt install gstreamer1.0-libav gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly`
- Go to Software Sources and enable Source Code repo
- Set up Time And Date control panel to keep sync with Internet time servers. First `sudo apt install ntp` then change Control Panel. (Why on Earth don't they install ntp automatically, or at least give a newbie-friendly error message? I knew what to do but a new user wouldn't.)
- Touchpad. *ugh, I do not like it compared to the XPS 15.* set up horiz + vert scrolling, two- and three-finger click/tap, turn off edge scrolling, turn off ~~*"nAtUraL"*~~ scrolling
- `sudo apt install compizconfig-settings-manager compiz-mate compiz`
- MATE Tweak: Cupertino layout, Compiz. (Windows weren't decorated after switching to Compiz... everything was messed up. Going to try importing settings, or see if a package is missing.) Also tried installing `compiz-plugins-main-default compiz-plugins-main compiz-plugins-extra` but no change.
- CompizConfig -> Preferences -> Backend: GSettings Configuration
- Download https://github.com/mdmayfield/Linux-XPS-15/blob/master/UbuntuMATE1804CompizDefaults181214.profile and import it
- `gsettings set com.solus-project.brisk-menu window-type 'classic'` to disable fullscreen Brisk Menu
- Plank theme: Matte
- Configure HUD: `gsettings set org.mate.hud shortcut '<Super>space'` then enable in MATE Tweak
# TODO: date in menubar
- `sudo apt install papirus-icon-theme`
- In Appearance, choose BlueSubmarine then Customize to Icons: Papirus-dark, Pointer: MATE (Black)
