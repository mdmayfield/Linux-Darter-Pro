- Battery/power saving; check if TLP and/or Powertop are as relevant as they were
- ~~System76 drivers for keyboard backlight?~~ Not needed it seems
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
- In Appearance, choose BlueSubmarine then Customize to Icons: Papirus, Pointer: MATE (Black)
- ~~**Experimental:** Instead of custom keyboard layout, using Options in Keyboard Preferences -> Layouts. **Alt/Win Behavior** Ctrl is mapped to Alt; Alt is mapped to Win / **Miscellaneous Compatibility Options** Numeric keypad always enters digits (as in macOS) / **Position of Compose key** Menu~~
- ~~Arrows and Delete are unaffected......~~
- Keyboard map: download "custom-darp", save as `~/.config/custom-darp.xkbmap`
- put in `~/.xsessionrc`: `(sleep 4 ; xkbcomp $HOME/.config/custom-darp.xkbmap $DISPLAY) &` (not sure why the sleep is necessary these days, but noticed it a few weeks ago on 20.04)
- `gsettings set com.solus-project.brisk-menu hot-key '<Control>space'`
- `sudo apt install autokey-gtk`; run Autokey, quit. Swap in `mdmayfield/Linux-XPS-15/autokey/data` for `~/.config/autokey/data`. Manually add AutoKey as `autokey` to Startup Items.
# TODO: figure out script error on system.exec_command
- Replace ~/.mozilla/firefox folder with backup from previous installation (`magic-wormhole` is good for this)
- Add to ~/.profile: `# enable smooth scrolling in Firefox  \n  export MOZ_USE_XINPUT2=1`
- Turn off Bluetooth at system startup: create `/etc/rc.local` and make it executable - systemd will run it. This is the same as doing "Turn Bluetooth Off" and it can be turned back on by the applet:
  ```
  #!/bin/bash
  rfkill block bluetooth
  exit 0
  ```
- Set up libinput-gestures:
  - `sudo gpasswd -a $USER input` to add self to input group
  - `sudo apt install xdotool wmctrl`
  - `sudo apt install libinput-tools`.
  - `cd ~/Developer`; `git clone https://github.com/bulletmark/libinput-gestures.git`; `cd libinput-gestures`; `sudo make install`
  - in `~/.config/libinput-gestures.conf`:
  ```
  gesture swipe up	xdotool key super+alt+Up
  gesture swipe down	xdotool key super+alt+Down
  gesture swipe left	xdotool key super+alt+Left
  gesture swipe right	xdotool key super+alt+Right
  swipe_threshold 300
  ```
  - `libinput-gestures-setup autostart` to automatically run at login; `libinput-gestures-setup start` to run now
  - Remove Plank icon from Plank dock: `gsettings set net.launchpad.plank.dock.settings:/net/launchpad/plank/docks/dock- 1/ show-dock-item false`
- Remove Indicator-Applet-Complete from dock, ???

- Follow https://gitlab.com/francois.kneib/clevo-N151ZU-fan-controller
