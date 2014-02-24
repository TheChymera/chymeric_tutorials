---
layout: post
title: "Free and Open Science for Your Thesis"
date: 2013-10-11 07:24
comments: true
categories: FOSS, science, FOS, LaTeX, PythonTeX, dissertation, open science
published: false
---

Topics such as [open peer review](http://en.wikipedia.org/wiki/Open_peer_review), [open data](http://en.wikipedia.org/wiki/Open_science_data), and [open notebook science](http://en.wikipedia.org/wiki/Open_notebook_science) are of increasing interest to the scientific community.
Many of the concepts behind this new spin on science are rooted in the [FOSS](http://en.wikipedia.org/wiki/FOSS) (Free and Open Source Software) world and draw credibility from its staggering success.
As such, we would refer to the aforementioned set of trends in science as **FOS** (Free and Open Science).

With so much talk about FOS going on - and even spilling over into [high-profile editorials about publication review][nature2006] - it is distressing how little FOS is actually taking place.
Talking about the next big thing is indeed quickening, but we would rather **show you** how to **become** a part of it.
And what better place to start your voyage into both academia and the FOS world than your thesis or dissertation?

<!-- more -->

## Why My Thesis/Dissertation?
Firstly, there is no better time to start than early.

Secondly, your thesis is among many other things a sandbox.
It is one of the last steps in your academic career where being adventurous about your work comes at little expenditure.

Lastly, the format of the classical thesis implies some sort of information sharing outside the framework of journals.
The (unconfirmed) suspicion hangs high that publishers may decide not to accept open notebook research (for more on this read [this interview by *Nature*][nature2008]).
The special circumstances of work performed as part of a thesis would however provide additional protection against such risks.

## Learning by Example
To aid in your comprehension of the following instructions we would like to point you to the following Master's thesis: [“Neuronal Correlates of Occulometric Parameters in Face Recognition”](https://github.com/TheChymera/masterarbeit).
This thesis is written and programmed in accordance with many FOS concepts and we will be discussing excerpts from it to showcase individual features of FOS.

You are also very welcome to fork the said GitHub thesis repository and prune the code so that it can compile locally on your machine.
We're here fore and happy to guide you along, but hacking is a great way to learn too!

## Requirements
To set up a thesis similar to [our example](https://github.com/TheChymera/masterarbeit) you need:

* **[TeX Live](http://en.wikipedia.org/wiki/Texlive)** - for document rendering (available in [Portage](http://en.wikipedia.org/wiki/Portage_(software)) as app-text/texlive)
* **[Matplotlib](http://en.wikipedia.org/wiki/Matplotlib)** - for rendering figures (in Portage as dev-python/matplotlib)
* **[PythonTeX](https://en.wikipedia.org/wiki/User:Chym%C3%A6ra/PythonTeX)** - for integration of python data processing output (strings, figures) in LaTeX (in the Portage *science overlay* as dev-tex/pythontex)


## Publishings 
If you are just now setting out into the world of FOS, we recommend publishing your thesis (or any other open research projects) via [GitHub](https://en.wikipedia.org/wiki/GitHub).
Additionally - and for the thesis format specifically - we encourage you to use the [LaTeX](https://en.wikipedia.org/wiki/Latex) document preparation system. 

### GitHub and Git 
GitHub (register [here](https://github.com/)) is a social coding website which helps you make your work openly available on the web, and which allows others to easily contribute.
GitHub uses the popular [Git](https://en.wikipedia.org/wiki/Git_(software)) version management system -
meaning that on GitHub you will also benefit from all the feature of Git, of which the following are of particular relevance to FOS: 

* A detailed overview of your files' history 
* Solid backups and proof of authorship 
* The possibility to create and rejoin branches (divergent versions of your work).

After installing git (available in Portage as dev-vcs/git), you can clone our example thesis and all its history to your local machine via:
{% codeblock  lang:bash %}
$ git clone https://github.com/TheChymera/masterarbeit.git
{% endcodeblock %}

### LaTeX 
LaTeX helps you create reproducible and high-quality typeset documents.
It is the standard markup language for most high-profile typographies and a great number of scientific journals.
 
One drawback of LaTeX in the context of FOS is that it is geared towards static, for-print output formats (as for instance ```.pdf```) and integrates less well with web-based publishing than Markdown or IPython would.
However, as typography is of greater concern to your thesis than portability, we would still recommend LaTeX over other alternatives here.

## Live Data Analysis 
Analyzing data on the fly removes the uncertainty and intransparence inherent in off-line data analysis.
Additionally, live data analysis saves you a great deal of time in the long run:
Whenever you may complete your data with additional samples, or whenever you may update your processing scripts you will no longer need to re-export any graphics.
All the new data and processing will pipe through your document without any expenditure on your part.

###PythonTeX

PythonTeX is a library that tries to provide integration between programing and markup languages.
Its strongest suit (as the name suggests) is Python integration in LaTeX.

Pythontex can be used to produce both figures or text (including tables) from python functions and place that into your ```.tex``` document.
To call functions from your document, you need to place them in an appropriate environment (the following excerpt is sourced from [the dedicated environment listing file](https://github.com/TheChymera/masterarbeit/blob/master/pythontex/pycode.tex) of our example thesis):

{% codeblock  lang:python %}
\begin{pycode}[pe_ss1]
pytex.add_dependencies('/home/chymera/src/faceRT/analysis/RTforCategories.py')
pytex.add_dependencies('/home/chymera/src/faceRT/analysis/data_functions.py')
pytex.add_dependencies('/home/chymera/src/faceRT/analysis/gen.cfg')
sys.path.append('/home/chymera/src/faceRT/analysis/')
import RTforCategories
data_pe_ss1 = RTforCategories.main(experiment='6px-4px-6steps', prepixelation=0, source='server', elinewidth=1, ecolor='0.3', make_tight={"pad": 0})
fig_pe_ss1 = latex_figure(save_fig(fig_width=6.64, fig_height=3), caption='Reaction times for Hariri-style face matching. Scrambled images for simple visual recognition were preprocessed only with a scrambling cluster of the sizes indicated in the graphic (sizes given in pixels). Reaction times for non-response trials were counted as \SI{5}{\second}. The error bars represent the standard deviation.', label='r_pe_ss1')
\end{pycode}
{% endcodeblock %}

## Open Data


[nature2006]: http://www.nature.com/nature/peerreview/debate/index.html "“Nature's Peer Review Debate”. Nature 2006"
[nature2008]: http://www.nature.com/news/2008/080915/full/455273a.html "Katherine Sanderson. “Data on display”. Nature 15 September 2008. doi:10.1038/455273a"
