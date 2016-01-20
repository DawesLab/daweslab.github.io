---
author: adawes
comments: true
date: 2011-12-19 15:00:48+00:00
layout: post
slug: data-manipulation
title: Data manipulation
wordpress_id: 545
categories:
- bad science
- graphics
tags:
- chart
- data
- tv
---

This isn't a political post, it's a post about data, and ethics. When you read a graph, you start with the assumption that whoever made the graph followed a set of basic guidelines. Breaking these guidelines _can_ happen by accident, but with computerized tools, this is rare. With the availability of graph software, making an X-Y graph misrepresent data requires some effort. Sometimes you can even prove it was intentional.

The case study here is a television graphic presented last week. Here is the original on-air version:

<span class="caption">"][![Fox data on unemployment](http://dawes.files.wordpress.com/2011/12/foxnews.jpg)](http://dawes.files.wordpress.com/2011/12/foxnews.jpg)</span>

There are two big problems with this graph. I'm not going to address graph design, chartjunk, or any other aspects beyond the fundamentals. Once this graph is _technically correct_, we could argue those points. Here we'll focus on graphs 101... the basics.

**The scale** is clearly wrong on the left of the chart. 9% roughly lines up with the data but the peak at 9.2 almost lines up with 9.5 on the scale. The valley (8.8) is close to 8.5 on the scale. Despite the error, this doesn't really matter because most line graphs are used to indicate a trend. As long as the trend is correct, we can forgive an error on the scale.

**The trend** is not only wrong, but it has been manipulated. This can be shown by comparing the data presented above to the [actual data](http://data.bls.gov/timeseries/lns14000000). First, in order to even compare these charts, we have to fix the scale issue. It turns out that the scale was wrong by exactly 1/2 so it seems reasonable to assume that an error was made in the preparation where either the data or the scale were reduced in size in order to make things fit. Perhaps it was more pleasing to see 8 and 10 as round numbers on the screen. The data doesn't vary by much so that scale would have made it seem too flat (a legitimate trick for skewing data perception). This kind of mistake happens... it shouldn't, but it does. With the scale fixed, the data sets overlap very well except for two key areas:

<span class="caption"> and TV news graphic (red)."][![TV vs reality](http://dawes.files.wordpress.com/2011/12/fox-vs-reality.png)](http://dawes.files.wordpress.com/2011/12/fox-vs-reality.png)</span>

You can spot the difference without my help. Just to be open, honest, and clear I have added error bars that represent the confidence interval for gathering data from the screenshot presented above. Thanks to [GraphClick](http://www.arizona-software.ch/graphclick/) software, this is an easy thing to do. The blue line is the original data from the [source](http://data.bls.gov/timeseries/lns14000000), and the red is the (scale corrected) TV version.

Consider the process of making a graph:



	
  1. Start with a data set

	
  2. Import data into software

	
  3. Choose fonts, colors, points, backgrounds, lines, labels, etc.

	
  4. Show graph on TV


Somewhere between steps 3 and 4 two things have happened. First, the scale shrunk (possibly to make 8 and 10 fit nicely on the TV screen). Second, at least two data points got tweaked. Perhaps you want to give the benefit of the doubt and assume that the last point was accidentally duplicated to show two points at 9 instead of one at 9 and one way down at 8.6. Ok, I'll let you think that. How can we explain why the next lowest point (March, 8.8) got shifted so far up? And why did the February point move down? Moving one point down doesn't cancel out moving another one up! This is data manipulation, this is what the same network continues to call [Climategate](http://www.foxnews.com/scitech/2011/12/16/complicit-in-climategate-doe-under-fire/)!

Sure, they could say "we gave you the raw data in yellow." Yes, but the graph is supposed to reinforce the numbers and represent them accurately. There are many ways to screw this up by accident... this was not an accident; **someone grabbed those points in the graph and moved them around. **
