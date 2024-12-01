---
title: CNC X,Y Pen Plotter
author: 
blurb: Designed an X,Y Pen Plotter, including from-scratch software using Arduino, Python, OpenCV, and Computational Geometry to convert 2D images to tool paths to create shaded drawings.
layout: blog
image: Gallery-Thumbnail-Small.PNG
---

<div style="display: flex; flex-wrap: wrap; gap: 20px; justify-content: space-between;">
  <div style="flex: 1 1 calc(33.333% - 20px); min-width: 300px;">
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@lifeofasamjohnson/video/7269625242182618410" data-video-id="7269625242182618410" style="max-width: 605px;min-width: 325px;" > <section> <a target="_blank" title="@lifeofasamjohnson" href="https://www.tiktok.com/@lifeofasamjohnson?refer=embed">@lifeofasamjohnson</a> <a title="fyp" target="_blank" href="https://www.tiktok.com/tag/fyp?refer=embed">#fyp</a> <a title="artistsoftiktok" target="_blank" href="https://www.tiktok.com/tag/artistsoftiktok?refer=embed">#artistsoftiktok</a> <a title="sketch" target="_blank" href="https://www.tiktok.com/tag/sketch?refer=embed">#sketch</a>  <a title="fypシ" target="_blank" href="https://www.tiktok.com/tag/fyp%E3%82%B7?refer=embed">#fypシ</a>  <a title="pendrawing" target="_blank" href="https://www.tiktok.com/tag/pendrawing?refer=embed">#pendrawing</a> <a title="artwork" target="_blank" href="https://www.tiktok.com/tag/artwork?refer=embed">#artwork</a>   <a title="drawings" target="_blank" href="https://www.tiktok.com/tag/drawings?refer=embed">#drawings</a>  <a title="artist" target="_blank" href="https://www.tiktok.com/tag/artist?refer=embed">#artist</a>  <a title="sketches" target="_blank" href="https://www.tiktok.com/tag/sketches?refer=embed">#sketches</a>  <a title="fyp" target="_blank" href="https://www.tiktok.com/tag/fyp?refer=embed">#fyp</a> <a target="_blank" title="♬ original sound - Roshan" href="https://www.tiktok.com/music/original-sound-7203832732459256581?refer=embed">♬ original sound - Roshan</a> </section> </blockquote> <script async src="https://www.tiktok.com/embed.js"></script>
  </div>
  <div style="flex: 1 1 calc(33.333% - 20px); min-width: 300px;">
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@lifeofasamjohnson/video/7268389183536794922" data-video-id="7268389183536794922" style="max-width: 605px;min-width: 325px;" > <section> <a target="_blank" title="@lifeofasamjohnson" href="https://www.tiktok.com/@lifeofasamjohnson?refer=embed">@lifeofasamjohnson</a> <a title="fyp" target="_blank" href="https://www.tiktok.com/tag/fyp?refer=embed">#fyp</a> <a title="artistsoftiktok" target="_blank" href="https://www.tiktok.com/tag/artistsoftiktok?refer=embed">#artistsoftiktok</a>  <a title="sketch" target="_blank" href="https://www.tiktok.com/tag/sketch?refer=embed">#sketch</a>  <a title="fypシ" target="_blank" href="https://www.tiktok.com/tag/fyp%E3%82%B7?refer=embed">#fypシ</a>  <a title="pendrawing" target="_blank" href="https://www.tiktok.com/tag/pendrawing?refer=embed">#pendrawing</a> <a title="artwork" target="_blank" href="https://www.tiktok.com/tag/artwork?refer=embed">#artwork</a>  <a title="drawings" target="_blank" href="https://www.tiktok.com/tag/drawings?refer=embed">#drawings</a>  <a title="artist" target="_blank" href="https://www.tiktok.com/tag/artist?refer=embed">#artist</a>  <a title="sketches" target="_blank" href="https://www.tiktok.com/tag/sketches?refer=embed">#sketches</a> <a target="_blank" title="♬ falling for ya - ★SPED UP AUDIOS" href="https://www.tiktok.com/music/falling-for-ya-7091906073669552902?refer=embed">♬ falling for ya - ★SPED UP AUDIOS</a> </section> </blockquote> <script async src="https://www.tiktok.com/embed.js"></script>
  </div>
  <div style="flex: 1 1 calc(33.333% - 20px); min-width: 300px;">
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@lifeofasamjohnson/video/7267304365378096430" data-video-id="7267304365378096430" style="max-width: 605px;min-width: 325px;" > <section> <a target="_blank" title="@lifeofasamjohnson" href="https://www.tiktok.com/@lifeofasamjohnson?refer=embed">@lifeofasamjohnson</a> <a title="firstpost" target="_blank" href="https://www.tiktok.com/tag/firstpost?refer=embed">#firstpost</a> <a title="fyp" target="_blank" href="https://www.tiktok.com/tag/fyp?refer=embed">#fyp</a> <a title="art" target="_blank" href="https://www.tiktok.com/tag/art?refer=embed">#art</a> <a title="robots" target="_blank" href="https://www.tiktok.com/tag/robots?refer=embed">#robots</a> <a target="_blank" title="♬ Them Changes - Thundercat" href="https://www.tiktok.com/music/Them-Changes-6741079454199580674?refer=embed">♬ Them Changes - Thundercat</a> </section> </blockquote> <script async src="https://www.tiktok.com/embed.js"></script>
  </div>
