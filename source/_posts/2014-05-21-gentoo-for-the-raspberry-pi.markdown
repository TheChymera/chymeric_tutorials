---
layout: post
title: "Gentoo for the Raspberry Pi"
date: 2014-05-21 00:12:11 +0200
comments: true
categories: [FOSS, Gentoo, Raspberry Pi, overview]
published: true
---

Gentoo is a Linux distribution which excels at flexibility and recommends itself for easy customization.
These qualities make it especially well-suited for scientific computing or for dedicated systems.
The [Raspberry Pi](https://en.wikipedia.org/wiki/Raspberry_pi) is one of the most popular (though not the only - see [Cubieboard](https://en.wikipedia.org/wiki/Cubieboard) as an alternate example) single-board computers to date, and is often deployed for dedicated tasks: scientific computing, home automation, etc.

Installing Gentoo on a dedicated platform makes it easy for the user to strip down his system to suit his needs precisely - e.g. in the guise of [an ultra-minimalist installation](http://dustinhatch.tumblr.com/post/38118003177/minimalist-gentoo-for-the-raspberry-pi).
Here we provide an overview of current means of installing Gentoo on your Raspberry Pi.

<!-- more -->

##Stage 3 - without cross-compiling

This is standard "quick" way of installing Gentoo on the Raspberry Pi.
It is widely recommended and features its own [Gentoo Wiki guide](http://wiki.gentoo.org/wiki/Raspberry_Pi_Quick_Install_Guide), mainly because it is consistent with common ways of deploying Gentoo, and more-or-less conveniently circumvents the need for [cross-compiling](https://en.wikipedia.org/wiki/Cross_compiler).
Sadly, this approach leads to a number of drawbacks, mainly revolving around the fact that it necessitates compiling everything with the limited resources of the Raspberry Pi.

Strengths:

* Flexible (you can tailor your system from the very start, but you have to use [the default kernel](http://wiki.gentoo.org/wiki/Raspberry_Pi_Quick_Install_Guide#Install_kernel_and_modules) to start with) 
* Widely used (you are very likely to get good support)

Weaknesses:

* Time consuming once you start working on the Pi.
* Requires copying a a number of sources via USB ([dhcpcd](https://www.gentoo.org/doc/en/handbook/handbook-x86.xml?part=4&chap=3&style=printable#doc_chap3), [connman](https://connman.net/), etc.) before you can connect to the internet, and download everything else.

##Stage 3 - with cross-compiling

This installation method allows you to unload all compilation work for the Raspberry Pi to the machine from which you are installing.
As your desktop machine will have a different architecture than the Raspberry Pi, this requires cross-compiling.
There are a number of Gentoo tools which help you set up cross-compilation toolchains - and some of them are covered specifically for our use case by unofficial blogs.

A few guides for a Raspberry Pi cross-compile installation with: [crossdev](http://dustinhatch.tumblr.com/post/38118003177/minimalist-gentoo-for-the-raspberry-pi), [static QEMU](http://www.mobileapes.com/gentoo/raspberry-pi), [QEMU](https://blog.ramses-pyramidenbau.de/?p=188).
Please note that static QEMU will not work if your system uses [systemd](https://en.wikipedia.org/wiki/Systemd) *(last checked May 2014)*; and crossdev-toolchains are known for being prone to compilation errors.

Strengths:

* Very Flexible (you can tailor your system from the very start, and [start off with a custom kernel](http://wiki.gentoo.org/wiki/Raspberry_Pi#Compiling_the_kernel)) 
* Used by some (you are likely to get some support from people who maintain the aforementioned guide)

Weaknesses:

* Time consuming until you set up cross-compilation (which, depending on your level of computer literacy, could be a very difficult process).
* Susceptible to failed compilation for certain packages.
* May need some debugging expenditure along the way

##Stage 4 

Stage 4 tarballs, are bootable fully working Gentoo systems.
Installing them is as easy as extracting the archive to a partitioned disk, and as they ship with more software than stage 3 tarballs, generally they reduce the time needed for subsequent compilation on the Raspberry Pi.
There are no official stage 4 tarballs for the Raspberry Pi; this owes to the fact that in setting up a stage 4 tarball, the developer invariably makes a few choices for the end-user.
These changes are easily undone, but this is not considered the *Gentoo way* of doing things.

We have a [detailed guide](http://tutorials.chymera.eu/blog/2014/05/23/raspberry-pi-live-gentoo-tarball/) for this simple Gentoo installation, and the stage 4 tarballs are available for download, [here](http://chymera.eu/resources/gentoo-stage4/) (one archive for the boot partition, one for the system partition).
We strive to update the tarball once every 3 months, and we *last updated May 2014*. 
There are a few other Gentoo stage 4 tarballs for the Raspberry Pi available for download, e.g. [one by intelminer](http://intelminer.com/raspberrypi/) (tarball unmaintained as of July 2012).

Strengths:

* Used by us (you are likely to get support right here in the comments section)
* Fast (you can start using your system immediately after you extract the archives)

Weaknesses:

* Less Flexible (you may have to delete software which you do not need)

##NOOBS

[NOOBS](http://www.raspberrypi.org/help/noobs-setup/) is the standard operating system install manager for the Raspberry Pi.
It provides you with a series of installation options, and while Gentoo is not supported by default, you can dd [a Gentoo image](https://rpi.pa.trickhieber.de/) to the NOOBS OS folder (```/os/Gentoo```).
Note that while the linked image is updated daily , the DD image is *unmaintained as of May 2013*. 

In principle, however, this is the same as doing a stage 4 installation (see above), with the added overhead of the NOOBS install manager.
Overall we do not recommend this.

