---
layout: page 
title: Tachyon
permalink: /tachyon/
---

I was a research intern *(Summer 2012)* at [Tachyon Technologies](http://tachyon.in) between graduating and starting full-time at Yahoo!. I worked on an applied computer vision problem to convert photographs of comic books into individual panels suitable for mobile viewing. My mentor was the CEO and an
[MIT TR35 awardee](http://www2.technologyreview.com/TR35/Profile.aspx?TRID=868).

This was my first exposure to machine learning and image processing. I performed a bunch of experiments and eventually settled on a research prototype that worked well in most cases. I also built an Android application wrapping this research up into a usable tool.

Solving the problem involved a series of steps. better understood in pictures (taken off the [Tachyon Demos site](http://tachyon.in/demos.html)):

![Comicreel Overview](/images/comicreel-1.png)

**Figure 1:** Overview
{:.caption}


   * *Dewarping:* Book pages in photographs usually appear warped and skewed,
     depending on the angle at which the photograph was taken. We need flat
     panels.

![Comicreel Dewarping](/images/comicreel-2.png)

**Figure 2:** Dewarping
{:.caption}

   * *Splitting Panels:* A comic book page consists of a series of panels. We
     needed to cut these out and rearrange them in reading order.

![Comicreel Splitting](/images/comicreel-3.png)

**Figure 3:** Splitting the comic into panels
{:.caption}

   * *Restoring Colour:* The colours in photographs are usually noisy, have gradients, and appear faded. But we know that the comic artist simply filled in outlines with solid colours. We need to restore these colours.

![Comicreel Example 1](/images/comicreel-4.png)

**Figure 4:** Restoring colour
{:.caption}

And the end result:

![Comicreel Example 2](/images/comicreel-5.png)

**Figure 5:** Result
{:.caption}