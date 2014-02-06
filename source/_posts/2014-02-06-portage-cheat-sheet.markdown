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
{% codeblock  lang:console %}
# emerge -av `eix -Jc | grep 9999 | cut -d" " -f2 | tr "\n" " "`
{% endcodeblock %}
The smart way (re-emerges live packages only if the upstream checksum has changed):
{% codeblock  lang:console %}
# emerge @smart-live-rebuild
{% endcodeblock %}

## Emerge stuff using only one core
This is useful if the package is prone to breakage when using parallel processing (some things can become required before they are compiled).
{% codeblock  lang:console %}
MAKEOPTS=-j1 emerge -vaDNu chromium 
{% endcodeblock %}

## What package pulls in foo?
{% codeblock  lang:console %}
$ equery b foo
{% endcodeblock %}

## See all packages in world 
{% codeblock  lang:console %}
$ cat /var/lib/portage/world 
{% endcodeblock %}

## Find out what package said file belongs to
{% codeblock  lang:console %}
qfile /path/to/file
{% endcodeblock %}
