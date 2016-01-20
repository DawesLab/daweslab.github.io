---
author: adawes
comments: true
date: 2010-06-08 14:12:50+00:00
layout: post
slug: basic-image-analysis-python
title: Basic image analysis in Python
wordpress_id: 324
categories:
- computing
- experiments
- physics
- python
- teaching
tags:
- image analysis
- kirlian photography
- laplace
- python
- scipy
---

<span class="caption">](http://dawes.files.wordpress.com/2010/06/jefferson_small_crop.jpg)</span>I always like to have a response ready for those times that people inevitably ask "why do you use Python in your research, don't you know c or Fortran?" I always like that question. "Yes, I know c and Fortran, and I know how painful and slow it can be to code and debug c and Fortran." Another prime example came to life over this past semester. I was working with a student on a senior capstone project and he was looking at images of the corona discharge around various metal objects. We wanted to analyze the images and map the brightness to the relevant physics (i.e., the electric field surrounding the object).
<!-- more -->


Our analysis task was to import images (JPG format), extract numerical data (pixel brightness), and compare to various theories. While I'm sure there are straightforward ways to do this in other languages, I found Python had more than enough to offer in terms of possible solutions. One additional requirement was that we wanted to average many slices of the image in order to decrease the sensitivity to localized variations. The final solution was to import the image using tools provided by [Scipy](http://www.scipy.org). This also allowed us to use standard image processing functions to rotate the image and average many cross sections. Because the object (a nickel) has rotational symmetry, we took 36 slices (each 10 degrees from the previous) and averaged them. This gives a good picture of the radial dependence of the brightness. Plotting and fitting were straightforward using other Scipy routines or your favorite 2D plotting software (mine is [DataGraph](http://www.visualdatatools.com/DataGraph/index.html)).

Writing and debugging the code took about an hour and plotting/analyzing took about another hour. Two hours start to finish!

We quickly realized that we don't have an analytic theory to compare to so we discussed various numerical models and decided to implement a relaxation method to solve the Laplace equation in 3D for a reasonable set of boundary conditions. This code took about 1.5 hours and depending on the mesh density, runs in about 3 minutes. Best of all, we get very interesting qualitative agreement. All this for about 4 hours at the computer. Not too shabby.

For what it's worth, the code is attached below. The relevant functions are scipy.misc.imread, pylab.imshow, pylab.semilogy, and scipy.sum. These import an image, show an image, plot on semilog axis, and sum an array along one axis. The code comments should help illustrate why each is used.

Image analysis:

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

Relaxation method:

{% highlight python %}
from scipy.misc import imread
from pylab import gray, imshow, plot, show, semilogy
from scipy import zeros, sum

image = imread("circle.png",flatten=True)
image = -image + 255 # rescale so background is zero

sizex,sizey = image.shape
depth = 15

mesh = zeros((sizex,sizey,depth))

mesh[:,:,0] = image
mesh[:,:,1] = image
mesh[:,:,2] = image
mesh[:,:,3] = image
mesh[:,:,4] = image

runs = 500
# iterate over the whole array setting each point to be
# the average of the neighbors
for round in range(runs):
     print "Run number: ", round
     for i in range(sizex-2):
          for j in range(sizey-2):
               for k in range(depth-2):
                    mesh[i+1,j+1,k+1] = 0.166 * (mesh[i+1,j+1,k] + mesh[i+1,j+1,k+2] + mesh[i+1,j,k+1] + mesh[i+1,j+2,k+1] + mesh[i,j+1,k+1] + mesh[i+2,j+1,k+1])

total = sum(mesh, axis=2) # Sum the potential through the whole region. This was to see if the light generated is proportional to the potential. It is more likely that the light is proportional to the field strength so more calculation will be required.
semilogy(total[:,sizex/2]) # plot a slice through the center of the region
{% endhighlight %}

I should point out that one interesting feature of this code is that is uses an image to provide the initial conditions for the Laplace solver. This means that the code could be easily adapted to a wide variety of situations and you could quickly explore all sorts of funky shapes.

The top five slices are set to have the potential given in a grayscale image. I just created a black circle on a white background in Inkscape and exported it to PNG. The code inverts this image in order to set the voltage to 255 in the center and 0 on the outside. Then there is a little trick to zero (ground) the areas outside the circle. From there, it's just a for loop that carries out the relaxation method: set each point to the average of the neighbors.

This project isn't necessarily polished, but I wanted to share the code in case anyone is looking for something like this. If you have to extract some data from an image, python is a great place to start.
