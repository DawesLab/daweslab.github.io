---
author: adawes
comments: true
date: 2009-12-19 01:27:35+00:00
layout: post
slug: build-a-laser-tripwire
title: Build a Laser Tripwire
wordpress_id: 265
categories:
- college
- experiments
- physics
- teaching
tags:
- electronics
- exam
- optics
- teaching
---

<span class="caption">](http://dawes.files.wordpress.com/2009/12/laser.jpg)</span>

I gave my final in Electronics on Tuesday (Dec. 15), and it went so well,  I can't stop thinking about it. The format was something I haven't tried before: 1.5 hours of written test (individual) and 1 hour of group problem solving. The problem they had to solve was to construct a laser tripwire alarm.

There are seven students in the class, so putting them all in one big group is feasible, but I was worried about students not participating or being pushed out of the project by other students. It turns out that I had nothing to worry about, they delegated and divided perfectly, coming back together to get over some hurdles and then breaking apart again to complete their roles. They passed with 12 minutes to spare, and even left it set up as a demo at their project showcase party. My only hope is that future classes work together as well as this group did.

<!-- more -->The written portion of the test wasn't anything special, but it was important for evaluating student mastery of the subject. The group problem is the part I am especially happy with, and it went like this: I gave them a box that included the following parts:



	
  * Digital multimeter

	
  * LCR meter

	
  * Laser diode and power supply

	
  * Headphone speaker (cannibalized from broken headphones)

	
  * Photoresistor (5 k to 0.5 k ohm, dark and lit).

	
  * Resistors: 30, 1k, 22k, 51k ohm.

	
  * Capacitors: 0.01 uF and 0.02 uF.

	
  * 2N3904 (NPN transistor)

	
  * LM555 timer IC (and datasheet)

	
  * Breadboard and jumper set


With the parts they were given the task of building a laser tripwire alarm. The system had to sound an alarm whenever the path of the a laser beam is interrupted.

With more parts, there would be many possible solutions to this problem, so I tried to limit the scope of the test by restricting the components to a bare minimum. I made it work using only these components and relying on information we learned in class. The test had a good mix of challenges for the students: they had to design several circuit blocks and interface them, use a datasheet to learn and use a new device (555 timer), and debug under time pressure.

The solution they came up with was very similar to my own: use the photoresistor in a voltage divider to drive the transistor base high or low. The transistor then gates power to the 555 timer which is configured as a 50% duty-cycle square-wave generator (schematic available in the datasheet). The 555 timer can drive a 50 ohm load, so putting a small resistor in series with the headphone worked like a charm. This is probably not the most robust or fault-tolerant design, but it works and it takes very few parts.

It was so much fun to watch them solve this problem that I think I'll run group questions on the midterms next time around. The best part for me was watching one student (who has been at the tail of the grade curve all semester) catch and fix two of the major problems they ran into with thier circuit. His struggles during the semester really paid off since he was now one of the better debuggers in the group.

If you have had good or bad experiences with group tests, I'd love to hear about them. I may have gotten lucky with my first attempt, but it seemed like a great way to test everyone without watching them fail for making silly mistakes.

UPDATE: Now with schematic drawing
<span class="caption">](http://dawes.files.wordpress.com/2009/12/lasertripwire.png)</span>
