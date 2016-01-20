---
author: adawes
comments: true
date: 2013-04-10 14:32:50+00:00
layout: post
slug: qutip-the-quantum-toolbox-in-python
title: 'QuTiP: The Quantum Toolbox in Python'
wordpress_id: 653
categories:
- computing
- open source software
- physics
- python
- tips and tricks
---



![](https://code.google.com/p/qutip/logo?cct=1337152688)

I've been tinkering with it for a while, but I am finally sitting down to write about [QuTiP](https://code.google.com/p/qutip/), a great toolbox for doing quantum mechanics in the Python computing language. A couple things came together recently to re-ignite my interest and get me to think about QuTiP again. First was an email and later [blog post](http://qutip.blogspot.com/2013/04/getting-started-with-qutip-on-picloud.html) by Markus Baden about how to set up QuTiP on picloud. The second was the discovery of picloud itself. Last week I was finally starting to dive in to a project to wire up five servers into a mini-cluster and then this week I learn about massively scalable computing in the cloud for mere pennies ([picloud.com](http://www.picloud.com)).[
](http://dawes.files.wordpress.com/2013/04/logo.png)

[![PiCloud](http://dawes.files.wordpress.com/2013/04/logo.png?w=150)](http://dawes.files.wordpress.com/2013/04/logo.png)I haven't done a lot with it yet, but I know enough to realize that I'll have to find another role for these servers. I estimate that keeping them on all year will cost about $800 in electricity (not including the AC to cool them). For that I can have 16,000 core hours of computing power per year. My cluster would only have 20 cores total so I would have to run a full month of computing jobs (800 hours = 33 days). Picloud is such an obvious win that I don't even have to factor in the time I would spend maintaining my own cluster.
