---
layout: post
title: "stack bracketed photos"
date: 2014-09-23 17:58:00 +0200
author: Horea Christian
googleplus_user: 117525803180879614771
comments: true
categories: [photography, coding, scripting, image-processing] 
published: true
---

[Bracketed](http://en.wikipedia.org/wiki/Bracketing) pictures are commonly taken to enhance the [dynamic range](http://en.wikipedia.org/wiki/High-dynamic-range_imaging) (and sometimes the sharpness) of a photographic scene.
The former type of bracketing is also known as *exposure* bracketing, and is what we will be dealing with in this article.
There are many software products offering this functionality, including but not limited to [Hugin](http://en.wikipedia.org/wiki/Hugin_(software)), [digiKam](http://en.wikipedia.org/wiki/DigiKam) and Adobe Photoshop.
A major drawback of these programs, however, is that they are designed mainly for graphical interface use; and will have you click through their interface for every set of bracketed images you wish to stack.
Here we present a rapid and easily-batchable way to stack your exposure bracketed images via a one-liner from the command line.

<!-- more -->

##Basic Function 

The most basic steps needed to stack bracketed shots are:

* *Aligning the images* - this could be skipped for pictures shot with high-end tripods, but is still recommended.
* *Fusing the aligned shots* - this is pretty much the core operation when dealing with bracketed shots.

More advanced features (which are arguably better implemented further downstream in the image processing workflow) include:

* *Cropping to rectangular area* - raw files on certain camera/lens combinations do not represent a perfectly rectangular section of the scene.
* *Lens distortion correction* - some lenses may create slightly "billowed" or "embossed" images (correcting this may also help with the previous point).
* *[Tone mapping](http://en.wikipedia.org/wiki/Tone_mapping)* - this is used to enhance the HDR appearance in limited dynamic range regimens; some scripts made for stacking bracketed shots include this functionality - though it is really best done in the post-processing phase.   

##The [stackHDR](https://github.com/TheChymera/stackHDR) Script

The Hugin software package may in itself be geared towards graphical interface use, yet it ships with a number of functions that can be used from the command line to automate the basic photo processing steps:

* `align_image_stack` - as the name says, this aligns the images
* `enfuse` - this fuses the images

Hugin, sadly, cannot load RAW files, and therefore (in order to keep the 16bit dynamic range) we need to convert the files to [TIFF](http://en.wikipedia.org/wiki/Tagged_Image_File_Format).
This is best done in batch with the `ufraw-batch` command from [UFRaw](http://en.wikipedia.org/wiki/UFRaw).

The stackHDR script (which is available via the aforementioned [GitHub link](https://github.com/TheChymera/stackHDR)) is based on earlier [efforts by Edu Perez](http://photoblog.edu-perez.com/2009/04/script-hdr-with-linux.html), which have also lead to at least [one other offshoot](http://linuxdarkroom.tassy.net/hdr-creation-script/).
Sadly, however, both these solutions are unmaintained at least as of 2011.

The improvements which stackHDR brings are:

* Version tracking via Git
* Longer maintenance timespan via GitHub contributors
* More verbose output
* Clean-run function (which removes all logs and original files) for batch usage
* Lighter dependency spectrum (not requiring the less widely-ported [Pfstools](http://wiki.panotools.org/Pfstools))

Notable omissions of our script include:

* No `.hdr` format output
* No tone mapping functionality

