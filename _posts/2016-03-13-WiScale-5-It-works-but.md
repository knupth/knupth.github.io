---
layout: post
title: Wiscale Devlog 5&#58; It works! But...
---

The device works, however a couple of problems have presented themselves.

First, the ESP8266 just destroys my LCD signals when turned on. This may not be a problem in the final layout, since the ESP8266 will be on the other side of the board to the signal wires, but I've decided to simply disable the ESP8266 while the Arduino grabs a signal from the LCD display. Works well except for the fact that after Wifi is enabled on the ESP8266 the only way I can force it to be disabled again is by power-cycling the module. Unfortunate but not a big deal since that was my plan all along (this thing will be run off batteries).

Second, my scales have started powering themselves up randomly. Not sure why, and not particularly interested in investing the time to fix that problem. Possibly it's happening because my table, on uneven ground in an electrically noisy environment, or I messedd up somewhere solding the wires, or who the heck knows. Worst case scenario, I power the scales directly from my wifi battery instead of with it's own 3v coin cell.

The big takeaway here is : **Working**
