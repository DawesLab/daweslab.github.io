---
author: adawes
comments: true
date: 2015-12-09 16:09:01+00:00
layout: post
slug: printing-on-shims
title: Printing on Shims
wordpress_id: 892
categories:
- 3D printing
---

_An emergency hack saves a doomed print job._

I've been 3d printing since late 2010 when I built my first kit. One thing I learned early on is that overhangs are tricky in printed objects. Generally that means that you either design an object to minimize overhangs or you print with support. Usually you can pick an orientation and part design that work well together and give good results. Sometimes you need to print support. Today, I ran into another issue. I've been printing many items for student projects in my electronics class and got a bit casual about sending files to the printer without looking too closely. I had a full print bed worth of parts running when I realized one part was designed with major overhangs; essentially a flat plate that had some mounting lugs extending up and down from it. The print was already 1/3 through and I didn't want to kill the job it since most of the print would be fine... but I knew that this part of the print would fail. Staring down this impending problem, I figured I'd try a hack and at least see if I could salvage the print job.

I looked through my gcode in octoprint to see where the overhang would kick in (layer 13 it turns out). Grabbed enough index cards to make a stack about 13*0.25mm high and started cutting. When I had a reasonable set of cards ready to go, I waited for layer 12 and paused the print. I started to stack the cards and tape them down with kapton tape. Based on feel, the layer height wasn't 0.25mm so I pulled a few cards off the stack until they felt as tall as the existing print. The results are certainly better than if there wasn't any support, and I'm actually surprised it worked as well as it did. Surface quality is actually about as good as it is with support; not as nice as it would be if the surface were more even, but I had to have a way to hold the cards in place so the tape strips show up a bit. In the future, I'd just lay down wide strips of masking tape (i.e. blue tape) since I like the finish it gives and I know PLA sticks to it.

An interesting note is that the cards definitely change the heat properties of the bed but that doesn't seem to have changed the outcome much. I was worried about printing on a cold surface instead of the heated bed but that seems to be an unfounded concern. I suspect ABS may be more picky about this, but the PLA didn't show any warping.

<span class="caption"> Shims in place. The printer was paused at this point.</span>

<span class="caption"> Finished print on the bed. Looks good so far.</span>

<span class="caption"> Part printed on shims shows minor surface defects.</span>

Overall, this definitely worked as a rescue mission. The easiest approach is to avoid the issue with careful design choices. However, some parts need to break the _no overhangs_ rule. And for those parts, shims may be a solution.

Video of the print in action:
[wpvideo lbh1rpZ1]

Update: After posting this I found [Xiang Chen](http://web.xiangchen.me/projects/5)'s work on print-over and other augmented printing techniques. Very exciting, and I'm going to have to start playing with some possibilities along those lines.
