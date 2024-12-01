---
title: Blood Analysis Device 
author: Sam Johnson
blurb: Building a device that measures platelet reactivity.
layout: blog
image: PlateletThrombometer.JPG
---
## Project Details:
#### Co: SUBC INC. <br>Supervisor: Dr. Dan Ericson <br>Dates Active: June 2020 – Present
<br>
The SJ models (SJ-01 and SJ-02) are the first two single-channel platelet reactivity test devices of their kind. These tests utilize blood from a finger stick with no chemical agonists to give users an overall picture of how reactive their platelets are. The PRT test mimics how platelets are activated in an arterial stenosis (constricted artery) with a micrometer sized spring.

<img src="\media\Project Pics 2021\PlateletProject\sidebyside.JPG" alt="SJ-01 and SJ-02"/>
<img src="\media\Project Pics 2021\PlateletProject\gui.JPG" alt="SJ-01 GUI Home Screen"/>


The PRT tests mimic how platelets are activated in an arterial stenosis by systematically increasing the shear stress. 
Blood is directed through coil, within a narrowed area in the test cartridge, increasing shear stress, activating platelets.
<img src="\media\Project Pics 2021\PlateletProject\cartridges.JPG" alt="test cartridges"/>
Above image are test cartridges where the user fills their blood.*
<img src="\media\Project Pics 2021\PlateletProject\plateletmass.jpg" alt="platelet mass"/>
The test is marked to end once enough platelets collect (see white masses in above image) around the coil, increasing the pressure within the system to a certain threshold.

Test times are reported in seconds--shorter times indicate higher platelet reactivity and longer times indicate reduced platelet reactivity (possibly identifying patients’ who are at risk of bleeding).
My own contributions to this project started with the conceptualization of the design with my associate/supervisor Dr. Dan Ericson. In May of 2020 we were benchtop testing prototypes and in June of 2021, iterated to a version that is in clinical trial at the University of Massachusetts, The Mayo Clinic and Ohio State University.

<img src="\media\Project Pics 2021\PlateletProject\circuitry2.JPG" alt="SJ-01 and SJ-02"/>
<img src="\media\Project Pics 2021\PlateletProject\ioport.JPG" alt="SJ-01 and SJ-02"/>


Things I did:
-	Unit tested:
	components for power and data logging purposes by writing Arduino code for microfluidic pumps, LEDs, photoresistors, H-bridges, solenoid valves, and ultra-low pressure transducers (with corresponding amplifiers).
	Programmed a touch-interactive GUI for a 3.5” 480x320 LCD display
-	Integration Tested:
	Developed algorithm to allow user to load blood to a point determined by the LEDs and photo resistors, and to then cycle until the pressure transducers reached a cutoff value
	The stop in blood flow is determined by increased pressure in the system.
-	System Tested:
	Troubleshooted microfluidic air leaks, circuit connectivity issues, and user interface bugs.
-	Acceptance Tested:
	Ran my own blood (but mostly Dan's) to ensure quality of data before shipping to other sites for clinical testing.

I also Designed, Modeled and 3D Printed around 20 different parts that made up various fixtures to hold the test cartridges, mount LEDs and photoresistors, in addition to shooting and editing videos for briefing and training purposes.


