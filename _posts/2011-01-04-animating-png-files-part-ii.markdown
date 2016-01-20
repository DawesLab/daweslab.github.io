---
author: adawes
comments: true
date: 2011-01-04 22:00:59+00:00
layout: post
slug: animating-png-files-part-ii
title: Animating PNG Files part II
wordpress_id: 245
categories:
- computing
- open source software
- physics
tags:
- animate png file open source
---

[![ffmpeg](http://dawes.files.wordpress.com/2011/01/ffmpeg-logo.png?w=150)](http://dawes.files.wordpress.com/2011/01/ffmpeg-logo.png)As an update to a previous post on [animating png files](http://dawes.wordpress.com/2007/12/04/animating-png-files/), I want to describe what I have found to be a good workflow for the process. To recap, I have some numerical code that generates a series of PNG files that are indexed numerically as: 000_frame.png, 001_frame.png, ... , 256_frame.png. This format is determined by the generating code, and allows easy ordering of the frames by filename.

<!-- more -->

I have found [ffmpeg](http://ffmpeg.org/) to be the most effective solution, although there are ways to do the same thing with mplayer's associated toolbox mencoder. ffmpeg works like a charm, and I’d have to say that the command-line options for ffmpeg leave mencoder in the dust. For example, I can use

ffmpeg -i %03d_frame.png frames.mp4

to take the sequence of files above and make the mpeg 'frames.mp4'. There are the advanced flags for users that need them, but in the spirit of making easy things easy and hard things possible, ffmpeg is a winner.

The only mildly tricky part about the command above is that the wildcard %03d matches parts of the filename that have 3 digits "3d" and are zero-padded on the left ("0" in the 03d). The files I have are all 001_frame.png and 002_frame.png etc. Another important note is that this requires the numbers that match the %03d to be in sequence (i.e., starting at 001 and not skipping numbers). Your mileage may vary but I'm happy to help debug if you have any issues. There might be things I've forgotten now that this workflow has been built in to my data processing setup.
