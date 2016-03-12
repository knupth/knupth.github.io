---
layout: post
title: Wiscale Devlog 2&#58; Decoding the signal
---

Now that we can, let's take a look at the signal. Yellow and Pink are common pins, azure is a segment pin with zero segments 'on', cyan is a segment pin with three segments 'on'.

[![Oscilloscope waveform](https://cloud.githubusercontent.com/assets/16624353/13721429/21c0ed94-e87b-11e5-8248-6b2e0fcfb4d1.jpg)
](http://imgur.com/1WjnDlk)

There are 4 important voltages here, 0v, 1v, 2v and 3v. The backplane voltage is looping in a \[3,0,1,2,1,2\] voltage cycle. They flip back and forth to make sure that there isn't much DC between the backplanes and the segments, otherwise the dialectric can get 'stuck'. So to calculate the voltage over a certain segment dialectric (as opposed to the voltage at the segment select pin) we subtract the voltage of the backplane from the voltage at the segment select pin. 

For example, the voltage of the dialectric between the yellow backplane and the azure segment we go \[3-2,0-1,1-2,2-1,1-2,2-1,1-2,2-1\], which is \[1,-1,-1,1,-1,1,-1,1\]. The voltage isn't fluctuating very much, this makes sense because the segment is 'off'. Now let's look at the voltage between the yellow backplane and the cyan segment. \[3-0,0-3,1-0,2-3,1-2,2-1,1-0,2-3\] = \[3,-3,1,-1,-1,1,1,-1\]. See we get that one spike in there from 3v to -3v, which turns the segment 'on'. The dialectric responds non-linearly to the voltage fluctuations. That's why an 'off' segment looks totally off and not just '1/3 as bright' as an 'on' segment.

This gives us an easy way to know if a segment is 'on' or not. If the segment select pin is at 3v when the common pin for that specific backplane drops to 0v, then we know that segment is 'on', and if it isn't at 3v we know it's 'off'. 

We can use the digital input pins on the Arduino for this. Looking at the datasheet, the required voltage for a "high" on the digital inputs when powered at 3.3v is about 1.6v. The signal coming from the LCD is pretty noisy, so let's assume a worst case scenario of 2.2v for the highest signal we want to count as "off". So we want to scale 2.2v to under 1.6v, let's say 1.5v so be safe. 1.5/2.2 ~= 0.68 , let's call that 66% for simplicity sake, so I'll use a 100k-200k voltage divider to reduce the voltage on the Arduino's digital input pins. That way the input pins will only ever be "high" when the LCD pin is at its highest voltage.

Even better, since the common pins change voltage during every step in the cycle we can simple monitor one pin and use the large voltage swing on it as an alignment signal, then just step along with the voltage changes and assume that the other common pins are behaving normally instead of having to monitor them directly.

The end result is needing 12 Arduino pins to monitor the LCD, one of which is an ADC pin. Very doable.
