---
author: adawes
comments: true
date: 2007-12-03 13:54:28+00:00
layout: post
slug: writing-pngs-from-c
title: Writing PNGs from C++
wordpress_id: 93
categories:
- computing
- open source software
tags:
- array
- c++
- matlab
- png
---

![hexagons](http://dawes.files.wordpress.com/2007/12/hexagons.png)To continue the series on using [C++ to replace MATLAB](http://dawes.wordpress.com/2007/10/30/matlab-cc/), here are some details about using the [pngwriter](http://pngwriter.sourceforge.net/) library. Included below is a function that I use in various places to write a 2D array to a png file. This can be left in a header somewhere and used in a similar way to MATLAB's `imagesc()` function.





I'd be happy to post more details if anyone is interested, and I'll try to keep up with posts about the process I followed to port from MATLAB to C++.




<!-- more -->



Assume the array `field` is square with `size` by `size` elements. There is a peak-finding routine used to normalize the color map, and I call `png.plot_text` to write the value of `max` in the image:



`

    
    
      void array_to_png (char* filename, int size, array2 &field)
      {
        char text[30];
        int i,j;
        double pixel;
        pngwriter png(size,size,0,filename);
        // Peak-finding for image scaling:
        double max = 1e-32; 
        for (i = 0; i < size; i++)
        {
          for (j = 0; j  max) max = real(field(i,j)*conj(field(i,j)));
          }
        }
    
        // Image writeout.
        for (i = 0; i < size; i++)
        {
          for (j = 0; j < size; j++)
          {
            pixel = real(field(i,j)*conj(field(i,j)));
            png.plot(i,j,pixel/max,pixel/max,0.0);
          }
        }
    
        sprintf(text, "%f7", max);
        png.plot_text("/xtmp/dawes/share/pngwriter/fonts/FreeMonoBold.ttf",10,10,10,0.0,text,1.0,1.0,1.0);
        png.close();
      }
    


`



The only other detail is that this image will be yellow because I've passed equal values to the R and G parameters (B=0) in the call to `png.plot()`.
