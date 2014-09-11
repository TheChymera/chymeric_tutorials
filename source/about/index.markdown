---
layout: page
title: "Interact!"
date: 2014-09-11 06:09
author: Horea Christian
comments: true
sharing: true
footer: true
---

Chymerric Tutorials is a robust, reproducible, and transparent collection of documentation and how-to articles [on a large variety of topics](http://chymeric.eu/blog/categories/).

##Features for Readers

Our advanced publishing approach provides a series of features to the average reader, as well as to editors, bloggers, and archivists interested in our content.

###Evergreen Content

Chymeric Tutorials is much less a blog than it is a web resource.
We value the quality and usefulness of our content, and as such keep old pages updated for as long as this is feasible given their respective topics.
Landed on a page authored over one year ago?
Great! You can be sure it also covers vital developments that may have happened since then.

###Version Control

As our pages are updated over time, we also provide curious readers with the opportunity to see a history of all our articles.
Our history is currently published on [GitHub](http://en.m.wikipedia.org/wiki/GitHub) at [this URL](https://github.com/TheChymera/chymeric_tutorials).
Also, for ease of reference, all our pages contain a link to the GitHub location of their respective files.
Consequently, editors interested in referencing our content have both the option of linking to our website (which always shows the latest content) or to a specific revision on GitHub - which will ensure that the content of their reference link remains unchanged.
*Neat - huh?*

###Robustness

A pleasant consequence of our versioning efforts is that our content remains online regardless of any potential crashes of our own (very sturdy!) servers.
Even if our website is down - and you need our content ASAP - you can find it on our [GitHub repository](https://github.com/TheChymera/chymeric_tutorials).
Further, we use [Git](http://en.m.wikipedia.org/wiki/Git_(software)) beyond the scope of just GitHub.
Our content is thus backed up on a multitude of our machines; and in fact you can easily copy it yourself, as well!

###Reproducibility



## Comment!
Commenting is simple, fast and fun!

Bear in mind, though, that our pages are versioned and change over time.
If you comment on any specific content please specify the revision which you are referring to.
You can find the identifiers of all revisions (the SHA checksums) by clicking the link displayed at the bottom of every page
- which commonly looks like this:

<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/interact/index.markdown)!</sup>

Once you are on the article's GitHub page you may continue by clicking on the **History** button in the top right.
The topmost revision is the latest, and you can copy the identifier (SHA) by simply clicking the button which appears when you hover the entry.


## Fork!
If you would like to directly and 100% constructively contribute to our website you may do so by *modifying its content*!

Every article contains a link to its GitHub page at the very end. You can navigate to that link and *fork* the article (or our entire website) into your own Git repository.

If that all just sounded like gibberish to you - don't fret! 
It's actually quite simple.
To get started you just need to [register on GitHub](https://github.com/).
After you have an account the **Edit** buttons on the upper right of all our article pages will become active and you can start editing from a convenient and pretty point-and-click visual interface!
Don't forget to add yourself under the ```author:``` section after you have edited the file!

Now, wasn't that easy?


## Submit Pull Requests!
If you are satisfied with your work and would like to see it published on our blog (along with recognition of your authorship) you may use the convenient GitHub **Pull Request** button to ask us to publish your work.
This will create a pull request page, where we can discuss how to best merge your file into ours.

Also, before submitting a pull request please make sure you have formatted your work according to our writing standards.
A brief rundown:

* Octopress-flavored markdown syntax (as seen in any and all of our own posts)

* Each sentence or “block of meaning” (think long statements in parentheses) on a separate line

* Citations formatted as links, like in the example below:

{% codeblock How to write citations in markdown: %}
Your text contains a statement about [khat][giannini1986] and then some more things.

After a while your text ends, and then you append the following reference, which will not be printed in the document - but only used to format the link and link-hover text display.

[giannini1986]: https://www.ncbi.nlm.nih.gov/pubmed/3734955 "Giannini AJ, Burge H, Shaheen JM, Price WA (1986). “Khat: another drug of abuse?”. Journal of Psychoactive Drugs 18 (2): 155–8."
{% endcodeblock %}
The code above would look like:

---

Your text contains a statement about [khat][giannini1986] and then some more things.

After a while your text ends, and then you append the following reference, which will not be printed in the document - but only used to format the link and link-hover text display.

[giannini1986]: https://www.ncbi.nlm.nih.gov/pubmed/3734955 "Giannini AJ, Burge H, Shaheen JM, Price WA (1986). “Khat: another drug of abuse?”. Journal of Psychoactive Drugs 18 (2): 155–8."


## Cite!
Well, this is not that interactive really, but our commitment to versioning is first and foremost in order to allow people to *cite* our articles.
Providing references is indispensable for making verifiable claims in media, publications, or social networks;
and sadly, most of the blogosphere cannot provide that.
Posts may change without a notice, or disappear altogether - 
and your citation? Puff!
 
We are different! 
Via the **History** section of every GitHub article page - which we diligently link to at the end of every post - you can obtain a static link which will remain the same and online for as long as our repository exists.

Is your citation so valuable that the immense trust - which I am sure you honor us with - *still* does not suffice?
No problem!
You can fork our repository on your machine or on your GitHub account.
Now, even if we *wanted* to delete all of our hard work - we could not.
You (and many others, we hope) would still have a copy.   

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/about/index.markdown)!</sup>
