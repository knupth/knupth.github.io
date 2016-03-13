---
layout: post
title: Wiscale Devlog 4&#58; Decoding the signal part 2
---

With the LCD segment pins connected to PortB and PortC on the microcontroller I get data like this

    PinB: 00110000, 00111001, 00101000, 00111000 
    PinC: 00000001, 00100001, 00100000, 00100001 

Just the port logic levels during each of the LCD screen phases. To get the actual digits I'm just using a binary search tree.

image

Pretty poorly balanced but it gets the job done.
