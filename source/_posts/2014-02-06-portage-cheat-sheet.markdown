---
layout: post
title: "Portage Cheat Sheet"
date: 2014-02-06 23:27:48 +0200
comments: true
categories: [linux, gentoo, portage, coding]
published: true
---

This is a small sample of commands dealing with a series of simple use cases involving [Portage](http://en.wikipedia.org/wiki/Portage_(software)).

<!-- more -->

## Re-emerge all live ebuilds
The hackish way (re-emerges all packages versioned 9999):

```bash
# emerge -av `eix -Jc | grep 9999 | cut -d" " -f2 | tr "\n" " "`
```
The smart way (re-emerges live packages only if the upstream checksum has changed):

```bash
# emerge @smart-live-rebuild
```

## Emerge stuff using only one core
This is useful if the package is prone to breakage when using parallel processing (some things can become required before they are compiled).

```bash
MAKEOPTS=-j1 emerge -vaDNu chromium 
```

## What package pulls in foo?

```bash
$ equery b foo
```

## See all packages in world 

```bash
$ cat /var/lib/portage/world 
```

## Find out what package said file belongs to

```bash
qfile /path/to/file
```

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-02-06-portage-cheat-sheet.markdown)!</sup>
