---
author: adawes
comments: true
date: 2012-03-31 14:58:38+00:00
layout: post
slug: python-fourier-mac
title: Fast Python Fourier Transforms on Mac
wordpress_id: 582
categories:
- computing
- open source software
- optics
- physics
- python
- tips and tricks
tags:
- fft
- fftw
- fourier
- mac
- numerical libraries
- python
- python distribution
- transform
---

[![Fourier Transform](http://imgs.xkcd.com/comics/fourier.jpg)](http://xkcd.com/26/)I use numerical fast fourier transforms (i.e., FFTs) a lot in optics research and so far I've been doing the hard-hitting numerical work in c (or even Fortran... laugh if you must but it's fast!). As I get more comfortable in python, and numpy in particular, I've decided to begin porting some projects to python. This code will have lots of nice python features that will make analyzing and presenting results much easier. To keep things moving along quickly, I'm using compiled numerical libraries for the FFT. In particular, I have both FFTW and Intel MKL libraries to use. Now to get them into python...

Fortunately, less than two months ago, [Henry Gomersall](http://hgomersall.wordpress.com/) [posted](http://hgomersall.wordpress.com/2012/02/01/the-joys-of-cython-numpy-and-a-nice-fftw-api/) his python wrappers for FFTW so I gave [pyFFTW](https://github.com/hgomersall/pyFFTW) a shot. Working primarily on the mac platform wasn't a major obstacle but there are some steps I had to sort out in order to get good performance from the combination (pyFFTW and FFTW itself). This post describes what ultimately worked, and has some tips that may be useful to others in the same situation.

At first, I was running a 32-bit version of python from the [Enthought Python Distribution](http://enthought.com/products/epd.php) (EPD). I ran at 32-bits because some of their toolchain is not 64-bit compatible. It turns out I don't use much of that toolchain at the moment, and there is a new alternative that makes this problem moot. In any case, my first attempt to install pyFFTW resulted in no performance improvement over stock numpy fft libraries. I compiled FFTW using many combinations of compiler flags and never saw more than a 5% speedup over numpy's fft.

Next I upgraded to 64-bit python (via EPD) and installed [macports](http://www.macports.org/) [FFTW libraries](http://www.macports.org/ports.php?by=name&substr=fftw). Note, to have the full functionality of pyFFTW, be sure to install all three fftw-3 ports: fftw-3, fftw-3-long, and fftw-3-single. These provide FFT routines for three different precisions, double, long-double, and single, respectively.

With 64-bit python, and macports libraries, I have a fast pyFFTW install. FFTs take about 1/5 the time using pyFFTW compared to using stock numpy fft routines. This makes it all worth it. If you are playing with FFTW on mac, I can at least vouch for the macports FFTW libraries and I definitely recommend Henry's pyFFTW if you're using python. These wrappers keep the flexibility of FFTW without being hard to use.

I can't say for sure if 64-bit python, or the macports FFTW libraries had a bigger impact. My hunch is that 64-bit code helps the most, but it is also likely that I didn't compile FFTW in a very optimal way when I did it myself. The bottom line is that the macports FFTW install works great, and saves a lot of compile time.

For what it's worth, I'm working to sort out the relevant compile flag options. The macports libraries were compiled with the following configure options:

    
    --enable-threads --disable-fortran --enable-shared


and cflags:

    
    -fno-common -O3 -fomit-frame-pointer -fstrict-aliasing


If you are interested in compiling your own FFTW libraries on Mac, these should be a good starting point. I have tested these configure options (but not the CFLAGS) with Xcode 4.3 (gcc 4.2) and they are definitely not as fast as the macports libraries. The pyFFTW test suite runs at 11.36 ms compared to 5.56 ms with macports FFTW. Surely the O3 flag, and others are important, but I wanted to try with a stock command line first.

In a future post I'll compare FFTW compiled with gnu compilers to that compiled with Intel compilers. I don't expect another 5x speed boost, but it may make a difference in my code where I typically run tens of thousands of FFTs per simulation.
