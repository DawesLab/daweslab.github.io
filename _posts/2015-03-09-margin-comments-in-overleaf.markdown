---
author: adawes
comments: true
date: 2015-03-09 14:24:00+00:00
layout: post
slug: margin-comments-in-overleaf
title: Margin comments in Overleaf
wordpress_id: 882
categories:
- physics
---

I have started using [overleaf](http://overleaf.com) a lot more these days and came across a nice way to add margin comments and notes (similar to MS Word comments). Simply include the `todonotes` package and then add a note where
you want it:

    \usepackage[colorinlistoftodos]{todonotes}
    \todo{Note text goes here}

Of course this works on any regular latex installation too (i.e. overleaf isn't required). This can be especially important for shared projects and communication between authors.
