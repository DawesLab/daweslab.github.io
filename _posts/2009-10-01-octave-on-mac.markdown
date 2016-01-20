---
author: adawes
comments: true
date: 2009-10-01 23:26:32+00:00
layout: post
slug: octave-on-mac
title: Octave on Mac
wordpress_id: 230
categories:
- college
- computing
- links
- matlab
- open source software
- physics
- teaching
---

<span class="caption"></span>

I have been interested in [GNU Octave](http://www.gnu.org/software/octave/) for a while, although never bothered to play much since I had access to recent Matlab releases while I was at Duke. Now that I am managing my own software budget, and trying to keep it to $0, I have a new found appreciation for Open Source Software. Of course, I like regular free-as-in-beer software too, but I've always preferred to use work that is licensed in an open way.

For anyone else who has been hesitant, Octave is now mature enough to be a Matlab replacement. You may even be impressed to find comparable toolboxes... also for free (as in speech and beer). I want to get to know Octave enough to use it in the classroom. At Pacific, we use Maple a fair bit and in the introductory courses, Excel is a stand-by for quick one-off data plots. Both of these tools are well suited to some tasks, but lack some of the features that a package like Octave offers. One definite advantage to Octave in the classroom: students who learn Octave will effectively know Matlab and can add that to their resume.<!-- more -->

I expect a certain amount of resistance when it comes to teaching students using a CLI, but honestly, it can't be as frustrating as some of the strangeness in Maple's document interface. I like Maple for doing integrals, algebra, and plotting functions, but generating data and importing data to process aren't as much fun.

I've also been looking into [SciPy](http://scipy.enthought.com), a python-based toolset with a Matlab feel (less a few exceptions). At this point, I find SciPy to be a good tool for me as a programmer and researcher. However, as a teaching tool, it requires too much familiarity with Python and programming in general. The IPython shell, and some other offerings like the Enthought Python Distribution, have the potential to change that. With [matplotlib](http://matplotlib.sourceforge.net), IPython can be pretty close to Matlab; the biggest difference is how to deal with arrays and ranges.

The best part about it, is that Octave Forge now packages [Octave.app](http://sourceforge.net/projects/octave/files/Octave%20MacOSX%20Binary) (and Gnuplot.app) into drag-and-drop installers. Since the mac is my platform of choice (and the platform used in one of our teaching labs), this is a big deal for me. Note: the Gnuplot.app is located in the "Extras" folder when you download Octave.app. Simply drag both into /Applications and you are off to the races.
