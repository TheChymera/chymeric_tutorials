---
layout: post
title: "Raspberry Pi Stage 4 Gentoo Tarball"
date: 2014-05-23 02:19:37 +0200
author: <a rel="author" href="https://plus.google.com/117525803180879614771/about">Horea Christian</a>
comments: true
categories: [FOSS, Gentoo, Raspberry Pi, download]
published: true
---

[Tarballs](https://en.wikipedia.org/wiki/Tarball) (a term for ```.tar``` archives) are a common medium for installing the [Gentoo Linux](https://en.wikipedia.org/wiki/Gentoo_linux) operating system.
The standard Gentoo installation starts with a non-bootable "stage 3" tarball, which includes only very limited software.
As discussed in a [previous article](http://chymeric.eu/blog/2014/05/21/gentoo-for-the-raspberry-pi/), on the Raspberry Pi - and other embedded systems - it is in certain respects better to start off with a bootable (and wifi-capable) tarball.

For these purposes we are publishing a stage 4 tarball with all the basic software you need on the Raspberry Pi - including the **sys-kernel/linux-firmware** package for broad wifi-device support and a Git repository for customizing and deploying the newest Raspberry Pi kernel sources from [upstream](git://github.com/raspberrypi/linux.git).
Though the archives total under 1 GB in size, we recommend you use at least an 8 GB SD card for use with your Raspberry Pi.

<!-- more -->

##Our Tarball Structure

The structure is fairly straightforward, our tarball distribution consists of 2 archives, which can be downloaded from [this directory](http://chymera.eu/resources/gentoo-stage4/).
The ```boot.tar.bz2``` archive contains files needed for the boot partition (namely the ```/boot``` directory), whereas the ```system.tar.bz2``` archive contains the files for the system partition (the rest of the root directory).

* [Boot tarball direct download](http://chymera.eu/resources/gentoo-stage4/boot.tar.bz2)
* [System tarball direct download](http://chymera.eu/resources/gentoo-stage4/system.tar.bz2)

##Partitioning Your Drive

It is important to partition the drive so that the tarball system will recognise everything properly.
For this you will need:

* **First partition**: formatted as *fat32*, we recommend 100 MB (this will be your ```/boot``` partition).
* **Second partition**: formatted as *linux swap*, we recommend 1 GB or more (this will be your swap partition)
* **Third partition**: formatted as *ext4*, as large as the remainder of your disk (this will be your system partition).

You may partition the drive with [gparted](http://en.wikipedia.org/wiki/Gparted), [parted](http://en.wikipedia.org/wiki/Parted), or whatever else you are most comfortable with.

##Extracting the Tarballs

To extract the tarballs simply mount your first and third partitions (boot and system respectively) on a functioning system; navigate to them and extract the archives with the ```tar -xvjpf``` command.

As an example:

```bash
cd /your/mount/point/for/boot
tar -xvjpf /your/download/directory/boot.tar.bz2
cd /your/mount/point/for/system
tar -xvjpf /your/download/directory/system.tar.bz2
```

We recommend you perform the above operations as root.
Unmount, plug the SD card into your Raspberry Pi, and you are good to go!

##Managing your Users

As per our minimal tarball, your root user is passwordless.
You are well advised to set a password immediately after your first log in (you can log in by simply entering the user *root* and pressing enter).

To set your root password, type:

```bash
passwd
```

You should also add a new user for yourself and add a password for that user as well.
To do this type:

```bash
useradd youruser
passwd youruser
```

##Connecting with Connman

Our tarball comes with a basic Connman installation, so that you can easily access your network whilst keeping system resource use at a minimum.
For a more thorough explanation of how to use Connman we kindly refer you to [the connman page on the Arch wiki](https://wiki.archlinux.org/index.php/Connman#Using_the_command_line_client).

We have added Connman to your default runlevel, and after you connect to your network once, everything should work automatically the next time you boot up - presuming the network is still reachable.

##Updating your Kernel

We have set up a repository which you can use to download the newest kernel sources.
The repository is located under ```/usr/src/linux-9999-rpi``` and pulls the files from ```git://github.com/raspberrypi/linux.git```.

You can control which kernel your ```/usr/src/linux``` symlink points to via [eselect](http://wiki.gentoo.org/wiki/Project:Eselect), though you should bear in mind that navigating to the Git repository via the symlink directory prevents you from using Git.

To update your kernel, run:

```bash
cd /usr/src/linux-9999-rpi
git pull origin master
make ARCH=arm bcmrpi_defconfig
make oldconfig
make && make modules_install
mount /boot
cp arch/arm/boot/zImage /boot/kernel-rpi-<version number>
```

To instruct your Rapsberry Pi boot loader to use the new kernel edit your ```/boot/config.txt``` file.
The first entry should read:

```bash
#kernel
kernel=kernel-rpi-<version number>
```

##Shipped Packages
For ease of overview - here is a paste of our ```@world``` file, which specifies all the packages we have explicitly installed.

```bash
app-portage/eix
app-text/wgetpaste
dev-vcs/git
net-misc/connman
net-misc/ntp
sys-apps/ifplugd
sys-kernel/linux-firmware
sys-kernel/raspberrypi-sources
```

##Increased Performance

To speed up your Raspberry, we have enabled a few optimizations (medium overclocking and reduced GPU memory) in the ```/boot/config.txt``` file.
For more information on these or other potential optimizations please consult the [relevant section](http://wiki.gentoo.org/wiki/Raspberry_Pi_Quick_Install_Guide#Overclocking) on the Gentoo wiki.

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-05-23-raspberry-pi-live-gentoo-tarball.markdown)!</sup>
