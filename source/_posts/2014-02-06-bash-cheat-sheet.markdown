---
layout: post
title: "bash cheat sheet"
date: 2014-02-06 23:35:02 +0200
comments: true
categories: [linux, gentoo, bash, coding]
published: true
---

This is a collection of bash scripts solving a series of eclectic use cases which we have encountered in the past.
These instructions use linux commands and directory structures. 

<!-- more -->

## Check sequence of files for missing entries
Say you are keeping your photography files in a single directory and have them incrementally numerated.
And say you would like to check if there is any index number wherefore neither a ```.JPG``` nor a ```.NEF``` file is present.
The following script would help you find any such indices starting form ```DSC_a0000``` and up to ```DSC_a8888```:

```bash
for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" && ! -e "${i}.NEF" ]] && echo "No File with $i found"; done
```

This command can also be easily modified to suit slightly different needs - say you are only interested in indices for which ```.JPG``` files are missing:

```bash
for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" ]] && echo "No File with $i.JPG found"; done
```

Or specifically indices for which a ```.NEF``` file is present but a ```.JPG``` file is missing:

```bash
for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" && -e "${i}.NEF" ]] && echo "No File with $i.JPG found, but $i.NEF exists"; done
```

## Paste the last 100 lines from some output

Sometimes your output is too large to paste in whole. 
If the part of the output your are interested in is located close to the end, ```tail``` can be of good use.

If you want to paste from a file, run:

```bash
tail -n 100 your/file/path | wgetpaste
```

and if you want to pipe some output directly from a command (e.g. ```dmesg```) to a bastebin, run:

```bash
dmesg | tail -n 100 | wgetpaste 
```

## Append text line to text file

```bash
echo your text here, you may even add special characters: .-, \ \\ \" \; >> /your/file/path
```

Quotation marks are optional here and come in handy only if your code snippet contains many special characters (```;```, ```\```, etc.).
You can escape single characters by prefixing them with a backslash (```\```).


---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-02-06-bash-cheat-sheet.markdown)!</sup>
