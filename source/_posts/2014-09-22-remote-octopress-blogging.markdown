---
layout: post
title: "remote octopress blogging - Sync and Inotify"
date: 2014-10-17 05:51:18 +0200
author: Horea Christian
googleplus_user: 117525803180879614771
comments: true
categories: [octopresss, blogging, meta]
published: true
---

[Octopress](http://octopress.org/) is one of the [most widely used static site generators](https://www.staticgen.com/), and as such attracts a large number of bloggers.
With the advent of [increasing](http://upload.wikimedia.org/wikipedia/commons/8/86/Usage_share_of_web_browsers_%28Source_StatCounter%29.svg) smartphone and tablet computer based internet usage, authors in general and bloggers in particular adapt their habits to write and publish on the go.
Most modern content management systems provide ample possibilities for this - static site generators, however, typically do not.

This is mainly a consequence of the infrastructure requirements that static site generation places on a system (in case of Octopress these being at least [Ruby](http://en.wikipedia.org/wiki/Ruby_(programming_language)) and a number of Ruby gems - possibly also Git), and the fact that most mobile platforms cannot yet meet them.
The different paradigm of static site generator blogging thus mandates a different approach to remote blogging.
Here we present a 2-element (sync and [inotify](http://en.wikipedia.org/wiki/Inotify)-triggered scripts) automatic solution for remote Octopress blogging, and a short section on remote content authoring (sans publication) via [GitHub](http://en.wikipedia.org/wiki/GitHub).

<!-- more -->

##Sync

Sync (or syncing), short for synchronization, describes keeping your directories and files identical over many machines, with updates spreading from the machine they were authored on to all others.
There are many software solutions for this (commonly referred to as sync clients), with some of the more popular being: [Dropbox](http://en.wikipedia.org/wiki/Dropbox_(service)), [Google Drive](http://en.wikipedia.org/wiki/Google_Drive), [BitTorrent Sync](http://en.wikipedia.org/wiki/BitTorrent_Sync), and [Syncthing](http://en.wikipedia.org/wiki/Syncthing) (the latter two being non-could-based, and the latter even being open source).

To set up syncing for static site generation, you need to install your sync client of choice on all your mobile devices **plus** on one (*just* one - in order to avoid update conflicts) machine that is neigh-continuously online. 
This can either be a server (or your shared server space) or simply your desktop computer if you never turn it off.
For the purposes of this guide (since we specifically give inotify instructions) you should also make sure this is a Linux machine.
Once your sync network is ready, simply enable syncing for your blog root - or just for your `/source`  or `/source/_posts` directory.

###Dropbox
In spite of its shortcomings (limited storage, closed-source, cloud-based) we currently recommend Dropbox over all other alternatives for remote static site generator blogging.
This is chiefly due to Dropbox being supported by all major platforms (Windows, OSX, Linux, Android, and iOS), and being well integrated with text-editors on operation systems which do not commonly allow [apps](http://en.wikipedia.org/wiki/Mobile_app) to access the same files (e.g. iOS).

In Dropbox you cannot simply select what directories you want synced, but rather have (one) dedicated `~/Dropbox/` directory where you have to place all your content.
You will thus need to move your blog folder from the location you may have become accustomed to - though this inconvenience can be mitigated by creating a symlink from your previously used path:

```
ln -s /Dropbox/path/to/your/blog /your/accustomed/blog/directory
```

##Inotify-triggered Commands (via Incron)

[Inotify](http://en.wikipedia.org/wiki/Inotify) allows the Linux kernel to detect changes in the filesystem.
Once you have successfully set up syncing you can use this to conveniently trigger site rebuild and deployment whenever a specific event happens in your synced blog directory.
Our (and advisably your) tool of choice for this task is [incron](http://inotify.aiken.cz/?section=incron&page=about&lang=en).

You can configure incron via incron tables (text files that tell it where to look for what events and what to do upon the specified events occurring).
These tables contain single-row instructions formatted as `<path> <mask> <command>`; where `<path>` is watched, `<mask>` specifies what events to look for, and `<command>` specifies the command to run upon occurrence of the aforementioned events.
You can get a list of the incrontab mask tags (as well as a more in-depth explanation of incron tables) from the relevant man page - just run `man 5 incrontab`.
Aditionally, incrontab also provides dollar sign wildcards which you can pass as arguments to your command of choice (more on this also in the aforementioned man page). 

Two things worth an explicit mention here, however, are:

* Incrontab commands [are not fully shell-compatible](http://stackoverflow.com/questions/18238962/incrond-running-but-not-executing-command-under-centos-6-4), meaning that you will not be able to reliably use - among other things - the `&&` or `;` operators. 
This is expecially relevant to our purposes, since you want to change the directory to your blog root, and generate and deploy your blog. 
The issue can be circumvented by calling a script, which you can either write yourself or clone from our [remote-octopress-incron utilities repo](https://github.com/TheChymera/remote_octopress_incron) on GitHub.

* Incrontab does not recursively monitor your directories - meaning that you will have to directly specify your `../source/_posts/` path and manually add multiple entries for all the pages (i.e. `../source/<page-title>` directories). 

A sample incron table for the task at hand (just monitoring your posts) would look somewhat like this:

```
/synced/path/to/your/blog/source/_posts IN_CREATE,IN_DELETE,IN_CLOSE_WRITE ./home/chymera/src/remote_cotopress_incron/update.sh $@
```

It is however advisable to check what inotify events your specific sync agent triggers (since these triggers may vary depending on how the sync client works - as seen in the Dropbox sub-section below).

###Dropbox
If you decide to use Dropbox due to it being the most portable choice, there will be one additional quirk to account for.
Dropbox currently does not open and modify your files in place. instead it moves them to a temporary directory, modifies them there, and moves them back (as tested by us, and also documented [here](http://stackoverflow.com/questions/3795022/dropbox-and-pyinotify)).
It thus becomes mandatory to check for `IN_MOVED_TO` events rather than `IN_CLOSE_WRITE`:

```
/home/chymera/Dropbox/tutorials/source/_posts IN_CREATE,IN_DELETE,IN_MOVED_TO ./home/chymera/src/remote_cotopress_incron/update.sh $@
```

##GitHub

There are a number of published GutHub-based remote Octopress blogging solutions (the most noteworthy documented [here, by Holger Frohloff](http://5minutenpause.com/blog/2013/07/05/remote-posting-with-octopress/)).
Such solutions - though feasible - generally require a bit more trial-and-error scripting and often assume you use not only GitHub, but also GitHub-pages.

For GitHub users we, however, recommend the increasingly powerful web-interface for content creation or editing.
Though it will not publish to your blog without additional scripting, it is easy to edit your content (and commit) directly via GitHub from any mobile platform which is HTML5-compatible.

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-09-22-remote-octopress-blogging.markdown)!</sup>
