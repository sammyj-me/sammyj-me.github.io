---
title: Computer Vision
author: Sam Johnson
blurb: 'Apertotech-Vision → An Open-Source Running Analysis Software'
layout: blog
image: Computer-Vision.PNG
---
<img src="/media/Computer-Vision-Media/Running Setup.PNG" style="max-width: 400px; float: right; margin-left: 20px; margin-bottom:20px;">
### About
ApertoTech-Vision is an Open-Source computer vision project that uses pose estimation to analyze sprinting performance from 2D video. Developed with Python, OpenCV, MediaPipe, and JavaScript, I created it to track my sprinting speed and (hopefully) lay the groundwork for cost-effective sport science technology for athletes, trainers, and researchers.

### Skills Involved
- Forward Kinematics
- Computer Vision
- Pose Estimation
- OpenCV
- MediaPipe
- JavaScript
- Data Analysis
- User Interface Design
- Cloud Integration

<img src="/media/Computer-Vision-Media/sam-runs.PNG" style="max-width: 400px; float: right; margin-left: 30px; margin-bottom:30px;">
### Procedure

<!-- 

Aperto-Vision combines OpenCV and Google MediaPipe pose estimation to map runner's positions and velocities based on the frame rate of the video. The Python code uses a point mapping algorithm I wrote to calculated velocities, based on the scale of measured fiducials that are recognized with image thresholding and contour detection.

After collecting joint data, ApertoTech-Vision determines stride length, stride frequency, max velocity, and 10m fly split, along with a velocity graph that spans the curve. This enables automated analysis of running technique, stride length, body alignment, and more.


This project implements computer vision techniques to analyze visual data from running activities. It uses pose estimation algorithms for tracking and mapping runner's positions accurately. The coding development primarily uses Python to construct and employ these computer vision and pose estimation algorithms.

Through a point-mapping algorithms based on recognizing measured fiducials, ApertoTech-Vision

OpenCV library serves as the basis for image processing and computer vision tasks, while the MediaPipe framework is employed to access pre-built computer vision models for efficient pose estimation. JavaScript is used for the creation of the user interface and other interactive elements of the platform. Mathematical principles and algorithms are applied to precisely map runner's positions based on their joint movements.

#### User Flow Algorithm: -->
To use this software, users set up four fiducials (cones) measured to 10m, which sets the scale of their joint coordinates in frame. They record a 60-240 FPS video of themselves performing a 10m acceleration or a 10m "flying" sprint (a popular rep distance for max effort sprint training).

The analysis process involves several steps. A thresholding/convex hull algorithm attempts to detect cones to set the pixel scale, although this has proven unreliable in different environments where there is low light, reflective materials, or inconsistent coloration.

Alternatively, I created a method to manually click cones (in any order) to set the scale of pixels to meters within the frame of the video.

<img src="/media/Computer-Vision-Media/Map-person.PNG" style="max-width: 400px; float: right; margin-left: 20px; margin-bottom:20px;">
After setting the scale, the video's frames are cycled through for analysis, storing each set of detected athlete's nose, ankle, toe and heel coordinates. The system calculates the runner's instantaneous velocity at every video frame based on nose-pixel (previously hip-pixel) distance travelled and the scale set with fiducials. Metrics such as max velocity and 10m fly split are derived from the nose coordinates because I found those to be most stable frame to frame.


Step length and step frequency are derived from the data set of ankle, toe and heel coordinates. It was beneficial to include all three joint coordinates because of the high density of 2D points as the coordinates on frames are stacked up. 

<img src="/media/Computer-Vision-Media/Hip-Velocity-Cycles.PNG" style="max-width: 400px; float: right; margin-left: 20px; margin-bottom:20px;">
I attempted to use a k-nearest neighbors algorithm to determine clusters of points, but the data proved to be too noisy, even with processing. Instead, I determined step length and stride frequency by flattening the 2D coordinates to a histogram and looking at the spikes in occurence. Each spike in occurrence indicate a "step." It wasn't perfect, but under certain filming conditions, standard deviation is able to detect the position of each foot touchdown. Time of median foot placements within each histogram data set averaged across each foot touchdown provides the step length result. The time between steps yields step frequency.

<div class="cols">
    <div class="half">
        <img src="/media/Computer-Vision-Media/Toe-Points-240fps.PNG" style="max-width: 400px; float: right; margin-left: 20px; margin-bottom:20px;">
    </div>
    <div class="half">
        <img src="/media/Computer-Vision-Media/Toe-Points-240fps-zoomed.PNG" display="inline;" style="max-width: 400px; float: center; margin-left: 20px; margin-bottom:20px;">
    </div>
</div>

All data was aggregated and converted to computer graphics that was then overlayed to the original video. I had the idea to release this as a SaaS and reached out online to sprinters in Kenya, Ireland, Denmark and across the USA for testing before realizing the challenges in cone detection and user issues with different phones and perspectives.

<!-- Without knowing the full scope of my problems, I built a user-authenticated website in javascript that was never officially released, but I did successfully implement my script into a cloud function for my own learning purposes. -->

Furthermore, I thought to address fiducial inaccuracies by adjusting instantaneous velocity points using a scale factor based on vantage point geometry. A solution I thought of but never was able to implement. 

The ApertoTech-Vision system is best suited for lab settings, with effectiveness in larger training settings yet to be tested.

The project underwent multiple iterations, including a kinogram generator for "useful" positions to guide coaches on proper positioning.

### Learn More
<a href="https://github.com/sammyj-me/ApertoTech-Vision">If you want to view my code, click this GitHub Link</a>