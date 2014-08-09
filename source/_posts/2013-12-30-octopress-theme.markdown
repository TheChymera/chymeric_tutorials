---
layout: post
title: "Write Octopress Themes"
date: 2013-12-30 06:30
author: Horea Christian
googleplus_user: 117525803180879614771
comments: true
categories: [Octopress, visual design, coding]
published: true
---

[Octopress](http://Octopress.org/) is a fast and clean blogging platform which advertises itself as "a blogging framework for hackers".
Here we provide the first comprehensive documentation on how to best create new Octopress themes by hacking the default theme (or any theme based on it).
We base our instructions both on general tools which you can use for better hacking and on solutions to popular use cases.

<!-- more -->

This documentation assumes that you are somewhat aware of how Octopress generates your site. 
The key concepts here are that all theming should be done exclusively in the ```/sass``` (mainly for CSS) and ```/source``` (mainly for HTML) directories (as relative to your blog root);
and that generating your blog via ```$ bundle exec rake generate``` processes styles and layouts defined in those directories and creates a slightly differently formatted static output exported to ```/public```.

## General Tools

To hack beyond the scope of documented use cases it's best to have a tool which quickly matches parts of the visual output to code snippets.
You can do this via an *element inspection* function in your browser (as for example the [Chrome DevTools](https://developers.google.com/chrome-developer-tools/)).
These functions allow you to either highlight parts of the website with your cursor and see the code - or browse through the code and see individual sections (e.g. DIVs).

Once you have identified a section and a style specification which interests you (e.g. ```margin-left: 1.3em;```), you can try to locate it in the theme directories via grep.
Grep is part of the [GNU coreutils](http://www.gnu.org/software/coreutils/), so any linux user should have it out of the box.
It is also easy to [get grep for Windows](http://gnuwin32.sourceforge.net/packages/grep.htm).

{% codeblock Look for the "margin-left: 1.3em;" code snippet in all relevant files (run inside the Octopress root directory): lang:console %}
$ grep -r "margin-left: 1.3em;" source/ sass/
{% endcodeblock %}

This should get you started wherever use case approaches fail.

## Change Fonts

You can customize the fonts of your Octopress website via [Google Fonts](http://www.google.com/fonts#AboutPlace:about) - a framework which allows you to choose between hundreds of free (mostly [SIL Open Font](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=OFL) or [Apache](http://www.apache.org/licenses/LICENSE-2.0.html) licensed) fonts, all with large character sets.
The fonts are loaded in ```/source/_includes/custom/head.html``` and selected in ```/sass/base/_typography.scss```.

You can add the following snippets to your theme to load and use - for instance - the **Lato** font from Google Fonts.

{% codeblock Code snippet for loading Lato - add to the start of "/source/_includes/custom/head.html" lang:html %}
<link href='http://fonts.googleapis.com/css?family=Lato' rel='stylesheet' type='text/css'>
{% endcodeblock %}


{% codeblock Code snippet for using Lato as the header font - redefine "$header-title-font-family" in "/sass/base/_typograpphy.scss" lang:scss %}
$header-title-font-family: 
"Lato",
"Fontdiner Swanky",
"Germania One",
"Poller One", 
"Georgia", 
"Helvetica Neue", 
Arial, 
sans-serif !default;
{% endcodeblock %}

## Change Colors

For the creation of a new theme, colors are best edited under ```sass/base/_theme.scss```.
If you would also like to edit the console (code-block) colors provided by the default [Solarized](http://ethanschoonover.com/solarized) palette by Ethan Schoonover - you can find the relevant color specifications under ```sass/base/_solarized.scss```.

## Center Elements

This is a bit tricky because it depends quite a bit on what elements you are trying to center.
For center-alignment of text inside any element, you should add the ```text-align: center``` specification to the style sheet of the element containing your text.
Additionally, you may want to justify your text (most Octopress themes do not do this) - do this by adding ```text-align: justify``` to the CSS instead of ```text-align: center```.

{% codeblock Code snippet for centering the article title inside its containing element - at the start of "/sass/partials/_blog.scss" lang:scss %}
article {
  header {
    text-align: center;
    }
}
{% endcodeblock %}

This alone may not always suffice to center the text *on the page*.
Often the element containing the text is not centered, meaning that center-aligning the text will only center it inside its container 
(which may be placed anywhere and aligned anyhow on the page).

The most common (and easiest) way to center-align an element via CSS is to set both the left and right margins to ```auto```.

{% codeblock Incomplete code snippet for centering the article DIV inside its containing element - "#content" section in "/sass/base/_layout.scss" lang:scss %}
#content {
  > div, > article { 
    margin-left: auto;
    margin-right: auto;
  }
}
{% endcodeblock %}

Now, as you will notice if you actually try this - it won't work.
Well, at least not just like that.
Many elements in the default Octopress theme (and in many web designs generally) are floats.
The problem with floats is they cannot be center-aligned by design -
they are created to float as far in one direction as it goes.
So, to actually center many of the default Octopress theme elements (as for instance the article container), you will need to change the type of the element to ```block```, or ```inline-block```. 

{% codeblock Code snippet for centering the article DIV inside its containing element - "#content" section in "/sass/base/_layout.scss" lang:scss %}
#content {
  > div, > article { 
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
}
{% endcodeblock %}

Most elements' style sheets are found either in ```/sass/base/_theme.scss```, ```/sass/base/_layout.scss```, or ```/sass/partials/_blog.scss```.
More specific elements (such as the website header or the navigation section) have additional style sheet specifications under ```/sass/partials/``` - for instance ```/sass/partials/_header.scss``` or ```/sass/partials/_navigation.scss```.

## Maintain Good Phone and Tablet Scalability

The default Octopress theme scales quite nicely on mobile phones and tablets by being semi-fixed width.
What semi-fixed means is that the elements of the theme scale in width along with the display, but do so non-linearly - 
which creates a consistent, seemingly "fixed" visual experience.

The website does no complex math for continuous non-linear scaling (though this could be interesting to implement!).
Instead it detects the display width and sets progressively smaller padding sizes (in px) based on 4 discrete monitor width cut-off values:

uses ```$pad-min``` **< 480px <** uses ```$pad-narrow``` **< 768px <** uses ```$pad-medium``` **< 992px <** uses ```$pad-wide```

These values are set at the start of ```/sass/base/_layout.scss``` and you should tweak them to best complement your design.
Also, to maintain quality scaling for smaller-width mobile devices, you should always use the ```$pad-*``` variables for padding spaces which should make way for your content whenever a width constraint is present.
An example of how the code for scaling a padding variable should look like can also be seen in ```/sass/base/_layout.scss```

{% codeblock Changing "padding-left" and "padding-right" contingent on monitor width - in "/sass/base/_layout.scss" lang:scss %}
body {
  > header, > nav, > footer, #content > article, #content > div > article, #content > div > section {
    padding-left: $pad-min;
    padding-right: $pad-min;
    @media only screen and (min-width: 480px) {
      padding-left: $pad-narrow;
      padding-right: $pad-narrow;
    }
    @media only screen and (min-width: 768px) {
      padding-left: $pad-medium;
      padding-right: $pad-medium;
    }
    @media only screen and (min-width: 992px) {
      padding-left: $pad-wide;
      padding-right: $pad-wide;
    }
  }
{% endcodeblock %}

## Keep Your Theme Hackable

Many Octopress themes use the provided customization directories, namely ```/sass/custom``` and ```/source/_includes/custom```, to make changes.
You should generally not do this.
These directories are intended for end-user customization and should **not** be edited when creating a new **theme**.

Adding any code to (or uncommenting any code from) ```/sass/custom/*.scss``` or ```/source/_includes/custom``` will make your theme slightly less responsive, harder to hack by the end-user, and harder to build any further themes on. 

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2013-12-30-octopress-theme.markdown)!</sup>
