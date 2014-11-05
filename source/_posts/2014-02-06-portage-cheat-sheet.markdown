---
layout: post
title: "Portage Cheat Sheet"
date: 2014-02-06 23:27:48 +0200
author: Horea Christian
googleplus_user: 117525803180879614771
comments: true
categories: [linux, gentoo, portage, coding]
published: true
---

This is a small sample of commands dealing with a series of simple use cases involving [Portage](http://en.wikipedia.org/wiki/Portage_(software)).
For all the code examples please note that ```emerge``` needs to be run as root.
Other commands such as ```equery``` can be run as user.
The Gentoo Wiki hosts a longer (though different) Portage/[Gentoo](http://en.wikipedia.org/wiki/Gentoo_Linux) cheat sheet [on this page](https://wiki.gentoo.org/wiki/Gentoo_Cheat_Sheet).

<!-- more -->

## Re-emerge all live ebuilds
The hackish way (re-emerges all packages versioned 9999).

```bash
emerge -av `eix -Jc | grep 9999 | cut -d" " -f2 | tr "\n" " "`
```
The smart way (re-emerges live packages only if the upstream checksum has changed):

```bash
emerge @smart-live-rebuild
```

## Emerge stuff using only one core
This is useful if the package is prone to breakage when using parallel processing (some things can become required before they are compiled).

```bash
MAKEOPTS=-j1 emerge -vaDNu chromium 
```

## Pass Portage options to scripts
Some scripts (like ```revdep-rebuild``` or ```perl-cleaner```) check the portage tree and the packages on your machine, and then pipe an ```emerge``` command for Portage.
Mostly they ```emerge -vD1 *```, you can usually add more arguments via ```--```.
Like so:

```bash
perl-cleaner -- -vDNu1
```

Additionally, this also works if the script takes arguments of its own:

```bash
perl-cleaner --all -- -vDNu1
```

## What package pulls in foo?

```bash
equery b foo
```

## See all packages in world 

```bash
cat /var/lib/portage/world 
```

## Find out what package said file belongs to

```bash
qfile /path/to/file
```

