---
id: 136
title: How HEX colors work
date: 2015-02-09T12:59:14+00:00
author: Gjermund Bjaanes
layout: post
permalink: /how-hex-colors-work/
dsq_thread_id:
  - 3499178281
categories:
  - CodeProject
  - Uncategorized
tags:
  - CSS
  - Programming
  - Web
---
Have you ever wondered what all those numbers and letters in a hex color means? 

What color is #AA3939 or #888888 and why is that combination giving the color that it gives? 

Well, it’s not magic, nor is it randomly picked values that correspond to colors. 

<!--more-->

It's actually a pretty simple and logical system. The only thing you have to really learn is how the hexadecimal number system work.

&nbsp;

# Number system

Hex is actually a number system, much like our normal decimal system. The difference is the **base** the system is based upon. Our normal number system is base 10. Hexadecimal is base 16. What that really means is what each position in a number is worth.

Each positions number worth is calculated with this formula:

$$number \times base^{(position-1)}$$

&nbsp;

## Base 10 (Our normal decimal system):

_Example:_

The number: $$123$$

&nbsp;

We always start from the right and go left. So the first position is worth

$$3 \times 10^0 = 3$$

&nbsp;

The second position is

$$2 \times 10^1 = 20$$

&nbsp;

The third position is then worth

$$1 \times 10^2 = 100$$

&nbsp;

Then you add the all up together:

$$3+20+100=123$$

&nbsp;

Easy as that.

&nbsp;

[<img class="alignnone size-full wp-image-157" src="http://gjermundbjaanes.com/wp-content/uploads/2015/02/1231.png" alt="123" width="456" height="220" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/1231.png 456w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/1231-300x145.png 300w" sizes="(max-width: 456px) 100vw, 456px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/02/1231.png)

## Base 16 (Hex):

_Example:_

The base 16 (hex) number $$B2C$$
  
You might have noticed that hex has letters and number in them. That is because they go from 0-15, and it would very difficult to make sense out of which number goes into which position. So we have 0-9 and then A=10, B=11 all the way up to F=15.
  
Again we start from right to left. First number is now worth

$$12 \times 16^0 = 12$$

&nbsp;

The second number is

$$2 \times 16^1 = 32$$

&nbsp;

The third number is

$$11 \times 16^2 = 2816$$

&nbsp;

The total number shown in our decimal system is then calculated by adding the numbers together:

$$12+32+2816=2860$$

&nbsp;

[<img class="alignnone size-full wp-image-159" src="http://gjermundbjaanes.com/wp-content/uploads/2015/02/b2c.png" alt="b2c" width="456" height="220" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/b2c.png 456w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/b2c-300x145.png 300w" sizes="(max-width: 456px) 100vw, 456px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/02/b2c.png)

# Making sense of the numbers

A hex color is made up of three parts that represent the amount of Red, Green and Blue that are mixed together. These are split up using the first and second number for red, third and fourth number for green and fifth and sixth number for blue.

&nbsp;

[<img class="alignnone size-full wp-image-137" src="http://gjermundbjaanes.com/wp-content/uploads/2015/02/hexcolor.png" alt="hexcolor" width="640" height="220" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/hexcolor.png 640w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/hexcolor-300x103.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/hexcolor-600x206.png 600w" sizes="(max-width: 640px) 100vw, 640px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/02/hexcolor.png)

&nbsp;

Armed with this knowledge, you can now specify the amount of red, green and blue in a color. Since there are two hex numbers for each color, you can have 0 amount of a color (00), all the way up to 255 (FF). Using this system, we can specify a large number of different colors, using the amount of red, green and blue (255\*255\*255=16 581 375 - to be exact).

_Examples:_
  
**White** is made when mixing the maximum number of red, green and blue together, so it will be #FFFFFF.

**Black** is when there are no amount of any of the colors. #000000

**Shades of grey** can be done like this: #111111 (very dark grey - almost black). #CCCCCC (very light grey)

&nbsp;

# How 3 digit HEX works

Sometimes people like to use a shorthand HEX for some colors with only 3 digits. The way this works is that each digit is representing their color (red, green, blue), but when you write #F00, this is actually the same as #FF0000. So its a shortcut for when you need some special colors like red, green, blue, black, white and grey scales.

_Examples:_
  
**Black**: #000 (#000000)

**White**: #FFF (#FFFFFF)

**Grey**: #888 (#888888)