---
author: adawes
comments: true
date: 2007-11-27 02:16:40+00:00
layout: post
slug: matlab-c-part-ii
title: MATLAB → C++ part II
wordpress_id: 82
categories:
- computing
- physics
tags:
- c++
- convert
- fftshift
- matlab
- porting
---

[![Matlab](http://dawes.files.wordpress.com/2007/11/matlab-100square.png)](http://dawes.wordpress.com/category/computing/)

I have had some success with converting my MATLAB code to C++. There are some caveats, from array indexing (minor), to missing functions (less trivial to fix). In case people are looking for solutions to these problems, I've posted some sample code.




To motivate the conversion a little bit more, my code spends 99% of its time computing FFTs. I initially found that FFT benchmarks in MATLAB were comparable to C++, which can be explained by the fact that MATLAB calls FFTW libraries which are well optimized. However, I wasn't using a well-optimized array implementation so the real improvement came when I found John Bowman's [fftw++ headers and Array class](http://www.math.ualberta.ca/~bowman/Array). In the end, re-writing my code with these data structures results in a 2-4x speedup over MATLAB. The additional advantage is that a portion of my simulation is embarrassingly parallel so C++ makes it easy to exploit that.




<!-- more -->



Now, on to the tips and tricks. Re-indexing arrays is a simple matter, just remember MATLAB is 1 to N and C++ is 0 to N-1 for arrays of N elements. You'll get used to nested _for_ loops, and the code isn't as compact as MATLAB's `array1(:,:) = 5*array2(:,:,5)` etc, but just match your index and you're set.




I was sorely missing the fftshift function but came up with the following workaround. More background: I have an operator, called expDz, that has to be applied in Fourier space. I can easily compute it in regular coordinates but the Fast Fourier Transform works in a shifted space where the DC component is the first element, and the N/2...N components are the negative frequencies. One dimensional arrays are pretty trivial to deal with, but when you're working with spatial transforms on 2D data, these ideas aren't as intuitive. What I did to get expDz to be properly aligned in Fourier space is the following in MATLAB:



`

    
    
      grid = (-N/2:N/2-1); % set up the numerical grid
      xstep = 6*w0/N; % spatial frequency in x
      ystep = xstep;
      Kxstep=2*pi/(N*xstep); % spatial K-vector steps
      Kystep=2*pi/(N*ystep);
      [kx ky]=meshgrid(fftshift(Kxstep*grid),fftshift(Kystep*grid)); 
      % shift everyone to build the meshgrid in Fourier space.
      theta_n = zstep/(2*sigma).*(kx.^2+ky.^2); 
      % arg to be put in Exp function
      exp_Dz = exp(-i*theta_n); % it's a one-liner
    


`



Which in C++ becomes:



`

    
    
    for (i = 0; i < N; i++){
      for (j = 0; j < N; j++){
        if (i < N/2 && j < N/2){
          expDz(i,j) = exp(-I*(zstep/(2*sigma)*(((i)*kxstep*(i)*kxstep) 
                           + ((j)*kystep*(j)*kystep))));
        } else if (i < N/2 && j >= N/2){
          expDz(i,j) = exp(-I*(zstep/(2*sigma)*(((i)*kxstep*(i)*kxstep) 
                           + ((j-N)*kystep*(j-N)*kystep))));
        } else if (i >= N/2 && j < N/2){
          expDz(i,j) = exp(-I*(zstep/(2*sigma)*(((i-N)*kxstep*(i-N)*kxstep) 
                           + ((j)*kystep*(j)*kystep))));
        } else if (i >= N/2 && j >= N/2){
          expDz(i,j) = exp(-I*(zstep/(2*sigma)*(((i-N)*kxstep*(i-N)*kxstep) 
                           + ((j-N)*kystep*(j-N)*kystep))));
        } else {
          cerr << "ERROR: could not properly determine the propagator" << endl;
        }
      }
    }
    


`


In short, I just calculate each quadrant of expDz individually by wrapping one or both index by N.The algorithm being used here is the split-step beam propagation method, which explains the need for doing math in the fourier domain. In general this approach works as a replacement for fftshift, and I plan to write a small header file with a C function that performs this.
