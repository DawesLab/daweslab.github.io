---
author: adawes
comments: true
date: 2008-02-22 11:42:26+00:00
layout: post
slug: math-fonts-in-latex
title: Math fonts in LaTeX
wordpress_id: 124
categories:
- physics
tags:
- bitstream charter
- fonts
- latex
- math
---

![Bitstream Math Font](http://dawes.files.wordpress.com/2008/02/bitstream-math-font.png)

Tired of Computer Modern or Times when you turn to LaTeX to document your hard work? This post outlines the relatively simple process of using another font that adds a bit more style to your documents. The general challenge is to find a font for the math that matches the text font. This is solved with the [mathdesign](http://www.ctan.org/tex-archive/help/Catalogue/entries/mathdesign.html) package for LaTeX.




<!-- more -->



Incidentally, there is a nice [overview](http://ctan.tug.org/tex-archive/info/Free_Math_Font_Survey/survey.html) of other text and math font pairings by Stephen G. Hartke hosted on ctan. Check it out to see a [sample](http://ctan.tug.org/tex-archive/info/Free_Math_Font_Survey/images/chartermd.png) of my new favorite, Bitstream Charter, in action.





These instructions exist in various places on the internet, but as much for my sake as for anyone else's, I'll post them here as well. First, you will need the [mathdesign](http://www.ctan.org/tex-archive/fonts/mathdesign/) package. Download `mdbch.zip` and `mdcore.zip` and put them in the root folder of your texmf tree. Unzip both, and run either "texhash" or "mktexlsr" (often one of these is aliased to the other, so either should work). Now you want to use "updmap" to update the font maps. You can do this by either adding a line like "Map mdbch.map" to your updmap.cfg file, or you can simply run `updmap --enable Map mdbch.map`. If you are root, the first may be easier, and more official. Otherwise, you'll probably have to use the latter option. They both work equally well.





Finally, to use bitstream Charter in a LaTeX document, include the following lines in the beginning of your tex file:
`\usepackage[T1]{fontenc}
\usepackage[bitstream-charter]{mathdesign}`




Enjoy!
