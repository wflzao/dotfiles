``` bash
# nvidia driver
sudo pacman -S nvidia nvidia-settings nvidia-utils lib32-nvidia-utils lib32-opencl-nvidia opencl-nvidia libvdpau libxnvctrl vulkan-icd-loader lib32-vulkan-icd-loader
sudo pacman -Syu && reboot

sudo pacman -S vim

# nvidia settings
sudo nvidia-settings
mkdir ~/.config/autostart
sudo touch /etc/xdg/autostart/nvidia-settings.desktop
sudo vim /etc/xdg/autostart/nvidia-settings.desktop
---
[Desktop Entry]
Name=nVidia2
Comment=Load nVidia Configuration
Icon=system-run
Exec=nvidia-settings --config=/etc/.nvidia-settings-rc --load-config-only
Terminal=false
Type=Application
OnlyShowIn=GNOME;XFCE;
X-GNOME-Autostart-enabled=true
---
sudo cp /etc/xdg/autostart/nvidia-settings.desktop ~/.config/autostart/nvidia-settings.desktop
sudo touch /etc/profile.d/autostart.sh
sudo vim /etc/profile.d/autostart.sh
---
#!/bin/bash
VAL=850
if [[ $(nvidia-settings -q "DigitalVibrance" | grep "Attribute.*$VAL\.") ]]
then
    nvidia-settings -a "DigitalVibrance=0" > /dev/null
else 
    nvidia-settings -a "DigitalVibrance=$VAL" > /dev/null
fi
---

# pc speaker
sudo touch /etc/modprobe.d/nobeep.conf
sudo vim /etc/modprobe.d/nobeep.conf
---
blacklist pcspkr
---
sudo rmmod pcspkr

# mouse accel
sudo touch /etc/X11/xorg.conf.d/50-mouse-acceleration.conf
sudo vim /etc/X11/xorg.conf.d/50-mouse-acceleration.conf
---
Section "InputClass"
	Identifier "My Mouse"
	Driver "libinput"
	MatchIsPointer "yes"
	Option "AccelProfile" "flat"
	Option "AccelSpeed" "0"
EndSection
---

# apps
yay -S picom-ibhagwan-git
sudo pacman -S lightdm-webkit2-greeter
sudo pacman -S zathura
sudo pacman -S zsh
sudo pacman -S kitty
sudo pacman -S vifm
sudo pacman -S feh
sudo pacman -S flameshot
sudo pacman -S mpv
sudo pacman -S code
sudo pacman -S bitwarden


# dotfiles
https://github.com/Manas140/dotfiles/tree/02a1c0e4f66fba231fc84da73ef968a672e11d0c

# keybinds
vim ~/.config/sxhkd/sxhkdrc

# lightdm
sudo pacman -R eos-lightdm-slick-theme
sudo pacman -R lightdm-slick-greeter
yay -Syu lightdm-webkit2-theme-glorious
sudo cp ~/Pictures/Wallpapers/* /usr/share/backgrounds/
sudo vim /etc/lightdm/lightdm.conf
sudo vim /etc/lightdm/lightdm-webkit2-greeter.conf

# polybar
# https://github.com/0jdxt/polybar-mpris
cd ~/Downloads && git clone https://github.com/0jdxt/polybar-mpris.git && cd polybar-mpris
mv get_status.sh ~/.config/polybar/scripts
mv scroll_status.sh ~/.config/polybar/scripts
vim ~/.config/polybar/config.ini
vim ~/.config/polybar/modules.ini
vim ~/.config/polybar/scripts/get_status.sh
vim ~/.config/polybar/scripts/scroll_status.sh

#rofi
vim ~/.config/rofi/config.rasi

#cursor
https://github.com/ful1e5/apple_cursor/releases/download/v2.0.0/macOS-BigSur.tar.gz
cd ~/Downloads
unzip macOS-BigSur.tar.gz
sudo rm /usr/share/icons/default/*
sudo cp ~/Downloads/macOS-BigSur/* /usr/share/icons/default/
sudo mkdir /usr/share/icons/default/cursors/
sudo cp ~/Downloads/macOS-BigSur/cursors/* /usr/share/icons/default/cursors
vim ~/.config/gtk-3.0/settings.ini
```
