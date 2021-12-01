---
title: Cara install DWM di Ubuntu 🐱‍👤
date: 2021-11-30
author: Anonymouse
summary: Cara install DWM di Ubuntu
tags:
  - Tips



---

# Cara install DWM di Ubuntu

```bash
sudo apt install build-essential libx11-dev libxinerama-dev sharutils libxft-dev
```

```bash
cd .config/
```

```bash
mkdir suckless
```

```bash
cd suckless
```

```bash
sudo apt install git wget vim curl
```

```bash
git clone https:/git.suckless.org/dwm
```

```bash
git clone https:/git.suckless.org/st
```

```bash
git clone https:/git.suckless.org/dmenu
```

```bash
cd dwm
```

```bash
make
```

```bash
sudo make install
```

```bash
sudo apt install xinit
```

# Tips 2

```bash
sudo apt install xorg stterm suckless-tools build-essential libx11-dev libxinerama-dev libxft-dev git vim curl wget libwebkit2gtk-4.0-dev
```

```bash
reboot
```

```bash
sudo apt remove gdm3
```

```
reboot
```

```
git clone https://git.suckless.org/dwm
```

```
cd dwm
sudo make clean install
```

```
vim .xinitrc

exec dwm
```

```
vim .bash_profile

startx
```

```
reboot
```

```bash
sudo apt install i3lock imagemagick feh fonts-font-awesome
```



#### Setting Backgroud

```bash
feh --bg-scale wallpaper.jpg
```

#### Resolution Screen

```bash
xrandr -s 1440x900
```



## VboxInstallGuest

```
sudo apt update

sudo apt install build-essential dkms linux-headers-$(uname -r)
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3xegt1sg6ensnu3vc1d0.jpg)

```
sudo mkdir -p /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
```

```
cd /mnt/cdrom
sudo sh ./VBoxLinuxAdditions.run --nox11
```

```
output

Verifying archive integrity... All good.
Uncompressing VirtualBox 5.2.32 Guest Additions for Linux........
...
VirtualBox Guest Additions: Starting.
```

```
sudo shutdown -r now
```

```
lsmod | grep vboxguest
```

```
output

lsmod | grep vboxguest
```



[^referensi]: [DWM Install on Minimal Version of Ubuntu Linux - No Bloat! Dynamic Window Manager - YouTube](https://www.youtube.com/watch?v=lipHPQL4nmQ)

[DWM initial setup and config. Icons, Bar Scripts, Keybindings, and Theming. - YouTube](https://www.youtube.com/watch?v=zaRzOEoyR4s)

