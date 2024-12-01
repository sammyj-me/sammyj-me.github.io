---
title: Reverse Engineering a $20,000 Running Machine
author: 
blurb: 'Building an Electronic Resistance Machine for Athletic Training and Analysis'
layout: blog
image: isometric_render.JPG
---

### About
When I saw this device: https://store.simplifaster.com/product/1080-sprint/ I thought the $20,000 price tag was reasonable for professional teams to purchase, but not for my personal use. So I decided to build my own and attempt to solo found and launch my own company, Aperto.

<img src="/media/Terrier-Media/use.png" style="max-width: 400px; float: right; margin-left: 10px; margin-bottom:20px;">
The Aperto Terrier is a consumer electronic device designed for measuring sprinting and linear velocity analysis. Athletes essentially unreel a spool that is measured by a rotary encoder, capturing their linear motion. Signal processing techniques extract over 18 running metrics including splits, max speed and more.

With a user-friendly interface, athletes can access detailed reports and velocity visualizations to gain insights into technique and progress.

The Aperto Terrier aims to help individuals, athletes, and researchers explore, innovate, and contribute to the advancement of athletic analysis.

### Skills Involved
- Mechanical Engineering and Industrial Design
- Electronics Engineering
- Sensor Technology
- Embedded Systems Programming
- Signal Processing
- Data Analysis and Interpretation
- Software Development
- Power Electronics

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

#### Mechanical Design
<img src="/media/Terrier-Media/Top-Down.PNG" style="max-width: 400px; float: right; margin-left: 20px; margin-bottom:20px;">
I began this project selecting off-the-shelf parts, trying to quickly prototype something viable. The key objective at first was to prove the concept that the device could accurately measure and record sprinting statistics.

Once a basic setup was working, I began redesigning the internal parts and mechanisms from the ground-up. I separated the design into a few "modules" including modules for the: line spool, level-wind mechanism and an encoder spool. These components were 3D printed and mounted inside an aluminum project box.

The line spool has integrated a Brushless DC (BLDC) motor to provide drag for backlash of 80lb braided kevlar line that is tied to a user.

The level-wind mechanism is a module with a servo, rack and pinion, that serves to maintain a level line as the BLDC motor reels back in the line.

The encoder spool has an AMT-102-V encoder that acquires all position data of athletes unspooling the line.

I applied concepts from drag, backlash, dimensioning and tolerancing, machine design, DFA/DFM, material science and physics to iterate to a mechanical design and part selection that worked.

I used ISO 2768 tolerances for shafts to guide the dimensions I assigned with GD&T to parts with their unique functions and features. 

For majority of development, I used PLA plastic sliced, printed and glued to have the strongest geometries for their function, since 3D printed parts are anisotropic.

It wasn't until after torsion failures on the shafts and motor-to-spool couplings that I refined prototype mechanisms to more robust designs using aluminum shafts and monolithic part bodies to save time and effort with assembly.

#### Embedded Software Development 

To add functionality to the parts, specifically the encoder, motor and servo, I wrote an Arduio program for an ESP32 to control the logic flow of the device. This enabled the acquisition of rotation point readings, stall detection, and managing the level wind mechanism's oscillation on rewind.

Embedded Control Concepts I found interesting:
- UART Bandwidth Limitations
- Encoder Look-up Tables
- Low level embedded control in tandem with the Arduino IDE
- Polling vs. Hardware Interrupts
- Sensor Integration and Design Trade-offs

I used simple geometry to convert the circumference of the idler spool to a 48 PPR calibrated 102-AMT-V encoder.

It was more complicated to accept the data. There were limitations on a single thread of an ESP32. Properly learning how threading worked would have saved me time and effort integrating sensors to perform actions required.

In terms of sensor choice, there are things with early prototypes that could have been done differently.

For example: I didn't realize there are motors with hall-effect sensor built in. This would have saved me time with designing the mechanical feature to fit a more expensive off-the-shelf separate hall-effect sensor, and integrating it, since there is a small neodymium magnet that's required to be embedded into the the side of the line spool.

The difficulty with choosing the "correct" hardware lies in the patience of the designer to find a more optimal design early before building. As a solo developer I found myself losing focus if I wasn't creating mechanical prototypes. The mistakes I made in this process made me realize the benefits of brainstorming and creating design matricies to analyze design from a system-level perspective.

