---
author: adawes
comments: true
date: 2012-06-25 21:18:15+00:00
layout: post
slug: spinning-my-wheels
title: Spinning my wheels
wordpress_id: 609
categories:
- physics
- stories and anecdotes
- try this at home
---

I have a flat tire on my subaru outback. This is an all-wheel-drive (AWD) vehicle so the manual (and many websites) recommend replacing all four tires if one goes bad. Fearing a tire-industry-funded scam, I had to investigate. Here are the facts:

My car has a 57.5 inch track distance (wheel spacing, 1998 subaru, info from [Vehix](http://www.vehix.com/car-reviews/1998/subaru/outback/vehicle-specifications))

My tires, when new are 26.3 inches in diameter (205/70-15 tires, from [tire size calculator](http://ejelta.com/tiresize/index.html?tiresize=185/60-15))

The minimum highway curve for a 55 mph road has a radius of 1060 feet (from the [NJDOT Roadway Design Manual](http://www.state.nj.us/transportation/eng/documents/RDM/sec4.shtm#Table45))

**Question:** If I drive in a circle (or any circular path) what is the typical number of differential revolutions between two tires on a single axle. This exercise is to test the claims that I need to replace all four tires at once in order to maintain proper driving load on the differentials in the drivetrain. I understand that if the tires are different sizes, one spins faster than the other... but how much is too much?

First, for a circle of radius 1060 feet, the different circumference of this path for my two front wheels separated by 57.5 inches is:

left wheel = pi*1060 feet while the right wheel = pi*(1060 feet + 57.5 inches). The difference is clearly equal to pi*57.5 inches, or 4.588 meters. Now, how many tire revolutions is that?

4.588 meters / (pi * 26.3 inches) = 2.18 revolutions.

You may think: _"But that is only while driving around a tight circle! Most curves aren't so tight."_ Look back at our first calculation, the difference in the distance traveled is only related to the wheelbase not to the actual radius of the curve! So we can generalize this to any driving distance on any path.

In absolute terms, any closed path results in 2.18 extra revolutions of one tire (or pi times the track width of your car if it is different)... regardless of the turning radius, distance traveled, or any other factor. If your path is a closed loop that turns right (clockwise from a bird's view) then your left tire went farther, and if your loop turns left (counterclockwise), it's the other way around. This may seem totally counter-intuitive but it is true. Pick _any_ closed path, and the difference between the distance traveled by the inner tire and that traveled by the outer tire is pi times the wheel separation distance (track width).

Back to our task at hand. [Tire rack](http://www.tirerack.com/tires/tiretech/techpage.jsp?techid=18) has a discussion of this that runs the math for a 1/8" difference in diameter on a 25" diameter tire... that would lead to an extra 4 revolutions per mile. Almost double what we find for a one-mile closed-loop trip. On the other hand, it's double a small number. What does this mean for my tires? Really what it means is that if my average round trip is a mile, I put just over 2 extra revolutions worth of wear on the differential. But with tires of different sizes, I can put additional wear on the differential with every mile—even driving straight.

**Solution:** If I replace only the bad tire, then I know which tire is (slightly) larger. Say it's a left tire. As long as I make more left-turn trips than right-turn trips, I can mostly cancel out the extra rotations! The down-side is that on long road trips, I'd need to drive in a circle every mile to keep the rotations equal... maybe I'll replace the four tires after all :-)
