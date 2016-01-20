---
author: adawes
comments: true
date: 2011-01-09 04:11:25+00:00
layout: post
slug: computer-controlled-rgb-led-mixer
title: Computer controlled RGB LED mixer
wordpress_id: 448
categories:
- physics
tags:
- arduino
- led
---

http://www.youtube.com/watch?v=Xs87uY_nlYo

I've been working on some interactive color-mixing exhibits and pulled together a fun system using an [arduino](http://www.arduino.cc), [processing](http://www.processing.org) code, and computer control. The video above shows a demo of the mouse-controlled RGB color mixer. The idea was to create an interactive exploration of the color gamut (range of colors that can be created by mixing a given set of three colored lights). Code and more details are given below:
<!-- more -->

The color gamut is usually illustrated as in the following figure. I've reflected this to some degree in the code. Moving the mouse to the top of the control window gives green light, the bottom right corner is red, and bottom left corner is blue. There are non-trivial issues with mapping a curved triangle to a square; I've completely ignored these issues. In one sense, I've stretched and compressed the gamut as necessary to get it all to fit into a square on the control end. That said, this should be a pretty easy way to get any of the possible colors out of a set of three LEDs.

<span class="caption">, CC-BY-SA-3.0 (www.creativecommons.org/licenses/by-sa/3.0) or GFDL, via Wikimedia Commons"][![gamut](http://upload.wikimedia.org/wikipedia/commons/6/60/Cie_Chart_with_sRGB_gamut_by_spigget.png)](http://commons.wikimedia.org/wiki/File:Cie_Chart_with_sRGB_gamut_by_spigget.png)</span>



#### Hardware:


I used a [Sparkfun KIT-10111](http://www.sparkfun.com/products/10111) tri-LED breakout board. The Arduino provides power, serial in/out, and PWM control of the red/green/blue input pins on the 10111 board.



#### Code:


The code is given below, I learned most of it from examples and looking through the processing API. This is my first project to use processing, and I first found myself wishing I had done it in python... but in the end, processing has some very slick ways to take input and to draw stuff. Since that is 90% of what I had to do here, it turned out to be a good fit.

Processing code (this is the control "gui" for the project):
{% highlight cpp %}
/**
 * RGB LED control
 * AMC Dawes (dawes@pacificu.edu)
 * dawes.wordpress.com
 * Updated 8 January 2011
 */


// Use the included processing code serial library
import processing.serial.*;        

int winSize = 255;

Serial port;  // The serial port
String myString;
int redBright, grnBright, bluBright;

void setup()
{
  size(winSize, winSize);
  colorMode(RGB, 255);
  noStroke();
  ellipseMode(CENTER);
  frameRate(100);

  println(Serial.list()); // List COM-ports

  //select first com-port from the list
  port = new Serial(this, Serial.list()[0], 57600);
}

void draw()
{
  background(0.0);
  update(mouseX, mouseY);
  fill(redBright,grnBright,bluBright);
  background(0);
  ellipse(mouseX, mouseY, 20, 20);
  //while (port.available() > 0) {
    //myString = port.readStringUntil(lf);
    //if (myString != null) {
	//println(myString);  // Prints String
    //}
  //}
}

void update(int x, int y)
{
  redBright = x*y/255;
  grnBright = -y+255;
  bluBright = (-x+255)*y/255;

  //Output the led brightness ( from 0 to 255)
  port.write(0x73); // Send control character (ASCII 's')
  port.write(redBright);
  port.write(grnBright);
  port.write(bluBright);
}
{% endhighlight %}

Load the following code onto your Arduino. You can test it with the serial monitor (be sure to set the baud rate correctly). Try sending control sequences like "saaa" or "s~~~" or "s!!!". The Arduino waits for an "s" (0x73) to indicate a control sequence. The next three bytes are red, green, and blue integers (0-255). The ASCII bytes associated with "a", "~" and "!" are 0x61, 0x7E, and 0x21 respectively. These are equivalent to decimal 97, 126, and 33. While these don't fill the 8-bit depth (decimal 0-255) they give you a good sense of being able to control the brightness. Of course, these examples would all have each LED light up by an equal amount (approximately). To make mostly red light up send: "s~!!". This would be approximately RGB (126,33,33) or for web designers out there #7E2121. The mouse interface in processing writes decimal integers between 0 and 255 to each LED so you should see one LED go dark as the mouse reaches the edge of the black window.

The hardest part was debugging the processing code to make sure it was sending the right thing to the Arduino. It has been a while since I've used C++ for any byte-level stuff. A serial LCD helped a bit, but mostly is was old-fashioned trial and error. Overall the project took about two hours to hash through (not counting assembly time for the LED kit, which was ~ 1/2 hour). Enjoy, and as always, your comments and suggestions are greatly appreciated.

Arduino code:
{% highlight cpp %}
/*
RGB color gamut (mouse control)

 The circuit:
 Sparkfun Three LED breakout board KIT-10111
 * RED on Arduino pin 9
 * GRN on Arduino pin 10
 * BLU on Arduino pin 11

 AMC Dawes (dawes@pacificu.edu)
 dawes.wordpress.com
 Created 4 Jan 2011
 Based on sample code "Fading" By David A. Mellis

 */


int redPin = 9;
int grnPin = 10;
int bluPin = 11;

int startbyte;
int userInput[3];
int i;
int red = 0;
int green = 0;
int blue = 0;

void setup()  {
  Serial.begin(57600); // initialize serial connection
}

void loop()  {
  if (Serial.available() > 3) {
    // Read the first byte
    startbyte = Serial.read();
    // If it's really the startbyte (0x73 or ASCII "s") ...
    if (startbyte == 0x73) {
      // ... then get the next three bytes
      for (i=0;i<3;i++) {
        userInput[i] = Serial.read();
        //if (userInput[i] == ) {break;} // just in case
      }
      // First byte = red
      red = userInput[0];
      // Second byte = green
      green = userInput[1];
      // Third byte = blue
      blue = userInput[2];
    }
    analogWrite(redPin, red % 255); // mod 255 just in case
    analogWrite(grnPin, green % 255);
    analogWrite(bluPin, blue % 255);
    // some serial output for debugging:
    Serial.print("red: ");
    Serial.println(red);
    Serial.print("green: ");
    Serial.println(green);
    Serial.print("blue: ");
    Serial.println(blue);
    Serial.println("------------");
  }   
}
{% endhighlight %}
