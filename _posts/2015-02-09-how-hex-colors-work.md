---
id: 136
title: How HEX colors work
date: 2015-02-09T12:59:14+00:00
author: Gjermund Bjaanes
layout: post
guid: http://maximumdeveloper.com/?p=136
permalink: /how-hex-colors-work/
video_url:
  - 
audio_url:
  - 
quote_content:
  - 
quote_attribution:
  - 
link_url:
  - 
link_title:
  - 
dsq_thread_id:
  - 3499178281
suevafree_template:
  - right-sidebar
categories:
  - CodeProject
  - Uncategorized
tags:
  - CSS
  - Programming
  - Web
---
Have you ever wondered what all those numbers and letters in a hex color means? What color is #AA3939 or #888888 and why is that combination giving the color that it gives? Well, it’s not magic, and it’s not random either. It&#8217;s actually  a pretty simple system. The only thing you have to really learn is how the hexadecimal number system work.

&nbsp;

# Number system

Hex is actually a number system, much like our normal decimal system. The difference is the **base** the system is based upon. Our normal number system is base 10. Hexadecimal is base 16. What that really means is what each position in a number is worth.

Each positions number worth is calculated with this formula:


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3Enumber+%5Ctimes+base%5E%7B%28position-1%29%7D%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>number &#92;times base^{(position-1)}</p> <p>" title="</p> <p>number &#92;times base^{(position-1)}</p> <p>" class="latex" /> 

&nbsp;

## Base 10 (Our normal decimal system):

_Example:_


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E123%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>123</p> <p>" title="</p> <p>123</p> <p>" class="latex" /> 

&nbsp;

We always start from the right and go left. So the first position is worth


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E3+%5Ctimes+10%5E0+%3D+3.%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>3 &#92;times 10^0 = 3.</p> <p>" title="</p> <p>3 &#92;times 10^0 = 3.</p> <p>" class="latex" /> 

&nbsp;

The second position is


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E2+%5Ctimes+10%5E1+%3D+20%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>2 &#92;times 10^1 = 20</p> <p>" title="</p> <p>2 &#92;times 10^1 = 20</p> <p>" class="latex" /> 

&nbsp;

The third position is then worth


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E1+%5Ctimes+10%5E2+%3D+100%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>1 &#92;times 10^2 = 100</p> <p>" title="</p> <p>1 &#92;times 10^2 = 100</p> <p>" class="latex" /> 

&nbsp;

Then you add the all up together:


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E3%2B20%2B100%3D123.%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>3+20+100=123.</p> <p>" title="</p> <p>3+20+100=123.</p> <p>" class="latex" /> 

&nbsp;

Easy as that.

&nbsp;

[<img class="alignnone size-full wp-image-157" src="http://maximumdeveloper.com/wp-content/uploads/2015/02/1231.png" alt="123" width="456" height="220" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/1231.png 456w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/1231-300x145.png 300w" sizes="(max-width: 456px) 100vw, 456px" />](http://maximumdeveloper.com/wp-content/uploads/2015/02/1231.png)

## Base 16 (Hex):

_Example:_
  
 _ _
  
<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3EB2C%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>B2C</p> <p>" title="</p> <p>B2C</p> <p>" class="latex" />

You might have noticed that hex has letters and number in them. That is because they go from 0-15, and it would very difficult to make sense out of which number goes into which position. So we have 0-9 and then A=10, B=11 all the way up to F=15.
  
Again we start from right to left. First number is now worth


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E12+%5Ctimes+16%5E0+%3D+12%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>12 &#92;times 16^0 = 12</p> <p>" title="</p> <p>12 &#92;times 16^0 = 12</p> <p>" class="latex" /> 

&nbsp;

The second number is


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E2+%5Ctimes+16%5E1+%3D+32%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>2 &#92;times 16^1 = 32</p> <p>" title="</p> <p>2 &#92;times 16^1 = 32</p> <p>" class="latex" /> 

&nbsp;

The third number is


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E11+%5Ctimes+16%5E2+%3D+2816%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>11 &#92;times 16^2 = 2816</p> <p>" title="</p> <p>11 &#92;times 16^2 = 2816</p> <p>" class="latex" /> 

&nbsp;

The total number shown in our decimal system is then calculated by adding the numbers together:


<img src="//s0.wp.com/latex.php?latex=%3C%2Fp%3E+%3Cp%3E12%2B32%2B2816%3D2860.%3C%2Fp%3E+%3Cp%3E&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="</p> <p>12+32+2816=2860.</p> <p>" title="</p> <p>12+32+2816=2860.</p> <p>" class="latex" /> 

&nbsp;

[<img class="alignnone size-full wp-image-159" src="http://maximumdeveloper.com/wp-content/uploads/2015/02/b2c.png" alt="b2c" width="456" height="220" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/b2c.png 456w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/b2c-300x145.png 300w" sizes="(max-width: 456px) 100vw, 456px" />](http://maximumdeveloper.com/wp-content/uploads/2015/02/b2c.png)

# Making sense of the numbers

A hex color is made up of three parts that represent the amount of Red, Green and Blue that are mixed together. These are split up using the first and second number for red, third and fourth number for green and fifth and sixth number for blue.

&nbsp;

[<img class="alignnone size-full wp-image-137" src="http://maximumdeveloper.com/wp-content/uploads/2015/02/hexcolor.png" alt="hexcolor" width="640" height="220" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/hexcolor.png 640w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/hexcolor-300x103.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/hexcolor-600x206.png 600w" sizes="(max-width: 640px) 100vw, 640px" />](http://maximumdeveloper.com/wp-content/uploads/2015/02/hexcolor.png)

&nbsp;

Knowing this, you can now specify the amount of red, green and blue in a color. Since there are two hex numbers for each color, you can have 0 amount of a color (00), all the way up to 255 (FF). Using this system, we can specify a large number of different colors, using the amount of red, green and blue (255\*255\*255=16 581 375 &#8211; to be exact).

_Examples:_
  
**White** is made when mixing the maximum number of red, green and blue together, so it will be #FFFFFF.

**Black** is when there are no amount of any of the colors. #000000

**Shades of grey** can be done like this: #111111 (very dark grey &#8211; almost black). #CCCCCC (very light grey)

&nbsp;

# How 3 digit HEX works

Sometimes people like to use a shorthand HEX for some colors with only 3 digits. The way this works is that each digit is representing their color (red, green, blue), but when you write #F00, this is actually the same as #FF0000. So its a shortcut for when you need some special colors like red, green, blue, black, white and grey scales.

_Examples:
  
_ **Black**: #000 (#000000)

**White**: #FFF (#FFFFFF)

**Grey**: #888 (#888888)

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_13">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-hex-colors-work%2F&linkname=How%20HEX%20colors%20work" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-hex-colors-work%2F&linkname=How%20HEX%20colors%20work" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-hex-colors-work%2F&linkname=How%20HEX%20colors%20work" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>