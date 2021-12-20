---
title: 3D Printing "Pre-Creased" Origami Crease Patterns
author: Sam Johnson
blurb: Is there an easier way to create complex origami?
layout: blog
image: PlateletThrombometer.JPG
---
## Project Details:
#### Co: Me <br>Supervisor: Me <br>Dates Active: December 2021
<br>
I picked up my first origami book at the age of 6: The complete book of origami by Robert J. Lang.

/* <img src="\media\Project Pics 2021\PlateletProject\sidebyside.JPG" alt="SJ-01 and SJ-02"/>   */
/* <img src="\media\Project Pics 2021\PlateletProject\gui.JPG" alt="SJ-01 GUI Home Screen"/> */

Over the last few years I've gotten into more complex origami that involves pre-creasing designs to a blueprint--a crease pattern--before collapsing them by folding each pre-made crease in a specific order.
The process of pre-creasing can be extremely tedious, taking hours to make hundreds of folds while weighing the risk of human error. Mistakes add up and inaccuracies can turn your art project into plain recycling.

To leapfrog the step of pre-creasing, I decided to create my own "paper" by modeling a thin plane in SolidWorks and extruding even thinner cuts along the crease pattern. The specific model I decided to craft is called "Spring Into Action" by Jeff Beynon.

I was only able to print 1/6th of the model due to size limitations of my trusty Prusa Mini.

Prusa Slicer Settings were as follows:
- 
- 
- 
- 
- 

Results: Print bed isn't always completely level or adhesion in certain areas isn't always as good--this is extremely important when printing thin layers that are critical to the form and function of your product.

I sent my results to Robert J. Lang himself while inquiring if he's worked on anything similar. He replied with a link to his Origami lamp that he designed, and that is in production. This piqued another thought of curiosity...What if I modeled a lithophane onto the surface of this lamp and created a custom graphic to the panels of the base or shade?

I found the lamp model on Thingiverse and a free lithophane generator. I generated the STL of the beloved video game character "Donkey Kong" before adding it to the lamp model in SolidWorks. 

The extremely high mesh density of the .STL did not play nice with SolidWorks so I figured out a few mesh settings to allow me to actually manipulate the models:
- Import the STL as a surface grpahic
- Insert -> Mesh -> Decimate Mesh so the overall feature count is <=5,000 (depending on your computer specs)
- Export as new STL

Then you can edit lithophane STL with only minor issues extruding cuts through complex surface geometries. With complex geometries, SolidWorks will crash if extruding completely through certain areas.

I needed to cut extrude through the lithophane and generate planes in certain areas to fit the dimensions of the lamp panels. To work around this crashing error, I cut extrude to leave a small bridge of material between panels that would overlap with geometries in the lamp shade anyway.

I joined the two parts (panel-adjusted lithophane and lamp geometries) in an assembly before exporting to a final STL.

I set up the print and waited ~11 hours to find that my print bed was again a limiting factor in creating a "successful" lamp. Everything printed smoothly but the panels were far too thick in order to fold. The thinness of the creases were still too thick to fold. My lamp print ended up cracking as I attempted to fold it.

Without a large-format printer I decided to call it a time for this project.

Things I learned:
- SolidWorks STL manipulation
- 3D print tuning
- FDM printing boundaries