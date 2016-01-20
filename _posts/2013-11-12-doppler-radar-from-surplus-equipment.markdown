---
author: adawes
comments: true
date: 2013-11-12 14:32:49+00:00
layout: post
slug: doppler-radar-from-surplus-equipment
title: Doppler Radar from Surplus Equipment
wordpress_id: 816
categories:
- college
- Designs
- electronics
- experiments
- physics
- try this at home
---

For the final projects in my electronics class, there are always a lot of different interests. One student wants to create a radar gun based on doppler-radar principles. This is a more complicated project mostly because at microwave (2—12 GHz) the devices in a circuit don't act like the nice simple components we study with Ohm's law—everything becomes an antenna or a waveguide or both. That said, there are a lot of scrap electronics around with GHz-range components and in fact we have a whole bin of old demos that were designed to show wave effects of microwaves (micro-waves, not the ovens!). The figure shown here is a modern version of what I found.

<span class="caption"> Example microwave demonstration apparatus</span>

You may be able to find an old setup on eBay or lying around in a demo room somewhere collecting dust. These are still very usable in their original purpose, but I wanted to go a little further since radar is a very practical application of 10 GHz signals.
<!-- more -->
Radar (**RA**dio **D**etection **A**nd **R**anging) is a technique for locating objects that may not be visible (i.e. through fog, distance, or darkness). I personally have a strong fondness for radar especially after sailing in the San Juan islands and winding up in heavy fog near a major commercial shipping lane. In addition to helping sailors, pilots, and military operators find what they are looking for, radar can be used to measure object speeds as well. The two most common applications for radar speed detection are police enforcement of speed limits, and weather prediction. Being able to measure the movement of air (and rain within the air) is an important tool for modern meteorologists.

So how can you turn a send/receive radar demonstration into a doppler radar system? First, some background on Doppler radar. The Doppler effect (capitalized because it is named after Christian Doppler) refers to the fact that waves appear to have a different frequency if the receiver is moving toward or away from the source of the waves. You hear the Doppler effect when a car siren drives past you on the street. As it comes toward you, the sound is high pitched, and while it drives away, it sounds a lower pitch. The Doppler effect also occurs for reflected waves. If an object is moving toward a wave source, then the wave reflected off of the moving object has a slightly higher frequency than the original wave. The frequency shift is proportional to the speed of the object.

So Doppler speed detection is really just a matter of measuring the frequency shift between the sent wave and the received wave. Fortunately, there are a variety of reliable ways to measure frequency. One of the most sensitive is our own ear. If we can convert the frequency difference between a sent wave and the received wave to an audible sound, our ear is very good at distinguishing changes in frequency.

As luck would have it, the frequency shift for objects moving at a speed of a few meters per second (standard human speed scales) cause an audible shift in waves that are 10 GHz. To show this, we use the following equation for the Doppler-shifted frequency:

$latex \Delta f = \frac{v}{c}f_0$

where $latex \Delta f$ is the shift in frequency due to reflection from an object moving at velocity $latex v$. $latex c$ is the speed of light in vacuum ($latex 3\times10^8$ m/s) and $latex f_0$ is the frequency of the original wave. A quick calculation shows that an object moving at 3 meters per second would cause a frequency shift of 100 Hz (low frequency audible sound).

But how do we measure the difference frequency? When two waves are combined by multiplication (in a device called a mixer) the output is an interesting combination of frequencies: both the sum of the two input frequencies and the difference of the to frequencies. Since the sum of two waves near 10 GHz is near 20 GHz, we pretty much ignore that part. But the difference frequency is exactly what we want to measure! Fortunately, as we found above, that frequency is already in the audible range so we just amplify the signal and put it into a speaker. The video below shows the system in action.

http://www.youtube.com/watch?v=zSOyC3K3xJE
