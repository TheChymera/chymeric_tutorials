---
layout: post
title: "Preview Octopress Themes with Theme-Space"
date: 2014-11-14 05:45:41 +0100
comments: true
categories: [octopress, themes, design, themespace]
published: false
---

The static site generator [Octopress](http://octopress.org/) is surrounded by a large community which has [generated a large variety of themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes) for it.
Many developers use actual blogs as theme previews, which - as Octopress bloggers are avid hackers - contain many customizations.
Thus, users (newer ones in particular) are oft disappointed by the unexpectedly low amount of chrome they see on their website upon deployment of the default theme.
Some developers instead keep an empty demo site with the default theme - a passable solution - which, however, takes up a lot of time (due to the need to update both Octopress and the theme manually on yet another site).

To make maintaining true-to-the-default demos easier for developers, we present *Theme-Space* - a GitHub-based repository for Octopress theme previews.

## The Concept

Would it not be great if all Octopress themes had reliable ture-to-the-default previews for users to easily peruse upon deciding for their new theme?
Would it not be great if making previews for themes required less manual updating?
Would the second not facillitate the first?

We think it would!
Over on GitHub, [TheChymera](https://github.com/TheChymera) and [Yous](https://github.com/yous) have set up a small organization, called [Theme-Space](https://github.com/themespace), which aims to address much of the above, by:

* Providing a common (but entirely open) platform for Octopress theme previews.
* Publishing scripts for easy update of preview site themes.
* Publishing scripts for easy update of the preview sites' Octopress core.
* Moving previews to a *live* or pseudo-live state by using either [GitHub push notifications](https://help.github.com/articles/receiving-email-notifications-for-pushes-to-a-repository/), a [sync+inotify approach](http://chymeric.eu/blog/2014/10/17/remote-octopress-blogging/), or [Cron](http://en.wikipedia.org/wiki/Cron).
