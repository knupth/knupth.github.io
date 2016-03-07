---
layout: post
title: WiScale\: Planning
---

I recently got into the whole activity tracker craze. Looked into getting a wifi scale and baulked at the price. I'm pretty sure I can do it much cheaper and have a neat project to work on at the same time.

So here's the plan: Break out the LCD pins on my current scales, then use an Arduino to read the LCD and an ESP8266 module to log it to [Thingspeak](https://thingspeak.com/).

I don't forsee many problems with this so here's the steps I'll be taking.

1. Setup the ESP8266 as a module for the Arduino
2. Decode the LCD with the Arduino and interface it with the ESP8266
3. Power management
4. Final assembly

Wish me luck.
