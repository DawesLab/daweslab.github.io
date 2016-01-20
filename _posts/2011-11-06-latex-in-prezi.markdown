---
author: adawes
comments: true
date: 2011-11-06 21:52:34+00:00
layout: post
slug: latex-in-prezi
title: LaTeX in Prezi
wordpress_id: 535
categories:
- computing
- latex
tags:
- latex
- presentation
- prezi
- swf
---

[![](http://dawes.files.wordpress.com/2011/11/screen-shot-2011-11-06-at-1-50-29-pm.png?w=150)](http://dawes.files.wordpress.com/2011/11/screen-shot-2011-11-06-at-1-50-29-pm.png)I've become a regular Prezi user in the past year, but one thing was holding me back: LaTeX math had to come in via file upload... until now.

The [codecogs equation editor](http://www.codecogs.com/latex/eqneditor.php) has an HTML integration scheme that will let you import a SWF image by entering LaTeX code directly in the URL. If you like this, please donate to CodeCogs... in a few minutes you'll see why you owe them for this hack and not me.

The URL scheme is described at the [HTML integration page](http://www.codecogs.com/latex/htmlequations.php). In particular, something of the form:

    
    http://latex.codecogs.com/gif.latex?1+sin(x)


will generate a gif image of 1+sin(x) in nice LaTeX. Replace gif with swf and you have an swf (flash) file that is ideal for importing to Prezi. For the import process, start editing a prezi and go ahead to the dialog for importing an image. In the image dialog, past the codecogs URL into the field as shown below, and hit enter (be sure to use the swf version of the URL). Prezi recognizes the file as an SWF and goes about importing it as expected.

For the example, I use the URL:

    
    http://latex.codecogs.com/swf.latex?1+sin(x)


<span class="caption">](http://dawes.files.wordpress.com/2011/11/screen-shot-2011-11-06-at-1-33-43-pm.png)</span>

<span class="caption">](http://dawes.files.wordpress.com/2011/11/screen-shot-2011-11-06-at-1-33-59-pm.png)</span>

There will be a short bubble notice that Prezi is thinking... but don't worry, it will do what you want it to.

Next you will see the glorious LaTeX result added to your Prezi in SWF format with all the speed and scalability of flash (the native Prezi format).

Please keep in mind that it is the awesome work of [CodeCogs](www.codecogs.com) that makes this hack work... and they ask for nothing in return. Do the right thing and support them with a small donation.

<span class="caption">](http://dawes.files.wordpress.com/2011/11/screen-shot-2011-11-06-at-1-34-13-pm.png)</span>

I can also suggest that spacing can be added either with LaTeX space commands (\, \quad, etc.) or a single space can be URL-ized with %20. The url with a literal space will not be processed correctly (at least it wasn't when I tried it).

As always, your mileage may vary, but let me know if it helps.
