---
author: adawes
comments: true
date: 2009-12-23 13:44:43+00:00
layout: post
slug: twitter-to-lcd
title: Twitter to LCD - with scrolling text
wordpress_id: 276
categories:
- computing
- open source software
- python
- try this at home
tags:
- arduino
- electronics
- HD44780
- LCD
- page
- python
- scroll
- sparkfun
---

[![](http://dawes.files.wordpress.com/2009/12/serlcd.jpg?w=150)](http://www.sparkfun.com/commerce/product_info.php?products_id=9393)I've been having some fun with a [Sparkfun](http://www.sparkfun.com) Serial-enabled LCD screen ([LCD-09393](http://www.sparkfun.com/commerce/product_info.php?products_id=9393), $24.95). This little package will write out whatever you send along a serial data line. So this means you can add an LCD to a project with only three wires:  +V, GND, and RX (serial receive). In the real world, I'm hoping to use these LCDs in some lab instruments that we'll be building in the spring semester. In particular, I'm looking at an [arduino](http://www.arduino.cc)-based [frequency counter](http://interface.khm.de/index.php/lab/experiments/arduino-frequency-counter-library/). I also want to explore an arduino-based PID controller for various lab projects (temp. control, etc.).

My first test, however, was just getting the LCD to work. And then, I wanted to make it show my Twitter status. I've been using twitter ([DrDawes](http://www.twitter.com/drdawes)) to post my office status and give students updates as to where I am or when I may be around again. This has been helpful since my research lab is in another building and I tend to be available but it may not look like it since I'm not in the physics building. This way if I want to step over to the lab, I can simply send an update, and save people the trouble of tracking me down. The rub is that not everyone has twitter, and sometimes people just come to my office anyway. That said, my goal is to post a 16x2 LCD screen on my door so that my availability status (formerly written on a whiteboard, or post-it) can be more 21st century.

<!-- more -->As of this weekend, the whole system is working, although not yet installed. I'm running an Arduino as the LCD controller, but really it's just reading serial from the computer and writing serial to the LCD, so I'm sure there is a more efficient way (I'll work on that for v2.0). The arduino code is given below:

{% highlight python %}

#include <SoftwareSerial.h>

#define txPin 2

int incomingByte = 0;    // for incoming serial data

SoftwareSerial LCD = SoftwareSerial(0, txPin);
// since the LCD does not send data back to the Arduino, we should only define the txPin

void setup()
{
 Serial.begin(9600);
 pinMode(txPin, OUTPUT);
 LCD.begin(9600);
}

void loop()
{
 if (Serial.available() > 0) {
 // read the incoming byte:
 incomingByte = Serial.read();
 LCD.print(incomingByte,BYTE);
 }
}

{% endhighlight %}

I like [python](http://www.python.org), so I used it for the computer end of the project. The only things I had to figure out were how to write hex bytes to the serial port, and how the LCD memory was laid out. I wanted it to be a bit fancier than stock so I wrote two functions, one that scrolls the text across the LCD and one that pages it up line by line. This is necessary since twitter runs up to 140 characters and I can only show 32 on the LCD (at a time).

{% highlight python %}
#!/usr/bin/env python
# encoding: utf-8
"""
TweetLCD.py

This twitter-to-LCD script implements two functions for displaying
text on a Sparkfun Serial LCD.

 scrollText - allows long lines of text to be scrolled along the top of the LCD
 pageText - allows long text to be paged up. First the top line is written, then
            the bottom line, then the lines shift up, and more text is
            written on the bottom line.

Created by Andrew M.C. Dawes on 2009-12-18.
Copyright (c) 2009 Andrew M.C. Dawes.
Some rights reserved. License: Creative Commons GNU GPL:
http://creativecommons.org/licenses/GPL/2.0/
"""

import serial, time, sys, twitter
SERIALPORT = "/dev/tty.usbserial-A6008cAP" # this is my USB serial port YMMV

def pageText(textstring, s):
    botline = ""
    cursor = 0
    for letter in textstring:
        # print letter, cursor   # this is for debugging
        s.write(letter)

        if cursor > 15:
            # I'm printing in second line so keep track of what I write
            botline = botline + letter
            # print botline

        if cursor == 31: # page the bottom line up to top, clear bottom, and write
            # print "cursor wrap"
            s.write('\xFE\x80') # wrap to start of first line
            s.write(botline) # write what was on the bottom (now on top)
            s.write("                ")
            s.write('\xFE\xC0') # skip to beginning of second line
            botline = ""
            cursor = 15 # reset to beginning of second line

        cursor = cursor + 1

        time.sleep(0.15) # set this delay to a comfortable value

def scrollText(textstring, s):
    nextstring = ""
    cursor = 0
    firstpass = True # test whether this is the first 16 characters
    for letter in textstring:
        if firstpass == False:
            s.write('\xFE\x18') # scroll left one spot at each letter

        # print letter, cursor  # this is for debugging
        s.write(letter)

        if cursor == 15:
            # I'm printing the last visible character
            s.write('\xFE\x90') # jump cursor to 2nd column of 16
            firstpass = False # once the first row is filled, we need to scroll

        if cursor == 31:
            s.write('\xFE\xA0') # jump cursor to 3rd column

        if cursor == 39:
            cursor = -1 # start over, there are only 40 characters in memory
            s.write('\xFE\x80') # this is the original character address.

        cursor = cursor + 1

        time.sleep(0.2) # adjust this to a comfortable value

def main():
    s = serial.Serial(SERIALPORT, 9600)
    time.sleep(2)
    s.write('\xFE\x01') # clear the LCD screen
    while(True):
        time.sleep(1)
        s.write('\xFE\x80') # goto 0 position
        api = twitter.Api()
        status = api.GetUserTimeline(user='DrDawes',count=1)[0]
        # textstring = "1111111111111111222222222222222233333333333333334444444444444444"
        textstring = "DrDawes@twitter: " + status.text
        scrollText(textstring,s) # choose one of these
        # pageText(textstring,s) # two options
        time.sleep(2)
        s.write('\xFE\x01') # clear the screen (in preparation to repeat)

    s.close()

if __name__ == '__main__':
    main()
{% endhighlight %}

You can see the two functions scrollText() and pageText() are responsible for cursor control and text movement. I'm still not sure which one I like better, but feel free to use these if you want them. The strange characters are pythons way of sending hex bytes as strings. The LCD uses the standard HD44780 controller, so there are special commands for controlling the LCD. For example, sending the string "\xFE\x01" in python sends two hex bytes: 0xFE and then 0x01. This happens to be the command to clear the LCD screen. The cursor motion is controlled in a similar way, with address locations following the \xFE byte. 0x80 is the first position so I send \xFE\x80 to move the cursor there. Similarly, \x90 is the 17th horizontal position in the top line, not viewable without scrolling and \xA0 is the 33rd position in the top line. There are 40 positions in each line (2 rows in my case) so the scrolling text function checks for this and wraps the cursor accordingly.

The other nifty command used in scrollText() is \x18 which scrolls the text to the left (the way we want to scroll in order to read it). You can see in the code that scrolling doesn't start until the first row is full of characters, once that happens it continues to scroll until all text has been shown. For scrolling, I take advantage of the fact that there are only 40 characters in memory and scrolling the screen has what I would call periodic boundary conditions (if you scroll past the end, you just get the beginning again). This makes it easy to write more than 40 characters to the display.

As part of my tinkering, I've also figured out a number of additional extended commands for the HD44780. Most of the useful ones are mentioned in the sparkfun datasheet, but there is a cryptic comment about many others existing. For an overview of additonal commands and a description of how to determine the others, see my [HD44780 instruction set](http://dawes.wordpress.com/2010/01/05/hd44780-instruction-set/) post.

[UPDATE: I replaced the Python code with properly indented code. Not sure what went wrong the first time, but let me know if you have issues.]
