---
title: Window Opening Robot
author: Sam Johnson
blurb: An Arduino-powered robot that cracks a window once temperature reaches a certain threshold.
layout: blog
image: WindowRobot.PNG
---


I  conceptualized a version of this project in 2017, to roll my blinds up and down in my freshman dorm.

I finally found time to execute this idea in 2018 after I moved into my a home off-campus, changing the object being actuation, from window blinds to sliding window.

My basement-room had a ton of heating elements and got uncomfortably warm in the winter time. I would wake up in sweat to open my window, but the frigid Minnesota air would quickly cool my room, waking me up again, only this time to CLOSE the window.

To create this linear actuating system to open and close my window for me I would have to...
#### link together the following:
- DHT 22 sensor
- Timing belt and pulleys mounted to a wooden frame
- Stepper motor and h-bridge controller
- AC Relay wired to a fan to circulate air
- An Arduino to commandeer everything

#### The logic was as follows:

1. Delay 30 minutes (1800 seconds)
2. Check reading of the DHT sensor
3. While adjust = true<br>
	3a. If sensor read > 72 degrees<br>
	3b. Open window, turn on fan<br>
	3c. If sensor read < 68 degrees<br>
		      i. Turn off fan, close window<br>
		     ii. Adjust = false (closing the loop)
4. Adjust = true (sets conditions for the next temperature check in 30 minutes)

Unfortunately I was not able to fully realize this project but I was able to prove the concept by:
- Modeling and printing a mount to connect the timing belt to the window itself
- Successfully reading values from the temperature sensor
- Actuating the stepper motor via h-bridge and Arduino code.