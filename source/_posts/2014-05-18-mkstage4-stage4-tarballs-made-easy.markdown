---
layout: post
title: "mkstage4 - Stage 4 Tarballs Made Easy"
date: 2014-05-18 05:53:23 +0200
author: Horea Christian
gooleplus_user: 117525803180879614771
comments: true
categories: [FOSS, Gentoo, Raspberry Pi, coding, ebuild]
published: true
---

Stage 4 tarballs are bootable, fully working, self-sufficient [Gentoo Linux](https://en.wikipedia.org/wiki/Gentoo_linux) distributions.
They include a complete Gento environment, which you can directly boot up and use.

Stage 4 tarballs are very well suited for system backups or use cases where chrooting and emerging your basic system requirements can become very tedious.
Situations in which stage 3 installation is difficult include:

* Installing Gentoo on machines with limited resources for compilation (e.g. many [ARM family](https://en.wikipedia.org/wiki/ARM_architecture) platforms)
* Installing Gentoo for machines which do not support standard live CD/USB distributions

<!-- more -->

##Background

Making a stage 4 tarball - while in principle as simple as [```tar```](https://en.wikipedia.org/wiki/Tar_(computing))-ing a Gentoo system - requires you to remember a long list of directories to exclude and a number of ```tar``` options.
The Gentoo Wiki used to have a guide for this process, which has since been removed from the official webpage (but is still archived [on a mirror](http://gentoo-en.vfose.ru/wiki/Custom_Stage4)).
Especially for users who are looking towards stage 4 tarballs for backup solutions, this process is excruciatingly tedious and repetitive, and begs for slips of the pen - so to say.

Not surprisingly, a bash script to keep all the details in place has been around since at least 2005: ["mkstage4"](http://blinkeye.ch/dokuwiki/doku.php/projects/mkstage4).
This script became unmaintained in 2009, but was later [re-edited](https://github.com/gregf/bin/blob/master/mkstage4) - though this edition also became unmaintained by 2012.

Here we present a new, maintained version of **mkstage4**, with broader functionality, and a more flexible command line interface.

##Usage

The script is hosted [on GitHub](https://github.com/TheChymera/mkstage4), and provides a basic usage guide on its [README page](https://github.com/TheChymera/mkstage4/blob/master/README.md).
It can be called *as root* from the directory it is located in:

```bash
cd /your/mkstage4/directory
chmod +x mkstage4.sh
./mkstage4.sh -s archive_name
```

This creates a stage 4 tarball of the current system - this being specified by the ```-s``` (sytem) flag - under the name name ```archive_name.tar.bz2```.
If you would like to use mkstage4 to create a tarball of an other mounted system you can point it to the respective mount point with the ```-t``` (target) flag:

```bash
./mkstage4.sh -t /your/mount/point archive_name
```

The folders which are excluded by the script can be seen in the ```EXCLUDES``` variable in the [script file](https://github.com/TheChymera/mkstage4/blob/master/mkstage4.sh).
Note that the exclude list is adaptive: specifying the name of the archive itself when the script is used for a current-system backup, or optionally specifying other folders (e.g. the ```/boot``` folder with the ```-b``` flag).

##Deploying Stage 4 Tarballs

Using the results of mkstage4 is equally simple.
Broadly speaking you only need to partition and mount your disk, and extract the archives.

Partitioning is simple and can be done via a graphical interface with [GParted](https://en.wikipedia.org/wiki/Gparted); but if you have never done this before you might want to consult the [respective in-depth walk-through](https://www.gentoo.org/doc/en/handbook/handbook-x86.xml?part=1&chap=4) from the Gentoo handbook.
It is important to note that the disks should be partitioned similarly to those of the system from which you created the stage 4 tarballs.

The archives should be extracted with ```tar xvjpf```.
Assuming that you have all of your system in one partition, extraction is as simple as:

```bash
cp archive_name.tar.bz2 /mount/point/for/your/partition/
cd /mount/point/for/your/partition
tar xvjpf archive_name.tar.bz2
```

If you use the more sensible approach and keep your ```/boot/``` partition separate you would be dealing with two archives, so additionally to the former, you would run:

```bash
cp boot_archive_name.tar.bz2 /mount/point/for/your/partition/boot/
cd /mount/point/for/your/partition/boot
tar xvjpf boot_archive_name.tar.bz2
```

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-05-18-mkstage4-stage4-tarballs-made-easy.markdown)!</sup>
