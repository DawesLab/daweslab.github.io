---
author: adawes
comments: true
date: 2009-12-19 16:31:46+00:00
layout: post
slug: nice-octave-plots
title: Nice Octave Plots
wordpress_id: 235
categories:
- computing
- matlab
- open source software
- teaching
- tips and tricks
tags:
- gnu octave
- octave
- PDF
- plot
---

One thing I look for in a numerical package is the ability to make nice plots (typically PDF) of what I'm working on. I know I could almost always work on my data, export it, and make a great graph... but in keeping with the [80/20 rule](http://en.wikipedia.org/wiki/Pareto_principle) I want to be able to do most of my plots without a lot of extra work. This is especially true if I'm making a one-off plot for class notes. For publications, I'd be happy to hand draw the figure in blood while standing on my head if I had to. The bottom line is: it's 2009, making a nice looking PDF plot should be easy.

Here is an example along with some quick tips I've found along the way. Hopefully these are easier to find for you than they were for me (digging through docs and searching through listservs). Remember, Octave is scriptable so you can save this in a plot template or a function, and make your plots even easier.

<!-- more -->


### Nice EPS output:


{% highlight python %}
h = figure;
set (h,'papertype', '<custom>')
set (h,'paperunits','inches');
set (h,'papersize',[3 2.5])
set (h,'paperposition', [0,0,[3 2.5]])
set (h,'defaultaxesposition', [0.15, 0.15, 0.75, 0.75])
set (0,'defaultaxesfontsize', 14)
plot(rand(50,1))
xlabel('Time (s)')
ylabel('Velocity (m/s)')
print('figure.eps','-deps')
{% endhighlight %}

The commands here select the papertype (as custom) and use inch units (could be 'centimeters' too). Next, set the paper size (figure size) and the position on the paper. The coordinates for paper position are [left bottom width height]. The default axes position is similar, although now in normalized units (between 0 and 1). I like the look of these axes, and there isn't too much whitespace. I also like a clear legible font size (14 in this example). The rest are some axes labels.


### Nice PDF plots


PDF plots are still problematic because it seems like I have to run an extra step. Either I can convert the EPS to PDF, or I can export PDF and then crop the PDF so the whole page isn't showing. For the former option, I just open the EPS in Preview.app and save as a PDF (this gives me the intermediate preview step for free). For the latter option, I have found pdfcrop useful. This is a little utility that ships wih TeX-Live which I have installed as part of MacTex 2008. There is a newer version [MacTex 2009](http://www.tug.org/mactex/2009/). In any case, the only major difference is the final print command:

{% highlight python %}
print('figure.pdf','-dpdf')
{% endhighlight %}

If you have a more elegant solution, please let me know. I think better PDF exports are on the list for Octave development but the current priority (in terms of graphics output) seems to be breaking away from Gnuplot and allowing other graphics backends. In general, this is a good thing. I love Gnuplot, but there are certainly uses where Gnuplot isn't the best tool in the toolbox.

Endnote: I'm using Octave 3.2.2 and Gnuplot 4.2 patchlevel 5 on a PPC mac. These packages were downloaded from [Octave Forge](http://octave.sourceforge.net/index.html).
