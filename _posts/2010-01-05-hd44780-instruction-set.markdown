---
author: adawes
comments: true
date: 2010-01-05 12:51:28+00:00
layout: post
slug: hd44780-instruction-set
title: HD44780 Instruction Set
wordpress_id: 297
categories:
- computing
- electronics
- try this at home
tags:
- HD44780 lcd controller serial sparkfun
---

[![](http://dawes.files.wordpress.com/2009/12/serlcd.jpg?w=150)](http://dawes.files.wordpress.com/2009/12/serlcd.jpg)There are a lot of LCD modules that use the HD44780 controller. This is a chip that accepts parallel data (8 bits) to control an LCD character display. In my recent [twitter2LCD](http://dawes.wordpress.com/2009/12/23/twitter-to-lcd/) project I needed to determine some of the control instructions such as how to make text scroll and how to control the position of the cursor. There are quite a few places where the complete instruction set is posted, but they are geared more toward seasoned digital electronics users. The main insight I can offer is that if you are using a serial-enabled LCD (as I was), you have to convert the 8 control bits into a byte and send that byte after a specific control character. For the Sparkfun LCD-09393 and related SerLCD modules, the control byte is "0xFE." This byte grabs the attention of the onboard controller and tells it that the following byte is an instruction and not a character.<!-- more -->The basic instructions can be determined from the following table.

<span class="caption">](http://dawes.files.wordpress.com/2010/01/picture-1.png)</span>

The various bit values have specific meanings outlined in the following figure.

<span class="caption">](http://dawes.files.wordpress.com/2010/01/hd44780-bit-meaning.png)</span>

The trick is then to read the DB0 throught DB7 bits as a byte where the LSB is DB0. For example, to clear the display I would send binary "00000001" or hex: 0x01. This is the documented clear byte in the Sparkfun SerLCD datasheet. Some other examples are included in that datasheet, but the following is a table of all HD44780 control combinations.
<table style="clear:both;" >
<tbody >
<tr >
Instruction
Byte
</tr>
<tr >

<td >Clear display
</td>

<td >0x01
</td>
</tr>
<tr >

<td >Return cursor to home, and un-shift display
</td>

<td >0x02
</td>
</tr>
<tr >

<td >Entry mode: The following control how the cursor behaves after each character is entered
</td>

<td >
</td>
</tr>
<tr >

<td >move cursor right, don't shift display
</td>

<td >0x04
</td>
</tr>
<tr >

<td >move cursor right, do shift display (left)
</td>

<td >0x05
</td>
</tr>
<tr >

<td >move cursor right, don't shift display (this is the most common)
</td>

<td >0x06
</td>
</tr>
<tr >

<td >move cursor right, do shift display (left)
</td>

<td >0x07
</td>
</tr>
<tr >

<td >Display control: The following control display properties
</td>

<td >
</td>
</tr>
<tr >

<td >turn display off
</td>

<td >0x08
...
0x0B
</td>
</tr>
<tr >

<td >display on, cursor off,
</td>

<td >0x0C
</td>
</tr>
<tr >

<td >display on, cursor on, steady cursor
</td>

<td >0x0E
</td>
</tr>
<tr >

<td >display on, cursor on, blinking cursor
</td>

<td >0x0F
</td>
</tr>
<tr >

<td >The following commands move the cursor and shift the display
</td>

<td >
</td>
</tr>
<tr >

<td >Shift cursor left
</td>

<td >0x10
</td>
</tr>
<tr >

<td >Shift cursor right
</td>

<td >0x14
</td>
</tr>
<tr >

<td >Shift display left
</td>

<td >0x18
</td>
</tr>
<tr >

<td >Shift display right
</td>

<td >0x1C
</td>
</tr>
<tr >

<td >Function set: the following commands set functions of the controller.
</td>

<td >
</td>
</tr>
<tr >

<td >These are more advanced and with a serial controller, you won't need to mess with them. If you do have to change these, follow the recipe of creating a byte from the bits shown in the table above.
</td>

<td >
</td>
</tr>
<tr >

<td >Cursor position: see following discussion for more detail.
</td>

<td >0x80 + position
</td>
</tr>
</tbody>
</table>
The cursor position can seem like black magic but it makes much more sense once you know that the HD44780 is designed to control a 40 character 4-line display. So if you have a 16x2 then you will only see the first 16 characters of the top two lines. Simple enough once you get used to taking these character positions into account. For example, in a 16x2 display, the first line is position 0-15. So 0x80 is the first position, 0x80 + 12 = 0x8C is the 13th (remember, they are zero indexed). The second line is a little tricky since it shows positions 64-79. Just add the position number (in decimal) to 0x80 (in hex) to get the hex address of the cursor position. The address is the command to move the cursor to that location. So, to move to the 13th position of the top line in a 16x2 Sparkfun Display, I would send "0xFE 0x8C". The first byte warns the onboard microcontroller that a command is coming, and the second byte is the command.
