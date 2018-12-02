# My Linux Development Environment  

Setup and software of my personal laptop, powered by Ubuntu Linux 18.04.  

## First Update

This is the first thing you should do after fresh installing Ubuntu.

```bash
$ sudo apt update && sudo apt upgrade
```

## Enable Canonical Partners repo

```bash
$ sudo sed -i 's/# deb http/deb http/g' /etc/apt/sources.list
$ sudo apt update
```

## Install Media Codecs

```bash
$ sudo apt install ubuntu-restricted-extras
```

## Enable ‘Minimize on Click’ for the Ubuntu Dock

```bash
$ gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
```

## Flatpak  

Flatpak is a universal packaging system from Fedora. Like Snap, you can install Flatpak packaged applications in various Linux distributions that support Flatpak.  
Snap is cool, but I had a lot of trouble usuing it. So, I tried to use flatpak and worked very well.  
I loved it.

```bash
$ sudo add-apt-repository ppa:alexlarsson/flatpak
$ sudo apt install flatpak
$ sudo apt install gnome-software-plugin-flatpak
$ flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```  

And restart the system

```bash
$ sudo shutdown -r now
```  