</div>

<script async src="https://www.tiktok.com/embed.js"></script>

<img src="/media/CNC-Media/CNC-big.PNG" style="max-width: 400px; float: right; margin-left: 10px">


### About

Since working at a Machine Shop I've been curious about CNC, but I wanted to build and integrate as much of a machine myself, so I converted a CNC Routing Machine into an X,Y Pen Plotter. It features a 3D printed fixture for Z-axis pen actuation, a custom plotting software, and custom embedded software/machine code.

### Skills Involved
- Mechanical Design
- Electronics
- Robotics
- Embedded Software Development
- Software Development

### Procedure

#### Converting the Router

I wired the router's X and Y axis (NEMA-17 Stepper Motors) to stepper motor controllers. I drove the stepper motors with an old laptop power supply.

<!--Close up of Z Axis with servo--> <img src="/media/CNC-Media/linear-fixture.PNG" style="max-width: 400px; float: right; margin-left: 30px; margin-bottom:30px">

#### Creating the 3D printed Z-Axis

To create the Z-Axis, I 3D printed a fixture with features for a servo, gear rack and pinion to mount to the head of the router. I went through a few iterations to find a design that was rigid when acutating the pen onto paper and quick to print. A ball screw and linear guides would have increased accuracy, but I was more focused on proving this pen plotting concept (and software) would work.

#### Creating the plotting software & Machine Code

At the moment, I've created custom plotting software that converts SVGs--made of bezier curves--into toolpaths. The curves are converted into polygonal lines, which are converted into a series of X,Y coordinates before being scaled to fit on a page that the CNC Router can plot.



<!--Picture of machine code, gif of moving head--> <img src="/media/CNC-Media/drawings-before-z-integration.PNG" style="max-width: 400px; float: right; margin-left: 30px; margin-bottom:30px;">
#### Accepting the Machine Code

These drawings were made before integrating the Z-Axis →

Not Bad!

It works because the machine code is sent to a ESP32 microcontroller with custom embedded software/machine code that moves the motors to the desired coordinates.

Essentially, once the motors have reached the desired point and moved the Z-Axis accordingly, the embedded software informs the plotting software that it's ready for the next X,Y coordinate. Commandeered by the plotting software, the router head plots "generated" images.

#### Trial and Error 

 I iterated a few designs to a working 3D printed gear rack and pinion. It took a few tries because of my material choice. The polylactic acid (PLA) filament and my printer doesn't have a fantastic tolerance or surface finish with the orientation I printed it, but I realized if I minimize the contact area between the rack and it's rail, it wouldn't over constraining the part. This allowed for surprisingly fluid and repeatable motion. I don't have a Keyence or MicoVu system at home but I would measure the repeatability if I could.
 <img src="/media/CNC-Media/line-repeatability.PNG" style="max-width: 400px; float: right; margin-bottom:30px; margin-top:20px; margin-left: 30px">

With a self-programmed CNC system I don't know how much the drive screws are slipping with respect to the motor and if there is skew happening due to the rust of the screws and the acceleration programmed in to the controller. As robotic as a CNC pen plotter can be, the imperfections make it surprisingly human.

I'm also in the process of creating a custom plotting software that converts images into hatched tool paths. The software posterizes an image into 4 rasterized colors (4 layers of shading), before programatically separating each color into respective layers. Each "colored" layer is characterized by a set of polygons that make up the contours of the continuous bodies of color. A bounding box is created for each polygon before applying a hatch pattern to it. The space outside the contours, but within the bounding box is negated, creating a "patch" for each polygon. 

The polygonal points are converted to bezier curves (and a respective SVG file), which are converted to a series of X,Y,Z coordinate that indicates the next position the router head needs to move and if the pen needs to be moved up or down. Each SVG file is then converted to a CSV to store the "machine code", which can be sent to the embedded script to move the router head.


<!-- #### Art Gallery: -->


<!-- ### Learn More
Github:  -->