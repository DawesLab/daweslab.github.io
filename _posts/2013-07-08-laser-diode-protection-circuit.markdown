---
author: adawes
comments: true
date: 2013-07-08 14:32:17+00:00
layout: post
slug: laser-diode-protection-circuit
title: Laser Diode Protection Circuit
wordpress_id: 771
categories:
- Designs
- experiments
- making
- optics
- physics
- try this at home
---

<span class="caption">](http://dawes.files.wordpress.com/2013/07/screen-shot-2013-07-06-at-6-08-44-pm.png) PCB for laser diode protection circuit</span>

Our lab is building our fourth and fifth lasers so I finally got around to documenting some of the process. I'll be posting related items here in order to share the lore and hopefully help others get to a finished working laser. This installment covers our standard laser protection board [1]. This is a small circuit board that is installed between the laser current supply and the laser diode itself. Specifically, the board is as close to the diode as practical in order to provide maximum protection from voltage spikes, surges, and other nasty stuff. The circuit is pretty simple, a filter reduces noise, three forward diodes will not conduct for normal operation (they won't conduct until the voltage hits 2.1V which is higher than most laser diode operating voltages). There is also a Schottky diode at reversed polarity to provide fast shorting for spikes of the opposite polarity.

The board is simple, and you could certainly make one on some sort of perfboard, but I went ahead and put together a PCB as an excuse to play with [circuits.io](http://circuits.io) — a handy site that combines schematic capture, PCB layout, and board ordering in one online interface.

The PCB and schematic are available for our [Laser Diode Protection Circuit](http://www.circuits.io/circuits/4354), and you can order all the parts from our [Mouser Project](http://www.mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=82bec0eef7). You may have many of the parts already, and the board is 100% through-hole so you can hack it to your hearts content.

[1] Many folks use this circuit, I first saw it in the paper by [MacAdam](http://ajp.aapt.org/resource/1/ajpias/v60/i12/p1098_s1) et al., and subsequently in a design specified by [Todd Meyrath](http://atomoptics.uoregon.edu/unilaser/unibody_files/peripherals/protection_circuit/meyrath_03.pdf). Please correct me if I should cite someone else.