After getting the encoder data acquisition method working in a minimum-viable version, I built various metrology tools to calibrate encoder values. This included Arduino and python scripts to collect physical encoder readings, and ways to visualize current and past trials.

#### Python Software Development

To interface with the ESP32 and store all the data, I wrote a Python program with a UI to send commands via USB because I found there wasn't a faster (and more easy to implement) method to transfer encoder data. In the Python program I used statistical analysis to process the raw encoder readings, visualize velocity sprinting stats, and organize athletes. More specifically, I enabled creation of athlete-specific folders for data organization, and reduced user friction through QR code recognition for wristbands (instead of repeatedly typing in user information).

I used versions of the metrology tools I built to create the user experience where the data starts collecting to the first 0 point after the athlete hits a speed threshold.

Python Programming Concepts I found interesting:
- Raw sensor data processing (Savitzky-Golay vs. Moving Average vs. Kalman Filtering) with architected .CSV
- Extracting analytics from raw data
- Excel Spreadsheet scripting
- OpenCV QR Recognition

The process of data acquisition is as follows (for the following reasons):
- The ESP32 logs all encoder values (polling the current count) to a multi-dimensional array to hold values of encoder count and time (since the string of data was too much for live serial-data acquisition).
- After finishing a rep, the ESP32 is sent a command to transfer the few thousand lines of encoder values to the python script and into a .CSV based on XON/XOFF flow control concepts.
- The CSV is trimmed to the correct distance, and Data to set distances is then extracted from the CSV file.
- The trimmed CSV is then plotted and saved to a local file location
- The user now has options to plot any collection of CSVs and extract relevant data to compare stats.

<div style="display: flex; justify-content: center; align-items: center;">
    <img src="/media/Terrier-Media/Data Comparison.PNG" style="margin-right: 20px;">
</div>
<br>

#### Power Electronics
There were a few critical items that I found in regards to power electronics:

- Mechanical Design and placement of components
- Battery Management and adjacent software features
- BLDC Motors and Compatible Speed Controllers

### Terrier In Action
<div style="display: flex; justify-content: center; align-items: center;">
    <iframe src="/media/Terrier-Media/use-video.mp4" style="height:500px; margin-left: 20px;"></iframe>
</div>
<br>
<br>
<br>
### Seeking Feedback from the Pros

- It was amazing to have a product that was immediately useful for coaches. Those reasons are as follows:
    - Track data, splits, etc. from rep to rep 
    - Track data, splits, etc. from within graphs
    - Track data, splits, etc. across dates
    - Track data, splits, etc. across different types of reps



^^ Need to be able to explain to a lay-person how this is useful... (this is where I failed in the interview because nobody knows how track works...what problem am I solving...? It's all about framing)

<div class="cols">
    <div class="half">
        <img src="/media/Terrier-Media/IMG_9031.JPG" display="inline;" style="max-width: 400px; float: center; margin-left: 20px;  margin-bottom:20px;">
        <p style="max-width: 400px; margin-left: 10px">
            Early in development, I shared my work online, which led to an invitation to visit Ferdinand Omanyala--Africa's Fastest Man--in Nairobi, Kenya. Embracing this opportunity, I demo'd my prototype and gained valuable feedback from a new culture's perspective.
        </p>
    </div>
    <div class="half">
        <img src="/media/Terrier-Media/Aperto x Ferdinand Omanyala.png" display="inline;" style="max-width: 400px; float: center; margin-left: 20px; margin-bottom:20px;">
    </div>
</div>

Similarly, I visited the 2022 Track and Field World Championships in Eugene, Oregon, and gained valuable feedback from international coaches and fans.
<br><br>
In October 2022, I took the Terrier to Oberlin College to test updated designs and software with Ben Wach, a coach I had previously met in Oregon.
<br><br>
Most recently, students from Cornell University's Track Team have started a similar project. I have been giving them resources to engineer an upgraded version.

<!-- Overall, this project demonstrated our capacity to integrate electronics, sensor data interpretation, embedded system programming, signal processing, statistical analysis, power management, design principles, and rapid prototyping into a successful, user-friendly sprint telemetry device. -->
<!-- 
### Learn More
Github -->
<!--Picture of device, picture of UI, picture of graphs, picture with Ferdinand + athletes, testing, in little gallery-->