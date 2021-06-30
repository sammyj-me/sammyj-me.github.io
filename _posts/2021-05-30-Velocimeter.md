---
title: Velocimeter
author: Sam Johnson
blurb: A device to measure position, velocity, and acceleration over time for sport application purposes.
layout: blog
image: running_machine.JPG
---
## Project Details:
#### Type: Personal Project <br>Supervisor: Me <br>Dates Active: May 2021 – Present
<br>

In May 2020 I injured my shoulder, throwing a wrench into my plans to experiment heavily with swim training over the year-long quarantine. I figured if I didn't have pool or gym access, I couldn't work my shoulders for a good while anyway so I decided to dive into
Track & Field, specifically sprinting.

Over the course of 13 months, I managed to improve my top speed over 10m from approximately 18.2 mph to around 21.0 mph by reading about training methodologies online and designing my own program to get me faster.

The way I would measure my times would be by taking a video of myself, and subtracting the end point timestamp from the start point timestamp. After about a year of doing this I have learned the following:
- It's tedious to flip between the camera, video editing app, and calculator on your phone
- 60 fps video has limitations in terms of counting frames/accuracy of times
- You are prone to biasing start frames to make you think you're faster than you actually are
- Bad camera angles or phone-related mishaps ruin the trial

Also over the course of the past year, I've explored commercial timing systems available online.

### One that caught my eye was the 1080 sprint, a string-based velocimeter where the device computes the velocity of a string as it's being pulled by an athlete.

I had seen this technology before in use by The Race Club, an elite swim club in Florida--it appears that technology can be used for a variety of velocity-based sports.

### The only issue was that the 1080 Sprint costs $17,500, and The Race Club charges you $1000 dollars to ONLY USE their device.

:(

## I got straight to conceptualizing my own in May of 2021 .

In my opinion, this is as much of a social issue as it is a financial one. I understand that these businesses are trying to make a profit, but I don't believe there should be a paywall as high
as there is. As I write this on 6/30/2021,

## it is to my understanding that there are whole sectors of society that will not have access to these technologies and potential advancement in knowledge of training because the cost of these devices are simply too high.
Long term, I hope to bring a more cost effective velocimeter to market.

6/30/2021 Project Updates:
<img src="\media\Project Pics 2021\Velocimeter\topdown_velocimeter_withpi.JPG" alt="Top Down View"/>
<img src="\media\Project Pics 2021\Velocimeter\pulleysystem_iteration.JPG" alt="Pulley System Iteration"/>

### Project Details (1 month since conceptualization):
- Raspberry Pi with Tkinter Python GUI & scripts that collects data from a rotary encoder and outputs live interactive data.
- Algorithms are in place to detect when athletes start and stop.
- An Arduino acts as the main "counter" to the rotary encoder and is interfaced to send position information to the raspberry pi.
- Designed, modeled and printed a working drive train to reduce data output to the Arduino.
- Position measurements are accurate to the inch and can calculate velocity and acceleration information every 0.03 seconds.