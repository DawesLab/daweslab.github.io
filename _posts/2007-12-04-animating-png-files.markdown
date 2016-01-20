---
author: adawes
comments: true
date: 2007-12-04 06:15:43+00:00
layout: post
slug: animating-png-files
title: Animating PNG files
wordpress_id: 98
categories:
- computing
- open source software
- tips and tricks
tags:
- animate
- c++
- codec
- divx
- mac
- perian
- png
---

I have struggled with optimizing the process of animating PNG files. I have [code](http://dawes.wordpress.com/2007/12/03/writing-pngs-from-c/) that generates a PNG image based on an array of data, which, in my case is the intensity of an optical beam, but it can be anything. I have found various options ranging from quick-and-dirty to fairly robust. MEncoder plays a role in several of them, and it was no easy feat to find a combination of flags that properly encode the video for playback on linux and Mac platforms. Here, I present my two most promising options so far.




To clarify the usage, the commands quoted are what I used on a linux machine,  which where I run C++ code to generate the images. I want to view movies on both linux and mac platforms (especially since I give presentations on my mac). The viewing is done with either mplayer (linux) or quicktime player (mac).




<!-- more -->



### Quick-and-dirty




As part of the [ImageMagick](http://www.imagemagick.org/) package, the `animate` command works fairly well. My images all have a common filename chunk so I use:



`animate *_frame.png`



This shows an animation of the frames, slowly first as they load into memory, and then at a framerate that can be set on the command line. You can also slow it down with the ">" key, and speed it up with the "<" key. Those seem backwards but YMMV.





### MEncoder




My files are generated from the [pngwriter](http://pngwriter.sourceforge.net/) libraries and they don't seem to play nice with MEncoder for some reason, although I'm still trying to track that reason down. In any case, ImageMagick comes to the rescue:



`mogrify -format jpg -quality 90 *.png`



The resulting JPG files can then be assembled into a DivX movie using:



`mencoder mf://*.jpg -mf fps=25:type=jpg -ovc lavc -lavcopts vcodec=mpeg4 -oac copy -o output.avi -ffourcc DX50`



I initially tried the same command but with `*.png` and `type=png`, as claimed in the MEncoder manual, but to no avail. All of the other codecs available to me (on a departmental machine) also either segfaulted or returned empty movies with the PNG files. Converting en-masse to jpeg is a hack, but it works. The `-ffourcc DX50` flag came to me from the [gentoo-wiki Mencoder HOWTO](http://gentoo-wiki.com/HOWTO_Mencoder_Introduction_Guide#Video_Codecs). This flag simply sets the video type to something that the player is likely to understand.





Of course your mileage may vary, but this series of commands works for me to animate PNG files and put them into a compressed video. Note, I have installed the DivX codecs on my mac laptop by installing the open-source [Perian](http://perian.org/) package. Having a DivX codec is a requirement to play these files. I am searching for a clear howto on creating mac-friendly videos, but right now I'm just trying to understand the codecs that ship with the mac. Historically there isn't a lot of AVI support built in to QuickTime player so that is a sticking point for most of the possible video formats.
