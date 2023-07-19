---
title: Consumer Electronic Device
author: 
blurb: 'The Aperto Terrier → An Open-Source Device for Linear Athletic Analysis'
layout: blog
image: isometric_render.JPG
---

### About
The Aperto Terrier is an open-source consumer electronic device designed for measuring sprinting and linear velocity analysis. It uses a simple motor and encoder to capture and track linear motion. Signal processing techniques extract metrics like stride length, speed, and acceleration.

With a user-friendly interface, users can access detailed reports and velocity visualizations to gain insights into technique and progress.

The Aperto Terrier aims to help individuals, athletes, and researchers explore, innovate, and contribute to the advancement of athletic analysis.

### Skills Involved
- Mechanical Engineering and Industrial Design
- Electronics Engineering
- Sensor Technology
- Embedded Systems Programming
- Signal Processing
- Data Analysis and Interpretation
- Software Development

### Procedure

<!-- Sourced Parts:
- off the shelf
- aimed for rapid prototyping because I didn't have enough knowledge to know what would work or what didn't.

Mechanical Design:
- Designed parts internal to device, mechanical mechanisms
- Line Spool (housed BLDC Motor that gave drag for backlash)
    - embedded a magnet for hall effect sensor/stall detection
- Level-Wind Mechanism
- Encoder Spool (with 80 lb braided fishing line--white for visibility)
- 3D printed these things
- mounted inside an aluminum project box

Electrical Design:
- Sourced a BLDC motor and ESC, with adjustable braking on the ESC
- Source ESP32
- Sourced Servo
- Created Voltage divider for LiPo battery
- hall effect sensor for stall detection

Embedded Software:
- Wrote Arduino program to ESP32 to acquire encoder readings
- read hall effect sensor for stall detection
- oscillated level wind mechanism on rewind
- centered servo and read encoder on unwind.

Supporting Software:
- Wrote python script to send commands from USB from an easy to use UI
- Allowed for athlete folders to be generated to organize users
- created QR recognition for wristbands to reduce friction of use
- statistical analysis to smooth data
- 18 variables, splits and stats and +150m of line
- Wrote UI, threaded application

A strong understanding of electronics is vital. This includes knowledge of circuit design, components like sensors, transistors, capacitors, and resistors, as well as digital electronics concepts such as microcontrollers and logic gates.

Knowing how to select, incorporate, and interpret data from sensors is critical in a telemetry device. This could include accelerometers, gyroscopes, or GPS modules for tracking movement and speed.

A sprinting telemetry device would likely involve an embedded system. Being able to program these systems, typically using languages like C or C++, is a crucial skill.

Raw data from sensors often needs to be processed and filtered to be useful. This requires an understanding of signal processing techniques.

Once the data is gathered, it needs to be analyzed and interpreted. This could involve statistical techniques, and even machine learning, depending on the complexity of the device.

Given that the device is likely to be portable, understanding how to manage power consumption for optimal battery life is an important skill.

The device needs to be designed to be durable, lightweight, and comfortable for the user. This involves knowledge of materials, ergonomics, and design principles.

For data visualization or interfacing with the device, a software application might be needed. This could involve coding in languages such as Python or Java, and knowledge of user interface and user experience design.

Rapid prototyping skills such as using a breadboard for electronic components or 3D printing for casing can speed up the development process. In addition, being able to thoroughly test and debug both hardware and software is a key skill.

#### Results/Professional Interest:
- After posting a prototype online I was invited (on my own dime) to Nairobi Kenya, to visit Ferdinand Omanyala. I went.
- I flew by myself to the 2022 Track and Field World Championships in Eugene, Oregon a week early to ask international coaches and fans for feedback.
- I went to Oberlin College in October 2022 to test updated designs and software with a coach I met in Eugene, Oregon. -->

#### General Design
I began this project selecting off-the-shelf parts, aiming for rapid prototyping due to the initial uncertainty about what components would work best. The key objective was to create a device that could accurately measure and record sprinting statistics.

Mechanical design involved a ground-up approach for the device's internal parts and mechanisms, including a line spool, level-wind mechanism and an encoder spool. These components were 3D printed and mounted inside an aluminum project box.

The line spool has integrated a Brushless DC (BLDC) motor to provide drag for backlash of 80lb braided kevlar line that is tied to a user.

The level-wind mechanism is a module with a servo, rack and pinion, that serves to maintain a level line as the BLDC motor reels back in the line.

The encoder spool has an AMT-102-V encoder that acquires all position data of athletes unspooling the line.

#### Embedded Software Development
I wrote an Arduio program for an ESP32, enabling the acquisition of encoder readings, reading the hall effect sensor for stall detection, and managing the level wind mechanism's oscillation on rewind. This program was also responsible for centering the servo.

#### Python Software Development
In addition, I wrote a Python script with a UI to send commands via USB, acquire encoder data, visualize velocity information, sprinting stats, and organize athletes. More specifically, I enabled creation of athlete-specific folders for data organization, and reduced user friction through QR code recognition for wristbands (instead of typing user information in every time).

After raw data acquisiton, this program also handled statistical analysis for data smoothing, extracting 18 variables from each rep, such as splits and stats from the +150m of unspooled line.

#### Public Recognition
Early in development, I shared my work online, which led to an invitation to visit Ferdinand Omanyala--Africa's Fastest Man--in Nairobi, Kenya. Embracing this opportunity, I demo'd my prototype and gained valuable feedback from a new culture's perspective.
<br>
<br>
Similarly, I visited the 2022 Track and Field World Championships in Eugene, Oregon, to seek feedback from international coaches and fans. <br><br>
In October 2022, I took the Terrier to Oberlin College to test updated designs and software with Ben Wach, a coach I had previously met in Oregon.

<!-- Overall, this project demonstrated our capacity to integrate electronics, sensor data interpretation, embedded system programming, signal processing, statistical analysis, power management, design principles, and rapid prototyping into a successful, user-friendly sprint telemetry device. -->
<!-- 
### Learn More
Github -->
<!--Picture of device, picture of UI, picture of graphs, picture with Ferdinand + athletes, testing, in little gallery-->