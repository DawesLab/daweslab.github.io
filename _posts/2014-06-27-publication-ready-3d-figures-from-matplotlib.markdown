---
author: adawes
comments: true
date: 2014-06-27 17:54:08+00:00
layout: post
slug: publication-ready-3d-figures-from-matplotlib
title: Publication-ready 3D figures from Matplotlib
wordpress_id: 847
categories:
- graphics
- open source software
- physics
- python
- tips and tricks
tags:
- matplotlib
- plotting
---

[![Screen Shot 2014-06-27 at 9.23.25 AM](http://dawes.files.wordpress.com/2014/06/screen-shot-2014-06-27-at-9-23-25-am.png?w=143)](http://dawes.files.wordpress.com/2014/06/screen-shot-2014-06-27-at-9-23-25-am.png)I'm a big fan of scripting my plot creation. I also use python for all of my data acquisition and analysis. This naturally put me in a spot to dive into matplotlib when it came time to create figures for a paper I'm working on. It took a bit of digging, but I worked through the kinks and put together a 3D surface plot (with contours) that is PDF and publication ready. I addressed the several issues by overriding the defaults. I want to clarify that I like the defaults for on-screen display, presentations, and posters, but they weren't quite right for a tiny two-pane figure in a two-column manuscript. Things I "fixed" include:

  * Too many ticks and labels
  * Small fonts (when reduced to publication dimensions)
  * Tick labels misaligned relative to ticks (problem seems to come from using larger fonts to fix the previous issue)
  * Odd axes label alignment, rotation, and placement
  * Busy background (removed the gray panes with gridlines)

Some of the solutions were easy, some are hackish and only one uses the lightly-documented [_axinfo](http://matplotlib.1069221.n5.nabble.com/Axes3d-have-improved-handling-of-label-placement-yet-td41498.html) dict. I'll highlight a few snippets that were useful in this process (full code linked below).
<!-- more -->


## Fontsize


To adjust the font sizes, I took the rc approach which modifies the global settings (at least within this script). The following three lines take care of the font style/size issues:

{% highlight python %}rc('font',size=28)
rc('font',family='serif')
rc('axes',labelsize=32){% endhighlight %}

Notice that this requires the use of `from matplotlib import rc`.
I didn't like the spacing between the tick labels and the axes so I use the following six lines to loop through the tick labels and set their alignment parameters:

{% highlight python %}
[t.set_va('center') for t in ax1.get_yticklabels()]
[t.set_ha('left') for t in ax1.get_yticklabels()]
[t.set_va('center') for t in ax1.get_xticklabels()]
[t.set_ha('right') for t in ax1.get_xticklabels()]
[t.set_va('center') for t in ax1.get_zticklabels()]
[t.set_ha('left') for t in ax1.get_zticklabels()]
{% endhighlight %}

Where `.set_va` is a method to set the vertical alignment, and .set_ha sets the horizontal alignment. Notice that the alignment choice depends on the axis in order to get the label close to the axis.


## Background


To clear out the grid, remove the gray fill and outline the panes (i.e. create an empty cubic wireframe around the plot) I use the following:

{% highlight python %}
ax1.grid(False)
ax1.xaxis.pane.set_edgecolor('black')
ax1.yaxis.pane.set_edgecolor('black')
ax1.xaxis.pane.fill = False
ax1.yaxis.pane.fill = False
ax1.zaxis.pane.fill = False
{% endhighlight %}

A final note of caution, in my testing, I found that the visibility of parts of the pane edge depends on the viewing angle. I found that setting the view to `ax1.view_init(elev=10, azim=135)` worked to see all the edge lines. Notice that this does put the x and y axes in a counter-intuitive orientation. For my purposes, those directions are arbitrary, but that may not always be the case.


## Tick placement


There are two things I changed about the ticks, first, the way they point and how long they are. I like ticks pointing into the plot that leave a clean edge around the boundary. To achieve this I did have to dive into the realm of `_axinfo` (here be dragons):

{% highlight python %}
ax1.xaxis._axinfo['tick']['inward_factor'] = 0
ax1.xaxis._axinfo['tick']['outward_factor'] = 0.4
ax1.yaxis._axinfo['tick']['inward_factor'] = 0
ax1.yaxis._axinfo['tick']['outward_factor'] = 0.4
ax1.zaxis._axinfo['tick']['inward_factor'] = 0
ax1.zaxis._axinfo['tick']['outward_factor'] = 0.4
ax1.zaxis._axinfo['tick']['outward_factor'] = 0.4
{% endhighlight %}

Notice the order isn't what I'd expect: I had to set the inward factor to zero and increase the outward factor. This may be a bug so don't count on it to always work (and don't count on access to `_axinfo` at all for that matter).

The final change to the ticks was to use a different tick placement. Matplotlib has several to choose from and I wanted to select an even interval so the MultipleLocator ticker is my tool. Load it with `from matplotlib.ticker import MultipleLocator` and then implement for all three axes as follows:

{% highlight python %}
ax1.xaxis.set_major_locator(MultipleLocator(5))
ax1.yaxis.set_major_locator(MultipleLocator(5))
ax1.zaxis.set_major_locator(MultipleLocator(0.01))
{% endhighlight %}

This is not automagic so you'd have to change the base interval (or make it programmatic) if you want a general-purpose figure script. I personally have some quick and dirty figure-making scripts (using mostly defaults) for analyzing my own data and then I write up a specific script to create a specific plot for the manuscript. Much of those scripts get heavily reused, but this was the first time I had to create a 3D surface plot and also the farthest I've had to dig into matplotlib. I figured I'd document it for that reason. Good luck, and I hope you find this helpful.

Thanks to Ben Root for the tip on setting the pane edgecolor... that piece took me the longest to work out.

[Original source for the figure](https://github.com/DawesLab/Qfunction/blob/master/PubQfunc.py).
