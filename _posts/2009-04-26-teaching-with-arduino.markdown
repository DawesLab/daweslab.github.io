---
author: adawes
comments: true
date: 2009-04-26 02:55:26+00:00
layout: post
slug: teaching-with-arduino
title: Teaching with Arduino
wordpress_id: 199
categories:
- computing
- open source software
- physics
- teaching
- try this at home
tags:
- arduino
- demo
- teaching
---

![arduino](http://dawes.files.wordpress.com/2009/04/arduino316.jpg?w=300)

I've decided to use the Arduino in my electronics class this fall. The Arduino is an "open-source electronics prototyping platform based on flexible, easy-to-use hardware and software." Even from the description it sounds like just what an electronics course needs. I finally had some time to tinker with it today, and after a few minutes I had it's LED [blinking](http://www.ladyada.net/learn/arduino/lesson1.html) away, and then after another few minutes it was an [oscilloscope](http://accrochages.drone.ws/en/node/90). A few minutes later it was playing a pulse-width-modulated (PWM) [melody](http://www.arduino.cc/en/Tutorial/Melody). Not bad for an hour's work.

With a little inspiration, and my new-found confidence, I took to my first project in hopes of having a little demo to show the intro students to recruit them for my class in the fall. An hour and a half later (including fielding questions about homework and our exam tomorrow) I had a photo-resistor theramin up and running. <!-- more -->The basic idea is to use a photoresistor as half of a voltage divider and tell the Arduino to read the voltage and output a PWM tone whose frequency depends on the voltage. This way the pitch can be controlled by blocking or unblocking the light at the photoresistor.

    
    int speakerOut = 9;
    
    void setup() {
      pinMode(speakerOut, OUTPUT);
    }
    
    int tone = 0;
    long input = 0;
    int maximum = 500;
    int minimum = 400;
    float range = 100;
    
    void loop() {
        input = analogRead(0);
        if (input > maximum) maximum = input;
        if (input < minimum) minimum = input;
        range = maximum-minimum;
        tone = 9090*float(1-float((input-minimum)/range));
        //tone is the period, so large means high frequency.
        // when using analogRead, this means a high voltage gives a low sound.
    
        digitalWrite(speakerOut,HIGH);
        delayMicroseconds(tone / 2);
    
        // DOWN
        digitalWrite(speakerOut, LOW);
        delayMicroseconds(tone / 2);
    }


Enjoy!
