# Linux-Tools
Everyday working tools I use to setup my Linux environment.

## Grub Bootloader
View the `grub` file to see the resolution size and color.

## Gnome Settings
View gnome.md

## Emacs
View README.md in emacs folder

## Bash Settings
$ cp bashrc ~/.bashrc

Adjust the spotify alias command to proper scaling factor

## Installing Spotify

1. Add the Spotify repository signing keys to be able to verify downloaded packages

$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys BBEBDCB318AD50EC6865090613B00F1FD2C19886 0DF731E45CE24F27EEEB1450EFDC8610341D9410

2. Add the Spotify repository

$ echo deb http://repository.spotify.com stable non-free | sudo tee /etc/apt/sources.list.d/spotify.list

3. Update list of available packages

$ sudo apt-get update

4. Install Spotify

$ sudo apt-get install spotify-client

## Remove minimize, maximize, and close buttons from Windows applications
$ gsettings set org.gnome.desktop.wm.preferences button-layout :

To undo:
$ gsettings reset org.gnome.desktop.wm.preferences button-layout
