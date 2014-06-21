---
layout: post
title: "(Faded) Color Processing Profiles"
date: 2013-10-22 03:05
author: <a rel="author" href="https://plus.google.com/117525803180879614771/about">Horea Christian</a>
comments: true
categories: [processing, filters, RawTherapee, color, photos]
published: true
---

In a [tumblr post](http://tmblr.co/ZHI4LqyOnj9f) regarding this issue we presented a conservatively processed version of the image at hand along with 3 of our more polished attempts at using ex-post faded color filtering.
This is part of an ongoing effort to experiment with processing methods which we traditionally regarded as “unprofessional” or, for lack of a better word, “instagramy”.

[{% imgcap  /images/photos/minis/DSC_a8273.jpg 193 0 “Conservative”, Faded %}](http://chymera.eu/photo/blog/DSC_a8273.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-ot.jpg 193 0 Faded Orange-Teal %}](http://chymera.eu/photo/blog/DSC_a8273-ot.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-pb.jpg 193 0 Faded Pink-Blue %}](http://chymera.eu/photo/blog/DSC_a8273-pb.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-rg.jpg 193 0 Faded Red-Gold %}](http://chymera.eu/photo/blog/DSC_a8273-rg.jpg)

A general rationale which speaks against such editing is that perfectly good color space extent is sacrificed for a look which may be regarded as shallow.
On the other hand, many appreciate this sort of look as “artsy” - which is more or less what prompted the effort.
<!-- more -->
Sacrificing some sort of detail for a better *feel* is by no means something uncommon.
Some photographers have been known to [forsake chrominance detail altogether][woodward1939] 
(the argument that this enhances luminance detail no longer holds for modern non-scientific photography),
and denoizing and subsequent sharpening are often used to lose detail on purpose 
(often we make the judgement that we should allow the viewer to concentrate on the contrast of the model's facial contours rather than on the texture of her wrinkles).

Bearing these thoughts in mind, it may be a worthwhile pursuit to see what exactly we can take away from the color space in order to obtain a still-good or maybe even *better* look.

##Processing

[RawTherapee](https://en.wikipedia.org/wiki/RawTherapee) is a modern, professional, cross-platform, and [FOSS](https://en.wikipedia.org/wiki/FOSS) image processing program.
It is widely used by photographers who value transparency in their processing work, and in contrast to many commercial alternatives it provides a good (though not-*yet?*-that-powerful) command line interface for batch processing.
Since 2013 the software also ships with a series of “faded looks” profiles, which we are currently exploring.
The profiles are poorly documented (the only published comments on their function are available [here](https://code.google.com/p/rawtherapee/issues/detail?id=1738)), and left to a more open-ended “artistic” evaluation for usage.
Here we will demonstrate their performance based on one picture, and try to offer some simple guidelines for their usage 
(we would be very thankful for comments to complete this basic guide in the discussion section below, or for [direct contributions](http://photo.chymera.eu/interact/)).

To create this set of profiles we have used a home-brewed python script released [on Github](https://github.com/TheChymera/RTbatch).
In short, all pictures were processed with the bundled processing profiles, then ligthened and denoized with our own custom settings (as the original shot was dark and noisy).
In case you are interested, our profiles can be found [here](https://github.com/TheChymera/RTbatch/tree/master/profiles).  

##The Pictures

[{% imgcap  /images/photos/minis/DSC_a8273-BW_1.pp3.jpg 193 0 BW 1 %}](http://chymera.eu/photo/blog/DSC_a8273-BW_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-BW_2.pp3.jpg 193 0 BW 2 %}](http://chymera.eu/photo/blog/DSC_a8273-BW_2.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-BW_3.pp3.jpg 193 0 BW 3 %}](http://chymera.eu/photo/blog/DSC_a8273-BW_3.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-BW_4.pp3.jpg 193 0 BW 4 %}](http://chymera.eu/photo/blog/DSC_a8273-BW_4.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Deep_Shadows.pp3.jpg 193 0 Deep Shadows %}](http://chymera.eu/photo/blog/DSC_a8273-Deep_Shadows.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Default_ISO_High.pp3.jpg 193 0 Default ISO High %}](http://chymera.eu/photo/blog/DSC_a8273-Default_ISO_High.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Default_ISO_Medium.pp3.jpg 193 0 Default ISO Medium %}](http://chymera.eu/photo/blog/DSC_a8273-Default_ISO_Medium.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Default.pp3.jpg 193 0 Default %}](http://chymera.eu/photo/blog/DSC_a8273-Default.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Equilibrated.pp3.jpg 193 0 Equilibrated %}](http://chymera.eu/photo/blog/DSC_a8273-Equilibrated.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Amber_1_TM_Bright.pp3.jpg 193 0 Faded Amber 1 TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Amber_1_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Amber_1_TM.pp3.jpg 193 0 Faded Amber 1 TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Amber_1_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Amber_1.pp3.jpg 193 0 Faded Amber 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Amber_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Blue_1_TM_Bright.pp3.jpg 193 0 Faded Blue 1 TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Blue_1_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Blue_1_TM.pp3.jpg 193 0 Faded Blue 1 TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Blue_1_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Blue_1.pp3.jpg 193 0 Faded Blue 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Blue_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Blue_Pink_TM.pp3.jpg 193 0 Faded Blue Pink TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Blue_Pink_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Blue_Pink.pp3.jpg 193 0 Faded Blue Pink %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Blue_Pink.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Chocolate_1_TM_Bright.pp3.jpg 193 0 Faded Chocolate 1 TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Chocolate_1_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Chocolate_2_TM_Bright.pp3.jpg 193 0 Faded Chocolate 2 TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Chocolate_2_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Golden_1.pp3.jpg 193 0 Faded Golden 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Golden_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Golden_2.pp3.jpg 193 0 Faded Golden 2 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Golden_2.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Green_1_TM_Bright.pp3.jpg 193 0 Faded Green 1 TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Green_1_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Green_1_TM.pp3.jpg 193 0 Faded Green 1 TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Green_1_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Green_1.pp3.jpg 193 0 Faded Green 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Green_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Green_2.pp3.jpg 193 0 Faded Green 2 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Green_2.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Green_3.pp3.jpg 193 0 Faded Green 3 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Green_3.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Neutral_TM.pp3.jpg 193 0 Faded Neutral TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Neutral_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Neutral.pp3.jpg 193 0 Faded Neutral %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Neutral.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Purple_1_TM_Bright.pp3.jpg 193 0 Faded Purple 1 TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Purple_1_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Purple_1_TM.pp3.jpg 193 0 Faded Purple 1 TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Purple_1_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Purple_1.pp3.jpg 193 0 Faded Purple 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Purple_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Purple_2_TM.pp3.jpg 193 0 Faded Purple 2 TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Purple_2_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Purple_2.pp3.jpg 193 0 Faded Purple 2 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Purple_2.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Teal_Orange_TM_Bright.pp3.jpg 193 0 Faded Teal Orange TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Teal_Orange_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Teal_Orange_TM.pp3.jpg 193 0 Faded Teal Orange TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Teal_Orange_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Teal_Orange.pp3.jpg 193 0 Faded Teal Orange %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Teal_Orange.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Warm_1_TM_Bright.pp3.jpg 193 0 Faded Warm 1 TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Warm_1_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Warm_1_TM.pp3.jpg 193 0 Faded Warm 1 TM %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Warm_1_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Warm_1.pp3.jpg 193 0 Faded Warm 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Warm_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Warm_2.pp3.jpg 193 0 Faded Warm 2 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Warm_2.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Faded_Warm_3.pp3.jpg 193 0 Faded Warm 3 %}](http://chymera.eu/photo/blog/DSC_a8273-Faded_Warm_3.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-High-Key.pp3.jpg 193 0 High-Key %}](http://chymera.eu/photo/blog/DSC_a8273-High-Key.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Natural_1.pp3.jpg 193 0 Natural 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Natural_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Natural_2.pp3.jpg 193 0 Natural 2 %}](http://chymera.eu/photo/blog/DSC_a8273-Natural_2.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Neutral.pp3.jpg 193 0 Neutral %}](http://chymera.eu/photo/blog/DSC_a8273-Neutral.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Pop_1.pp3.jpg 193 0 Pop 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Pop_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Pop_2_L.pp3.jpg 193 0 Pop 2 L %}](http://chymera.eu/photo/blog/DSC_a8273-Pop_2_L.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Pop_3_Skin.pp3.jpg 193 0 Pop 3 Skin %}](http://chymera.eu/photo/blog/DSC_a8273-Pop_3_Skin.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Pop_4_BW.pp3.jpg 193 0 Pop 4 BW %}](http://chymera.eu/photo/blog/DSC_a8273-Pop_4_BW.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Portrait_Lejto.pp3.jpg 193 0 Portrait Lejto %}](http://chymera.eu/photo/blog/DSC_a8273-Portrait_Lejto.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Portrait_Smooth.pp3.jpg 193 0 Portrait Smooth %}](http://chymera.eu/photo/blog/DSC_a8273-Portrait_Smooth.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Punchy_1.pp3.jpg 193 0 Punchy 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Punchy_1.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Punchy_2.pp3.jpg 193 0 Punchy 2 %}](http://chymera.eu/photo/blog/DSC_a8273-Punchy_2.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Natural_TM.pp3.jpg 193 0 Skintones - Natural TM %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Natural_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Natural.pp3.jpg 193 0 Skintones - Natural %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Natural.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Pale_TM_Bright.pp3.jpg 193 0 Skintones - Pale TM Bright %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Pale_TM_Bright.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Pale_TM.pp3.jpg 193 0 Skintones - Pale TM %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Pale_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Pale.pp3.jpg 193 0 Skintones - Pale %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Pale.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Soft_Texture.pp3.jpg 193 0 Skintones - Soft Texture %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Soft_Texture.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Strong_Texture.pp3.jpg 193 0 Skintones - Strong Texture %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Strong_Texture.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Studio_TM.pp3.jpg 193 0 Skintones - Studio TM %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Studio_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_Studio.pp3.jpg 193 0 Skintones - Studio %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_Studio.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_StudioBase_1_TM.pp3.jpg 193 0 Skintones - StudioBase 1 TM %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_StudioBase_1_TM.pp3.jpg)
[{% imgcap  /images/photos/minis/DSC_a8273-Skintones_-_StudioBase_1.pp3.jpg 193 0 Skintones - StudioBase 1 %}](http://chymera.eu/photo/blog/DSC_a8273-Skintones_-_StudioBase_1.pp3.jpg)

##Evaluation

As promised, we are concluding with some basic guidelines for usage of the bundled RawTherapee profiles (which would also apply to similar profiles released in the future).

######Faded:

* **Faded colorized profiles** provide a cleaner appearance by masking patchy redness of the skin.
* The **“Faded Chocolate”** and **“Faded Purple”** color profiles are well-suited for emphasizing items other than skin (in our case the clothing) - as they leave skin tones rather desaturated.
* Generally, the **faded monochrome** colorizing profiles look dull (we predict this is detrimental not just for this but for very many compositions).
* Overall we believe that the best results for our composition are achieved with 2-color faded filters (these would be: **teal-green**, **pink-blue**, and gold - which we would refer to rather as **red-gold** since it also very nicely accentuates the reds of the picture). 
Their outstanding performance is due to successful masking of skin imperfections, while still allowing for good color contrast and feature emphasis (as their color range is broader than in monochrome pictures).

######Non-Faded:

* The **“Pop”** profiles, as the name indicates, make facial features pop more, though at the cost of also emphasizing coarseness or imperfections of the skin.
* The **“Portrait Lejito”** profile generates popping features *and* masks skin imperfections - it does however make make-up look smudged and exaggerated. 
* The **“Punchy”** profiles overly flatten the colours (in our case detrimental).

#####“Not enough” you say? Help us make this guide more useful! Comment or [contribute](http://photo.chymera.eu/interact/)!	
[woodward1939]: http://www.smithsonianmag.com/arts-culture/Shades-of-Ansel-Adams.html "Woodward, Richard. “Ansel Adams in Color”. Smithsonian Magazine."

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_photography/blob/master/source/_posts/2013-10-22-faded-color-filters.markdown)!</sup>
