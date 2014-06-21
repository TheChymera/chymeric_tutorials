---
layout: post
title: "per-photo model release form"
date: 2014-06-06 07:30:38 +0200
author: <a rel="author" href="https://plus.google.com/117525803180879614771/about">Horea Christian</a>
comments: true
categories: [model photography, legal, meta]
published: false
---

[Model release](http://en.wikipedia.org/wiki/Model_release) forms help photographers secure the freedom to publish and sell their photography work.
One common issue with model release forms (especially in the context of informal photo sessions) is that they are tailored to the practice of professional photography, and commonly grant the photographer all rights to *all* pictures they may have taken of the model.
While for professional models this might not be an issue, for relatives, friends, and acquaintances of the photographer such a commitment becomes daunting.

Here we present a model release form concept based on encryption technology which you can use to transfer rights for single photographs.

<!-- more -->

##Legal Disclaimer

*This document does not address every circumstance or possibility, and might not fit all of your needs exactly. Further, it is not intended as legal advice. Horea Christian and other authors of this work are not lawyers and take no responsibility for the use of this form. Your use of this Model Release in no way creates an attorney-client relationship between you and Horea Christian, or any other person or entity. We suggest that you contact a lawyer to discuss your circumstances, and verify that this Release fits your needs.*

##The Model Release Form

A versioned repository of our release form is published [on GitHub](https://github.com/TheChymera/model-release-form), and the document is available for **[direct download here](http://chymera.eu/resources/mrf/mrf.pdf)**.

The document is written in the LaTeX markup language, and the text is based on a number of other model release forms published on the internet.
We have tried to be as inclusive as possible in the document, and we welcome law-aware contributions with different versions for different countries.
We also provide check-boxes to accommodate not only per-photo model release, but also the more generic all-photos model release. 

##Single Photo Specifications

For per-photo model release we include a form structure with which you may specify and accurately identify up to 10 individuals photos.
This works via [MD5 checksums](http://en.wikipedia.org/wiki/Md5), sequences of 32 hexadecimal digits which uniquely identify your photos.
While explaining [checksum](http://en.wikipedia.org/wiki/Checksum) functions exceeds the scope of this article, the gist of the concept is that two photos with a difference of even only one pixel will still have different MD5 checksums.

On most Unix-like operating systems (OS X, Linux, BSD, etc.) checksums can easily be computed in the command line via by entering: 

```bash
md5sum /path/to/your/original/photo
```

Windows users may use a number of free online services instead - such as [this](http://sha1md5checksum.bugaco.com/cryptocalc/index.html).

After obtaining the checksum of the photos for which the photographer desires release rights, these 32 digit sequences should be transcribed to the document.
Due to the sequence length we provide 2 entries per photo, in which both photographer and model can transcribe the code to ensure it is correct.

The picture being accurately identified and assuming the agreement is legally valid, you secure the rights over both the original image and all derivative works.
All you need to do is keep the original file on record and evidence that all resulting pictures are indeed processed from it.
You can always recalculate the checksum and it will always be the same.
This is pretty much it!

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-06-06-per-photo-model-release-form.markdown)!</sup>

