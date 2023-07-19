---
title: CNC X,Y Pen Plotter
author: 
blurb: Designed an X,Y Pen Plotter, including from-scratch software using Arduino, Python, OpenCV, and Computational Geometry to convert 2D images to tool paths to create shaded drawings.
layout: blog
image: WindowRobot.PNG
---

### About
Since working at a Machine Shop I've been curious about CNC, but I wanted to build and integrate as much of a machine myself, so I converted a CNC Routing Machine into an X,Y Pen Plotter. It features a 3D printed fixture for Z-axis pen actuation, a custom plotting software, and custom embedded software/machine code.

### Skills Involved
- Mechanical Design
- Electronics
- Robotics
- Embedded Software Development
- Software Development

### Procedure

#### Converting the Router: <!--Picture of router, wired-->
I wired the router's X and Y axis (NEMA-17 Stepper Motors) to stepper motor controllers. I drove the stepper motors with an old laptop power supply.

#### Creating the 3D printed Z-Axis <!--Close up of Z Axis with servo-->
To create the Z-Axis, I 3D printed a fixture with features for a servo, gear rack and pinion to mount to the head of the router. I went through a few iterations to find a design that was rigid when acutating the pen onto paper and quick to print. A ball screw and linear guides would have increased accuracy, but I was more focused on proving this pen plotting concept (and software) would work.

#### Creating the plotting software & Machine Code <!--Picture of software converted to hatch patterns-->
I then created a custom plotting software that converts images into hatched tool paths. The software posterizes an image into 4 rasterized colors (4 layers of shading), before programatically separating each color into respective layers. Each "colored" layer is characterized by a set of polygons that make up the contours of the continuous bodies of color. A bounding box is created for each polygon before applying a hatch pattern to it. The space outside the contours, but within the bounding box is negated, creating a "patch" for each polygon. 

The polygonal points are converted to bezier curves (and a respective SVG file), which are converted to a series of X,Y,Z coordinate that indicates the next position the router head needs to move and if the pen needs to be moved up or down. Each SVG file is then converted to a CSV to store the "machine code", which can be sent to the embedded script to move the router head.

#### Accepting the Machine Code <!--Picture of machine code, gif of moving head-->
The machine code is sent to a ESP32 microcontroller with custom embedded software/machine code that moves the motors to the desired coordinates. Essentially, once the motors have reached the desired point and moved the Z-Axis accordingly, the embedded software informs the plotting software that it's ready for the next X,Y coordinate. Commandeered by the plotting software, the router head plots custom generated (and shaded) images.

<!-- #### Art Gallery: -->


<!-- ### Learn More
Github:  -->