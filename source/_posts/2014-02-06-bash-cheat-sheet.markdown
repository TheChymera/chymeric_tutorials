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
And say you would like to check if there is any number wherefore neither a ```.JPG``` nor a ```.NEF``` file is present.
The following script would help you find any such files starting form ```DSC_a0000``` to ```DSC_a8888```:
{% codeblock  lang:bash %}
$ for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" && ! -e "${i}.NEF" ]] && echo "No File with $i found"; done
{% endcodeblock %}

This command can also be easily modified to suit slightly different needs - say you are interested in indices for which ```.JPG`` files are missing:
{% codeblock  lang:bash %}
$ for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" ]] && echo "No File with $i.JPG found"; done
{% endcodeblock %}

Or specifically indices for which a ```.NEF``` fileis present but a ```.JPG``` file is missing:
{% codeblock  lang:bash %}
$ for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" && -e "${i}.NEF" ]] && echo "No File with $i.JPG found, but $i.NEF exists"; done
{% endcodeblock %}

## Paste the last 100 lines from some output

Sometimes your output is too large to paste in whole - 
if the part of the output your are interested in is located close to the end, ```tail``` can be of good use.

If you are pasting from a file, run:
{% codeblock  lang:console %}
$ tail -n 100 your/file/path | wgetpaste
{% endcodeblock %}

and if you are piping some output directly from a command (e.g. ```dmesg```) to a bastebin, run:
{% codeblock  lang:console %}
dmesg | tail -n 100 | wgetpaste 
{% endcodeblock %}

## Append text line to text file
{% codeblock  lang:bash %}
$ echo your text here, you may even add special characters: .-, \ \\ \" \; >> /your/file/path
{% endcodeblock %}