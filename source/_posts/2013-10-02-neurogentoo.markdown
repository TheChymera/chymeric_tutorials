---
layout: post
title: "How-To: NeuroGentoo"
date: 2013-10-02 09:15
author: Horea Christian
comments: true
categories: [Gentoo, neuroscience]
---

## Gentoo

[Gentoo linux](http://en.wikipedia.org/wiki/Gentoo_Linux) is a modern, extremely flexible, and very transparent linux distribution.
Among many other things it provides:

* Rolling releases (continuous versioning, in brief: no tedious “OS version updates” for you - ever)
* Building from source (custom geared for every machine - from ancient laptop to data-analysis power-box)
* Seamless support for live source packages (get that *very latest* version with that one new function that solves all your problems - directly from the source code upstream wrote 5 minutes ago!)

Cutting the Gentoo publicity short, and getting to the point: **Gentoo is awesome for science**.



## Neuro

### Already In!

Sadly, until July 2013 Gentoo provided almost no neuroscience software.
In response, we started writing up some [ebuilds](http://en.wikipedia.org/wiki/Ebuild) for popular neuroscience (mainly neuropsychology, to be precise) software packages.
With the help of a handful of enthusiastic Gentoo-Science overlay maintainers we have managed to help [Portage](<http://en.wikipedia.org/wiki/Portage_(software)>) bring you up-to-date and development versions of the following software packages (in order of ebuild pull):

* sci-biology/**psychopy**
* sci-biology/**pybrain**
* sci-libs/**nipy**
* sci-libs/**nipype**
* sci-libs/**nibabel**
* sci-libs/**pydicom**
* sci-biology/**mne-python**
* sci-biology/**pysurfer**

<!-- more -->

Which you can conveniently access over the popular and stable [**gentoo-science**](https://github.com/gentoo-science/sci) overlay.
To enable the overlay we suggest you follow the “Manually setting overlay locations” instructions from the [Gentoo overlay guide](http://wiki.gentoo.org/wiki/Overlay).
In short, the procedure is:

  1. Add ```PORTDIR_OVERLAY="/usr/local/portage/sci"``` (or whatever directory you prefer) to your ```/etc/portage/make.conf``` file.
  2. Run ```git clone https://github.com/gentoo-science/sci.git /usr/local/portage/sci``` (or whatever other directory you previously chose).

There - wasn't that easy?

### Work In Progress:

But all is not always fun and games in the world of NeuroGentoo.
Arguably the most important software packages for neuropsychology and brain imaging - [AFNI](http://en.wikipedia.org/wiki/Afni), [FSL](http://en.wikipedia.org/wiki/FMRIB_Software_Library), and [SPM](http://en.wikipedia.org/wiki/Spm) - got stuck in the pull phase.
Apparently the packages do not really meet Gentoo security, build, and file management exigences and need to be patched - quite a bit.
The Project is community-lead, and help would be much appreciated!

But the good news is: 
The packages kind of work!
Not yet well enough for the gentoo-science overlay, but perhaps well enough for you and me.
So, these are the packages we are still working on (and which you can already use):

* sci-biology/**afni** - relevant [pull request](https://github.com/gentoo-science/sci/pull/115)

* sci-biology/**fsl** - relevant [pull request](https://github.com/gentoo-science/sci/pull/118)

* sci-biology/**spm** - relevant [pull request](https://github.com/gentoo-science/sci/pull/107) *(works wthout MATLAB!)*

While officially unsupported, these packages are just as easy to get as the supported ones.
You can simply merge the NeuroGentoo branch from our gentoo-science fork into your local gentoo-science repository.
**After** following the gentoo-science overlay instructions from the previous section, run:
   
```bash
cd /usr/local/portage/sci
git remote add chymera https://github.com/TheChymera/sci.git
git pull chymera neurogentoo
```
    
## NeuroGentoo!

Now that you have read, understood, and followed the instructions above - **How-To: NeuroGentoo** boils down to the following:

### Emerge!

The stable versions are at your fingertips - and if you want the cutting-edge development versions you can just [tell Portage](http://wiki.gentoo.org/wiki/Knowledge_Base:Unmasking_a_package). 

{% codeblock To install - for instance - PsychoPy, simply emerge from a root shell: lang:console %}
# emerge psychopy
{% endcodeblock %}

### Contribute!

Yes, NeuroGentoo is supported by Gentoo users and neuroscientists (if you are here you might well be at least one of those) - 
we do not have paid employees nor do we make a direct profit from this.
We contribute because neuroscience is important and Gentoo is awesome!

Please submit patches and contribute to the pull requests for [AFNI](https://github.com/gentoo-science/sci/pull/115), [FSL](https://github.com/gentoo-science/sci/pull/118), and [SPM](https://github.com/gentoo-science/sci/pull/107)!

Additional packages are welcome, and we would recommend you submit pull requests *directly* to [gentoo-science](https://github.com/gentoo-science/sci).
We will however gladly include any working ebuilds in [our overlay](https://github.com/TheChymera/sci.git) - if they take too long to get into gentoo-science.

### Credits

The Neurogentoo initiative is coordinated by [Horea Christian](https://github.com/TheChymera), and contributors include [François Bissey](https://github.com/kiwifb) and [Martin Luessi](https://github.com/mluessi).

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2013-10-02-neurogentoo.markdown)!</sup>
