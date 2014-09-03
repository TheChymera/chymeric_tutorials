#Chymeric Tutorials Repository

Git repository for the [Chymeric Tutorials blog](http://chymeric.eu).
This repository contains all files unique to the blog and their history dating back to the orginal publication date.

##Cite Stable Versions

Websites in general and blogs in particular are often unsuited for citation in texts striving to provide reliable sources.
This is chiefly because the content of a web-URL (to a blog post or wiki article) may be modified at any time without notice or ways to retrieve the previous version.
The Chymeric Tutorials Blog provides a high degree of reliability as a citable source by backing up and versioning its entire content.

While we recommend viewing our content through our website for the best reading experience;
we encourage citation of fixed versions via links to our repository hosted on the reliable and stable GitHub service.
In this way your citation links will remain accessible whatever happens to our website, and the content they point to will always be the same.

You can view a history of our updates by clicking the ["commits" link above](https://github.com/TheChymera/chymeric_tutorials/commits/master).
You may browse versions of each particular file by clicking through the file tree above.
Our actual articles are all under [```/source/_posts/```](https://github.com/TheChymera/chymeric_tutorials/tree/master/source/_posts).

##Reproduce this Website

Reproducible content is a vital to the quality control and transparency of any source of information.
To this end, we are happy to offer you the possibility of cloning **our entire** website.

To obtain a publishing-ready identical copy of the [Chymeric Tutorials Blog](http://chymeric.eu) on your machine, please follow the instructions below.

###Get Octopress

As per the [upstream instructions](http://octopress.org/docs/setup/):

    $ git clone https://github.com/imathis/octopress.git tutorials
    $ cd tutorials
    $ gem install bundler
    $ bundle install
    
###Get our Theme of Choice

We use the [whitespace theme](https://github.com/lucaslew/whitespace) for our website, and this repository also contains visual customizations matching that theme.

    $ git clone https://github.com/lucaslew/whitespace.git .themes/whitespace
    $ rake install['whitespace']
    
###Replace Octopress Git Data with Chymeric Tutorials

    $ rm -rf .git
    $ git init
    $ git remote add origin https://github.com/TheChymera/chymeric_tutorials.git
    $ git fetch --all
    $ git reset --hard origin/master
  
And generate the [Chymeric Tutorials Blog](http://chymeric.eu):

    $ rake generate

###Compatibility Issues

Sometimes the Octopress upstream code (the current standard Octopress instructions are to pull from the development branch) might have been updated, and we might not yet have gotten a chance to update our content accordingly.
This seldom happens but it does happen every once in a while.
You usually notice something went awry when the above step (`$ rake generate`) fails.

The files usually to blame for breakage are `Rakefile` and `_config.yml`.
You can view a comparison between our version and the latest Octopress development master with the following code (ideally you should replace all lines in the comparisons with the upstream versions - save for those containing customizations such as blog name, author, etc.):

```
git remote add octopress https://github.com/imathis/octopress.git
git fetch --all
git difftool master octopress/master Rakefile
git difftool master octopress/master _config.yml
```

If that won't work, you will have to find out which of the many other files pointed out by `git difftool master octopress/master` are responsible.

##Push Content
If you would like to contribute to our website you would have to contact us for ssh login data.
If you would like to host a mirror or fork of our website somewhere else, you would have to edit the following bits

    ssh_user       = "m4nt1s@redwings.dreamhost.com"
    ssh_port       = "22"
    document_root  = "~/chymeric.eu/"

of your ```Rakefile``` file.

Other than that, you're good to go!

##Update Your Website Dependencies

###Theme Updates

From your blog directory (using the *whitespace* theme as an example):

    $ git -C .themes/whiteapace pull origin master
    $ rake install['whitespace']
    $ git fetch --all
    $ git reset --hard origin/master
    $ rake generate
    
###Octopress Update

Please remember that this might be subject to some breakage if (when) upstream Octopress updates `Rakefile` or `_config.yml` syntax.
If things don't work after the update, check these two files in particular on upstream and use a merge tool (e.g. [meld](http://en.wikipedia.org/wiki/Meld_(software))) or manually replace all the lines not containing custom content.

    $ git remote add octopress https://github.com/imathis/octopress.git #you only need to do this the first time
    $ git fetch --all
    $ git reset --hard octopress/master
    $ bundle install
    $ bundle update
    $ rake update_source
    $ rake update_style
    $ git -C .themes/whitespace pull origin master
    $ rake install['whitespace']
    $ git rm --cached -r .
    $ git reset --hard origin/master
    $ rake generate
    
