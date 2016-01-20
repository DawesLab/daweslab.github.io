---
author: adawes
comments: true
date: 2007-09-04 17:58:17+00:00
layout: post
slug: final-ruling-on-juggling-riddle-for-now
title: Final ruling on Juggling riddle (for now)
wordpress_id: 64
categories:
- experiments
- physics
---

As referenced earlier, some of us have been going over the physics of an [old riddle](http://rulesoflunch.wordpress.com/2007/08/31/juggling-off-the-weight/). There were a few bits of information lacking from the theoretical analysis so far, although basic kinematics covers most of what you need. For the rest, it turns out, we can follow the work of [Claude Shannon](http://en.wikipedia.org/wiki/Claude_Shannon) famous for Shannon Information Theory and perhaps one of the most influential scientists of the 20th century. For perspective, his master's thesis at MIT suggested that digital circuits should use binary numbers and operate with boolean logic. To say the least, that turned out to be a good idea.

Back to juggling...


<!-- more -->

Shannon proved an equation that describes the relationship between the timing of juggled objects and the number of objects. Shown in Eq. (1) where b is the number of balls, h is the number of hands (presumably two for all juggling bipeds), d is the dwell time (from catch to throw), f is the flight time of each ball, and e is the empty time for each hand (from throw to catch).

![JugglingTheory](http://dawes.files.wordpress.com/2007/09/jugglingtheory.png)

Using this, I'll refer to the post where we determined the condition for the boat sinking is given in Eq. (2). If Eq. (2) is true then the boat sinks. Plug Eq. (3) into (2), solve Eq. (1) for f/d and plug that in next and you get Eq. (4). To compare to some true juggling data ([found here](http://www.juggling.org/papers/OJ/)) we define r in Eq. (5), which can be solved in terms of e/d to be used in Eq. (4). For three balls, two hands, and an average r of 0.63 we arrive at Eq. (7) where the sinking condition is confirmed.

Now I'll keep this problem in mind because this is not a conclusive proof of the riddle solution, it is 75% theory and 25% experimental (using the average r value over many jugglers). The remaining part of the proof would be to show that r can never be such that Eq. (4) is false.
