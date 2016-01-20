---
author: adawes
comments: true
date: 2008-03-06 07:05:12+00:00
layout: post
slug: why-i-love-python
title: Why I love python
wordpress_id: 128
categories:
- computing
- open source software
- physics
---

![python logo](http://dawes.files.wordpress.com/2008/03/python.png)As you can imagine, during the depths of my thesis-writing experience, I don't have a whole lot of time for anything except... well, writing my thesis. Sometimes, especially in the sciences, as you are writing the paper, the data is still coming in and ideally still getting better. Lucky for me that was the case today. The new data meant new analysis, which for my project means more python code.

It's never happened to me before, but today was a notable day in my evolution as a programmer: I wrote my first non-trivial program, from an empty file, to working code, in one iteration. Now, of course, I can write a "hello world" program in fortran or c++ without debugging (I might have to change linker flags, but that doesn't count), but today it was a real program, doing real things... things that were non-trivial in a programming sense.

<!-- more -->

If you want to know the details, the program runs through an array (presumably time-series data, but it could be anything), checks for level-crossings, interpolates between sampled data points, and returns the interpolated level-crossing as a list of x,y values to make plotting easy. I had level-crossing code before, so it wasn't entirely from scratch, but it was enough to be a real "oh, wow, it worked right the first time!" moment. I know for sure it would have taken me the whole day to work this up in c++. And that is why I love python.
