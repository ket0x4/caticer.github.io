---
title: "How to use Gnu/Linux distro under android"
layout: post
date: 2019-10-22 20:40
image: /assets/images/gnuandroid.jpg
headerImage: false
tag:
- Andrid
- linux
- chroot
- proot
- gnu
star: true
category: blog
author: İbrahim
description: How to use Gnu/Linux distro under android with chroot or proot
---

## Requirements:
* A Android phone with enought storage
* GNu/Linux installed PC or VM
* Brain

## Chroot method
1. Install Chmount script to mount rootfs:
https://github.com/TheDoop/Chmount (use Magisk 4 Systemless or not ¯\_(ツ)_/¯ )

2. Download Distro RootFS:
- Debian: Don't be lazy Generate yourself (I will release rootfs soon)
- Arch: Arm64 [Download](http://os.archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz) (Arm64. you can find ARM version on the web)

3. Extract Rootfs and copy phone ("system/media/distorname" recommended), (example copy command: "adb root && adb push /debian /system/media/debian")
Never ever never Extract Rootfs under NT(windows)FS systems. beacuse NTFS does not support symlinks!

4. Open your favorite Terminal emulator and:
    su [ENTER]
    chmount /data/media/debian bash (you can repalce "bash" example: fish,vncserver etc.)
Now you're in Debian  (＾◡＾) 

## Proot (Termux)
1. Install termux:
    Google play store: https://play.google.com/store/apps/details?id=com.termux
    Fdroid(recommended): https://f-droid.org/repository/browse/?fdid=com.termux

### For Debian:
         pkg install debootstrap proot wget
           debootstrap --arch=ARCH stable stable http://ftp.debian.org/debian/ (ARCH is arm64 for aarch64, etc.)
            nano start.sh and paste this:
            --------------------------------
             #!/data/data/com.termux/files/usr/bin/sh
             proot -0 -r ~/stable -b /dev/ -b /sys/ -b /proc/ -b /data/data/com.termux/files/home /usr/bin/env -i HOME=/root TERM="xterm-256color" PS1='[root@stable \W]$ ' PATH=/bin:/usr/bin:/sbin:/usr/sbin:/bin /bin/bash --login
            ---------------------------------
            Ctrl+x save
            chmod +x start.sh

And "start.sh" to enter debian 


## Create Your own Rootfs(Debian and debian based systems):
su -c "apt install debootstrap wget"
debootstrap --arch=ARCH stable stable http://ftp.debian.org/debian/ (ARCH is arm64 for aarch64, etc.)

