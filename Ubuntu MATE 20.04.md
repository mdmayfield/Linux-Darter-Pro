- Battery/power saving; check if TLP and/or Powertop are as relevant as they were
- ~~System76 drivers for keyboard backlight?~~ Not needed it seems
- Wiped internal SSD and installed Ubuntu MATE 20.04
- `sudo apt update`; `sudo apt upgrade`
- `sudo apt install tlp tlp-rdw powertop`; `sudo powertop` and leave running to monitor battery. 5ish W while idle
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
- `sudo apt install papirus-icon-theme`
- In Appearance, choose BlueSubmarine then Customize to Icons: Papirus, Pointer: MATE (Black)
- ~~**Experimental:** Instead of custom keyboard layout, using Options in Keyboard Preferences -> Layouts. **Alt/Win Behavior** Ctrl is mapped to Alt; Alt is mapped to Win / **Miscellaneous Compatibility Options** Numeric keypad always enters digits (as in macOS) / **Position of Compose key** Menu~~
- ~~Arrows and Delete are unaffected......~~
- Keyboard map: download "custom-darp", save as `~/.config/custom-darp.xkbmap`
- put in `~/.xsessionrc`: `(sleep 4 ; xkbcomp $HOME/.config/custom-darp.xkbmap $DISPLAY; xset -r 105) &` (not sure why the sleep is necessary these days, but noticed it a few weeks ago on 20.04. xset -r 105 turns off autorepeat for right Control which we're using as a Compose/Multi key. For some reason repeat=false in the xkb file doesn't work.)
- `gsettings set com.solus-project.brisk-menu hot-key '<Control>space'`
- `sudo apt install autokey-gtk`; run Autokey, quit. Swap in `mdmayfield/Linux-XPS-15/autokey/data` for `~/.config/autokey/data`. Manually add AutoKey as `autokey` to Startup Items.
- Replace ~/.mozilla/firefox folder with backup from previous installation (`magic-wormhole` is good for this)
- Add to ~/.profile: `# enable smooth scrolling in Firefox  \n  export MOZ_USE_XINPUT2=1`
- ~~Turn off Bluetooth at system startup: create `/etc/rc.local` and make it executable - systemd will run it. This is the same as doing "Turn Bluetooth Off" and it can be turned back on by the applet:~~ *This doesn't seem to work*
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
  gesture swipe up        3 xdotool key super+alt+Up
  gesture swipe down      3 xdotool key super+alt+Down
  gesture swipe left      3 xdotool key super+alt+Left
  gesture swipe right     3 xdotool key super+alt+Right

  gesture swipe up        4 xdotool key shift+super+alt+Up
  gesture swipe down      4 xdotool key shift+super+alt+Down
  gesture swipe left      4 xdotool key shift+super+alt+Left
  gesture swipe right     4 xdotool key shift+super+alt+Right

  #gesture pinch in        4 xdotool key super+s
  #gesture pinch out       4 xdotool key super+s

  swipe_threshold 200
  ```
  - Doesn't seem to work with > 2-finger pinches?
  - `libinput-gestures-setup autostart` to automatically run at login; `libinput-gestures-setup start` to run now
  - Remove Plank icon from Plank dock: `gsettings set net.launchpad.plank.dock.settings:/net/launchpad/plank/docks/dock- 1/ show-dock-item false`
- Power Management -> brightness controls
- Install custom mate-indicator-applet with no hotkeys from source.
  - `cd ~/Developer`; `git clone https://github.com/mdmayfield/mate-indicator-applet.git`; `cd mate-indicator-applet`
  - `sudo apt build-dep mate-indicator-applet`; `./autogen.sh --with-ubuntu-indicators`; `make`; `sudo make install`
  - Log out/in or restart
- Use indicator-applet and separate clock to get desired format

# Todo 

- Follow https://gitlab.com/francois.kneib/clevo-N151ZU-fan-controller
- *The touchpad is annoyingly slow when moving finger quickly, and too fast when moving finger slowly. Look into this*
- In AutoKey, figure out script error on system.exec_command
- Find a reliable way to disable Bluetooth at startup while allowing it to be enabled from the menu
- Figure out the top-pixel-row unreliable thing (There was a bug in X with negative fractional pixel values, or something? Was investigating this on the desktop a while ago. I believe I worked around it there by telling the panel app to fall back to an earlier Xinput or something)
