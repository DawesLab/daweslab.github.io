---
author: adawes
comments: true
date: 2011-01-02 16:48:02+00:00
layout: post
slug: scientific-python
title: Scientific Python
wordpress_id: 355
categories:
- computing
- experiments
- open source software
- physics
- python
- try this at home
tags:
- enthought
- numpy
- python
- scipy
---

[![](http://dawes.files.wordpress.com/2010/07/screen-shot-2010-07-27-at-7-18-00-am.png)](http://dawes.files.wordpress.com/2010/07/screen-shot-2010-07-27-at-7-18-00-am.png)I have been using python more and more in my scientific work. This has been enabled by several excellent resources. The most important resource is the [Enthought Python Distribution](http://www.enthought.com) (EPD). The EPD makes it trivially easy to have a complete python installation that includes many scientific packages. Best of all, the EPD is available for free under an Academic license. All software included in the EPD is open-source so it is straightforward to install an equivalent set of packages; the only difference is convenience. Enthought also offers many tutorials, webinars, and other support resources for scientific python.

Here, I have put together some of my favorite resources, along with a brief presentation that illustrates the power of SciPy/Numpy through several examples based on my own various projects.

<!-- more -->

These resources are also available at my [python resources page](http://newton.ns.pacificu.edu/~dawes/python). The examples that can be found at the end of this post and in my presentation:




  * import data and plot two columns as x and y


  * fit data with an arbitrary function


  * extract relative intensity data from an image


  * propagate uncertainties in formula evaluation


The last example requires software that is not available in the EPD, but it is very easy to install. The [python uncertainties](http://pypi.python.org/pypi/uncertainties/) package is a great tool for propagating error when evaluating formulas using numbers with uncertainty. There are formulas for this and I'm sure some calculators can do it, but this package has a great interface and makes error propagation something to stop fearing.

I have helped several students get started using python (SciPy in particular) and each of them have commented positively on how easy it is to learn and to keep using. I'll have a few python projects that I will post here as they mature. In the meantime, enjoy these links and happy coding.


### Import data and plot


{% highlight python %}
from scipy import loadtxt
from pylab import figure, plot, title, xlabel, ylabel, show

data = loadtxt("TEK0006.CSV", delimiter=",", usecols=(3,4))

time = data[:,0] # 0th column is time data
voltage = data[:,1] # 1st column is voltage data

transmission = voltage/max(voltage)

fig = figure()

plot(time,transmission)

title("Cold Rb-87 Spectrum, F=2->F'")
xlabel("Time (s)")
ylabel("Transmission (Arb. Units)")
show()
 {% endhighlight %}

This code loads columns 3 and 4 (zero indexed) from a csv file. In this case it is a file saved by a Tektronix scope (TEK0006.CSV). The time and voltage data are named to make calculations more transparent. Finally, the voltage is scaled to its own max. In this case, the signal is a spectroscopic transmission so to convert to transmission, we just scale to the max and call that 1 (full transmission). Finally, we plot with some labels and a title.


### Fit with arbitrary function


{% highlight python %}
from numpy import linspace, exp, random
from pylab import plot, show
from scipy.optimize import curve_fit

def func(x, a, b, c):
	return a * exp(-b*x) + c

x = linspace(0.0, 4.0, 50) # 50 points from 0 to 4)
y = func(x, 2.2, 1.7, -0.5)
yn = y + 0.2*random.normal(size=len(x))

[a, b, c], covar = curve_fit(func, x, yn)

print "a = ", a, " var_a = ", covar[0,0]
print "b = ", b, " var_b = ", covar[1,1]
print "c = ", c, " var_c = ", covar[2,2]
plot(x, yn)
plot(x, func(x, *[a,b,c]), '-k')
show()
{% endhighlight %}

First, define a function with some variables (a, b, c). As a demo, we have to generate some data, so we take the function and add some random noise. In an experimental situation, you could import data as in the prior example, and play with fitting against the actual data. Finally, output the covar elements from curve_fit to find the uncertainty in the three fit parameters. Students love this since usually the do curve fitting in excel and then complain that they don't know the uncertainty in the fit. "Use better tools" I say, and here is one that's easy to use.


### Extract image intensity


{% highlight python %}
from pylab import imshow, figure, zeros, plot
from scipy.misc import imread
from scipy.ndimage.interpolation import rotate
from numpy import savetxt

a = imread("Jefferson.JPG",flatten=1)
# imshow(a)

center = [1930,1289] # define the center of the image (for cropping)
width = 1000 # choose a radius for the cropped image

crop = a[center[0]-width:center[0]+width,center[1]-width:center[1]+width]
# imshow(crop)

stack = zeros((2000,10)) # create an array to save the slices
total = stack[:,0] # create an array to save the average slice

for i in range(10): # take ten slices
	stack[:,i] = rotate(crop,i*36,reshape=False)[1000,:]
	total += stack[:,i]

plot(total) # plot the data
savetxt("Jefferson-v2.dat", total) # save the data to a file
{% endhighlight %}

<span class="caption">](http://dawes.files.wordpress.com/2011/01/jefferson.jpg)</span>

This example isn't as obvious but it was a great example of how easy it can be to code something to do a quick data analysis. I had a student working on Kirlian Photography (I'll save that discussion for a later post) by imaging the corona around electrified objects. In this case, the object was a dime and we wanted to know how the corona brightness depended on distance from the edge of the dime.

<span class="caption">](http://dawes.files.wordpress.com/2011/01/screen-shot-2011-01-02-at-9-40-52-am.png)</span>

We wanted to model the effect so we needed something to compare to our models. Python imports the image using the imread function. Then we assign a center and crop the image to make it square. Finally, to build up a bunch of cross sections, we start taking slices and then rotating the image and take another slice. The slices are then averaged to give a nice smooth curve describing the corona brightness as a function of radius.


###




### Propagate errors (uncertainty)


{% highlight python %}
from uncertainties import ufloat
from uncertainties.umath import *

# Calculate number of photons per pulse
#      P * tau
# N = ---------
#         E
#
# Where P -> power, tau -> pulse duration, E -> photon energy

tau = ufloat("3.2e-6+/-0.2e-6")
# in seconds
wavelambda = ufloat("780+/-0.25")
# in nanometers (note, "lambda" is a special word in python)
P = ufloat("3.2e-9+/-0.5e-9")
# in watts

# photon energy is hc/lambda, hc = 1240 eV*nm or 1.986e-16 J*nm

N = (P * tau)/(1.986e-16/wavelambda)

print N
{% endhighlight %}



This example is fairly straightforward. The uncertainty package has several ways to specify a number and the error. I like the +/- text way since it is easy to read. Calculations simply "do the right thing" when you define the numbers as ufloat (floats with associated uncertainty).
