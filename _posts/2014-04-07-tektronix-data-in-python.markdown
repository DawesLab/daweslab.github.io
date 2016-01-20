---
author: adawes
comments: true
date: 2014-04-07 14:30:54+00:00
layout: post
slug: tektronix-data-in-python
title: Tektronix data in Python
wordpress_id: 832
categories:
- computing
- Designs
- open source software
- physics
- python
tags:
- oscilloscope
- tektronix
---

<span class="caption">](http://dawes.files.wordpress.com/2014/04/screen-shot-2014-04-06-at-6-29-06-am.png) Screenshot of python code for viewing and saving data from Tektronix scopes.</span>

In the Photonics and Quantum Optics lab, I've made open-source a high priority. With that in mind, we've written software to interface with many of our instruments. We also rely on [github](http://github.com/DawesLab) for version control and dissemination of our code. I'm particularly happy with a small application that pulls data from a Tektronix oscilloscope (tested on TDS1000 & 2000 models). This is my first python GUI app, despite having worked in python quite heavily for the past 12+ years. If you are interested, the work-in-progress code is [available](http://github.com/DawesLab/instruments) and should work for a Tek scope plugged in to USB on a linux host. I can't promise it works on other platforms.

Here is a partial list of the requirements:



	
  * Python

	
  * numpy

	
  * matplotlib

	
  * wxPython

	
  * python-usbtmc


All but the last are fairly standard for scientific use of python. The last can be installed by your package manager. In Fedora, run

    
    yum install python-matplotlib-wx


and that should ensure that you have all but the last of these components installed. I used the python package manager "pip" to install the usbtmc package:

    
    pip install python-usbtmc


Credit for this project also goes to Eli Bendersky for an awesome [example](http://eli.thegreenplace.net/2008/08/01/matplotlib-with-wxpython-guis/) that got me 90% through this process.
