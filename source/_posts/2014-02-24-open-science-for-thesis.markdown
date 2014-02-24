---
layout: post
title: "Free and Open Science for Your Thesis"
date: 2014-02-24 18:14
comments: true
categories: [FOSS, science, FOS, LaTeX, PythonTeX, dissertation, open science]
published: true
---

Topics such as [open peer review](http://en.wikipedia.org/wiki/Open_peer_review), [open data](http://en.wikipedia.org/wiki/Open_science_data), and [open notebook science](http://en.wikipedia.org/wiki/Open_notebook_science) are of increasing interest to the scientific community.
Many of the concepts behind this new spin on science are rooted in the [FOSS](http://en.wikipedia.org/wiki/FOSS) (Free and Open Source Software) world and draw credibility from its staggering success.
As such, we would refer to the aforementioned set of trends in science as **FOS** (Free and Open Science).

With so much talk about FOS going on - and even spilling over into [high-profile editorials about publication review][nature2006] - it is distressing how little FOS is actually taking place.
Talking about the next big thing is indeed quickening, but we would rather **show you** how to **become a part of it**.
And what better place to start your voyage into both academia and the FOS world than your thesis or dissertation?

<!-- more -->

## Learning by Example
To aid in your comprehension of the following instructions we would like to point you to the following Master's thesis: **[“Neuronal Correlates of Occulometric Parameters in Face Recognition”](https://github.com/TheChymera/masterarbeit)**.
This thesis is written and programmed in accordance with many FOS concepts; and we will be discussing excerpts from it to showcase individual features of FOS.

Those of you already accustomed to [Git](https://en.wikipedia.org/wiki/Git_(software)) and [LaTeX](https://en.wikipedia.org/wiki/Latex) are also very welcome to just fork the said GitHub thesis repository and prune the code so that it can compile locally on your machine.
We're happy to guide you along, but hacking is a great way to learn too!

## Requirements
To set up a thesis similar to [our example](https://github.com/TheChymera/masterarbeit) you need:

* **[TeX Live](http://en.wikipedia.org/wiki/Texlive)** - for document rendering (available in [Portage](http://en.wikipedia.org/wiki/Portage_(software)) as app-text/texlive)
* **[Matplotlib](http://en.wikipedia.org/wiki/Matplotlib)** - for rendering figures (in Portage as dev-python/matplotlib)
* **[PythonTeX](https://en.wikipedia.org/wiki/User:Chym%C3%A6ra/PythonTeX)** - for integration of python data processing output (strings, figures) in LaTeX (in the Portage *science overlay* as dev-tex/pythontex)


## Publishing
If you are just now setting out into the world of FOS, we recommend publishing your thesis (or any other open research projects) via [GitHub](https://en.wikipedia.org/wiki/GitHub).
Additionally - and for the thesis format specifically - we encourage you to use the [LaTeX](https://en.wikipedia.org/wiki/Latex) document preparation system. 

### GitHub and Git 
GitHub (register [here](https://github.com/)) is a social coding website which helps you make your work openly available on the web, and which allows others to easily contribute.
GitHub uses the popular [Git](https://en.wikipedia.org/wiki/Git_(software)) revision control system -
meaning that on GitHub you will also benefit from all the feature of Git, of which the following are of particular relevance to FOS: 

* A detailed overview of your files' history 
* Solid backups and proof of authorship 
* The possibility to create and rejoin branches (divergent versions of your work).

After installing Git (available in Portage as dev-vcs/git), you can clone our example thesis and all its history to your local machine via:

```bash
$ git clone https://github.com/TheChymera/masterarbeit.git
```

### LaTeX 
LaTeX helps you create reproducible and high-quality typeset documents.
It is the standard markup language for most high-profile typographies and a great number of scientific journals.
 
One drawback of LaTeX in the context of FOS is that it is geared towards static, for-print output formats (as for instance ```.pdf```) and integrates less well with web-based publishing than Markdown or IPython would.
However, as typography is of greater concern to your thesis than portability, we would still recommend LaTeX over other alternatives here.

## Live Data Analysis 
Analyzing data on the fly removes the uncertainty and intransparence inherent in off-line data analysis.
Additionally, live data analysis saves you a great deal of time in the long run:
Whenever you complete your data with additional samples, or whenever you update your processing scripts you will no longer need to re-export any graphics.
All the new data and processing will pipe through your document without any expenditure on your part.

###PythonTeX

PythonTeX is a library that tries to provide integration between programing and markup languages.
Its strongest suit (as the name suggests) is Python integration in LaTeX.

Pythontex can be used to produce figures or text (including tables) from python functions and place that into your ```.tex``` document.
A powerful feature of PythonTeX figure piping is that it can use the ```.pgf``` graphics format which natively draws the figure in the LaTeX environment - meaning that text elements in your figure can  be selected and can contain clickable links in the final document.

To call functions from the ```.tex``` source of your document, you need to place them in an appropriate environment (the following excerpt is sourced from [the dedicated environment listing file](https://github.com/TheChymera/masterarbeit/blob/master/pythontex/pycode.tex) of our example thesis):

```python
\begin{pycode}[pe_ss1]
pytex.add_dependencies('/home/chymera/src/faceRT/analysis/RTforCategories.py')
pytex.add_dependencies('/home/chymera/src/faceRT/analysis/data_functions.py')
pytex.add_dependencies('/home/chymera/src/faceRT/analysis/gen.cfg')
sys.path.append('/home/chymera/src/faceRT/analysis/')
import RTforCategories
data_pe_ss1 = RTforCategories.main(experiment='6px-4px-6steps', prepixelation=0, source='server', elinewidth=1, ecolor='0.3', make_tight={"pad": 0})
fig_pe_ss1 = latex_figure(save_fig(fig_width=6.64, fig_height=3), caption='Reaction times for Hariri-style face matching. Scrambled images for simple visual recognition were preprocessed only with a scrambling cluster of the sizes indicated in the graphic (sizes given in pixels). Reaction times for non-response trials were counted as \SI{5}{\second}. The error bars represent the standard deviation.', label='r_pe_ss1')
\end{pycode}
```

As you can see, there are a few functions called here which are not defined in the snippet - they are inherited from the ```{pycode}``` environment.
This is done via [an other dedicated file](https://github.com/TheChymera/masterarbeit/blob/master/pythontex/functions.tex) which is very handy for writing down functions and imports which you will need in all or most of your python snippets.
Upstream has nicely elaborated on this topic [here](https://github.com/gpoore/pythontex/wiki/matplotlib).

Finally, to actually get some output from the above you have to call the snippet via its ID (for the aforementioned example ```[pe_ss1]```).

```latex
\py[pe_ss1]{fig_pe_ss1}
\py[pe_ss1]{tex_nr(ttest_rel(data_pe_ss1[(data_pe_ss1['scrambling'] == 0) & (data_pe_ss1['intensity'] == 40)]['RT'], data_pe_ss1[(data_pe_ss1['scrambling'] == 0) & (data_pe_ss1['intensity'] == 100)]['RT'])[1]/2)}
```

These excerpts are taken from [a chapter of our example thesis](https://github.com/TheChymera/masterarbeit/blob/master/preliminary_experiments.tex).
The first call prints a figure (as seen above, ```fig_pe_ss1``` is the result of the latex figure function), and the second call uses some of the functions loaded [here](https://github.com/TheChymera/masterarbeit/blob/master/pythontex/functions.tex) to perform a t-test and format the output to obtain the best typographical result.
Needless to say, the result of this t-test will be recalculated and the figure re-plotted whenever you update any of the scripts dependencies.

## Open Data

Live data analysis on your machine is awesome in itself - however it is even more awesome to afford others the benefit of seeing your live data analysis work on their machines as welll.
This increases trust and transparency and can greatly ease collaborative research, publishing, and review.

A fresh new approach to sharing data is [Academic Torrents](http://academictorrents.com/).
this initiative has many merits, including being decentralized, and providing feasible high-speed downloads.
As torrents do not serve data directly, piping data from academic torrents to your python scripts would require additional scripting.

In our example thesis we found it far more convenient to serve the data via ```http``` and have python source it from there - without even requiring a formal download.
We do this via the HTML parser in the [data acquisition file](https://github.com/TheChymera/facesRT/blob/master/analysis/data_functions.py) of an [example analysis script](https://github.com/TheChymera/facesRT):

```python
if source == 'server':
	from HTMLParser import HTMLParser
	import urllib
	class ChrParser(HTMLParser):
		def handle_starttag(self, tag, attrs):
			if tag =='a':
				for key, value in attrs:
					if key == 'href' and value.endswith('.csv'):
						pre_fileslist.append(value)
	results_dir = data_path+experiment+'/px'+str(prepixelation)+'/'
	print results_dir
	data_url = urllib.urlopen(results_dir).read()
	parser = ChrParser()
	pre_fileslist = []
	parser.feed(data_url) # pre_fileslist gets populated here
if pre_fileslist == []:
	raise InputError('For some reason the list of results files could not be populated.')
files = [lefile for lefile in pre_fileslist if lefile.endswith('.csv') and not lefile.endswith(ignore_filename+'.csv')]
```

A good tool to put data online is ```rsync```.
We use it running the following from our data root:

```bash
rsync --filter '- */.*' -e "/usr/bin/ssh"  --bwlimit=2000 -av EXPERIMENT_ID user@server.host.com:remote/data/root/
```

An added benefit of this command is that it omits files and folders of the ```*/.*``` format.
You can use this format to store crash logs, botched output, or other (meta)data from your experiments which you may be interested in keeping but which is irrelevant for the data analysis.

Of course for the command to work you need to set up ```ssh``` for your server.
This is totally easy, and most hosting companies have short how-tos for this online (we use Dreamhost, and [here's ours](http://wiki.dreamhost.com/SSH)). 

[nature2006]: http://www.nature.com/nature/peerreview/debate/index.html "“Nature's Peer Review Debate”. Nature 2006"
[nature2008]: http://www.nature.com/news/2008/080915/full/455273a.html "Katherine Sanderson. “Data on display”. Nature 15 September 2008. doi:10.1038/455273a"

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-02-24-open-science-for-thesis.markdown)!</sup>
