---
layout: post
title: "Miscellaneous Cheat Sheet"
date: 2014-02-03 21:20:58 +0100
comments: true
categories: [linux, coding]
published: true
---

This is a collection of workflows, commands, or bash scripts solving a series of common use cases.
These instructions use linux commands and directory structures. 

<!-- more -->

## Batch Rotate Images
There are a number of ways to do this.
One would be via the [GIMP](https://en.wikipedia.org/wiki/GIMP) [script-fu](http://docs.gimp.org/2.8/en/gimp-concepts-script-fu.html), which is awfully complicated to use (as an example of how you would batch rotate files with script-fu, you can see [this thread on StackOverflow](http://stackoverflow.com/questions/23554843/batch-rotate-files-with-gimp)).

If your image happens to be in the JPEG file format, however, you can easily rotate it with a library function called ```jpegtran```.
This function ships with the ```libjpeg-turbo``` package, which you already have installed if your system is capable of viewing JPEG format files.
To use this function simply run:

{% codeblock replace .JPG with your respective extension formatting lang:bash %}
find *.JPG -exec jpegtran -rotate 180 -outfile "{}" "{}" \;
{% endcodeblock %}

An other option is via [ImageMagick](https://en.wikipedia.org/wiki/Imagemagick), which is easy, but which would require you to download software you may otherwise not need.
The respective command would be:

{% codeblock replace .png with your respective extension as necessary lang:bash %}
mogrify -rotate 180 *.png
{% endcodeblock %}

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

## Change file permissions recursively
This command grants all users read permissions to the folder, subfolders, and all files therein - in addition to whatever permissions are already set.
Note that ```chmod``` may need to be run as root.

```bash
chmod -R a+r your/directory/path/
```
Or better yet, use octal to accurately define what permissions the owner, the group, and everyone else has:

```bash
chmod -R 775 your/directory/path/
```

##Remove .orig files from (Git) folder
Occasionally Git merges may leave you with residual ```.orig``` files which clutter your repository.
[This question](http://stackoverflow.com/questions/12366150/how-to-delete-orig-files-after-merge-from-git-repository/20895666#20895666) on StackOverflow exemplifies how the issue may arise. 
To solve the issue run the following command from your repository root.

```bash
find . -name '*.orig' -delete
```


## Text lookup in folder
The ```grep``` command with the ```-r``` option lets you find the occurrences of a string inside all files within a folder and all its subfolders.

```bash
grep -r "yourstring" folder1/ folder2/
```

## Nested Markdown/reST Syntax
Use the following too get a bold (or italic, etc.) link via markdown:

```bash
**[link name](http://address.you.want.to.point.to)**
```
In reStructured Text (reST) this feature is on the *to do* list, but not yet available. 

## OpenRC: See and edit runlevels
This assumes you are using [OpenRC](http://en.wikipedia.org/wiki/OpenRC) and will not work on systems set up with [systemd](http://en.wikipedia.org/wiki/Systemd). 
Note that ```rc-update``` may need to be run as root.

```bash
rc-update show/add/del
```

## Convert .flac to .mp3
Here you will need [ffmpeg](http://en.wikipedia.org/wiki/FFmpeg) - a command line program which ships with the FFmpeg libraries,
and comes together with media playback dependencies on many linux distros 
(meaning that you probably have it installed already).

```bash
ffmpeg -i your/song/path.flac your/song/path.mp3
```

## Rsync sub-directory
Run from the directory containing ```DIR```. ```DIR``` is the directory to be synced and created if needed on the remote host.
**Do not** use trailing slashes after the ```DIR``` directory name or all the contents will get dumped directly into ```your/remote/path/```:

```bash
rsync --filter '- */.*' -e "/usr/bin/ssh" --bwlimit=2000 -av DIR user@server.domain.com:your/remote/path/
```

## Mass copy files without overwriting
Sometimes you want to copy all files in one (large) directory to another - which already contains some of these files.
Usually using a file manager of ```cp``` (whithout arguments) for such a task can prove quite tedious.
Here is an variant using ```rsync``` (recommended):

```bash
rsync -tr /copy/from/here/* /copy/to/here/
```
And alternative using the ```--no-clobber``` argument for ```cp```:

```bash
cp -n /copy/from/here/* /copy/to/here/
```

## Download flash videos under Linux

#### 1) Youtube-dl

[Youtube-dl](http://rg3.github.io/youtube-dl/index.html) is a FOSS python script which allows you to download flash videos from not only YouTube, but [over 150 websites](http://rg3.github.io/youtube-dl/supportedsites.html).
You can download it directly [from the official website](http://rg3.github.io/youtube-dl/download.html) or through your package manager of choice (it is provided by portage and many others).

In case you foresee running into DRM restrictions, you may also want to get [RTMPDump](http://rtmpdump.mplayerhq.hu/).
Youtube-dl calls RTMPDump automatically if it encounters Adobe's proprietary RTMP protocol and the software is installed. 

#### 2) Chrome and wget

* Open your Chrome cache page (at [chrome://cache/](chrome://cache/)).
* Open the page containing your video in a new tab.
* Start playing the video.
* Return to your chrome cache page and refresh it, your topmost link *should* point to the video
* Copy the link (in plaintext, *or* copy the link destination and remove the ```chrome://...``` part at its start)
* Run this from your terminal:

```bash
wget "your_URL" video
```

## Edit apps launched at startup in GNOME 3.*

```bash
gnome-session-properties
```

##Make Git cache passwords for 10 hours

```bash
git config --global credential.helper cache
git config --global credential.helper "cache --timeout=36000"
```

## Change owner of a directory recursively

Note that ```chown``` may need to be run as root.

```bash
chown -R user your/directory/path/
```

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-02-03-cheat-sheet.markdown)!</sup>
