---
title: 3D Printing "Pre-Creased" Origami Crease Patterns
author: Sam Johnson
blurb: Is there an easier way to create complex origami?
layout: blog
image: plasticorigami1.png
---
## Project Details:
#### Co: Me <br>Supervisor: Me <br>Dates Active: December 2021
<br>
After being introduced to origami when I was 6 by a book by Robert J. Lang, I've evolved to explore more complex origami that involves pre-creasing designs to a crease pattern before collapsing them by folding each pre-made crease in a specific order.
The process of pre-creasing can be extremely tedious, taking hours to make hundreds of folds while weighing the risk of human error. 

<img src="\media\Project Pics 2021\PlasticOrigami\precreasesteps.PNG" alt="26 steps of pre creasing before folding the actual model..."/>
<img src="\media\Project Pics 2021\PlasticOrigami\dollarkoi.jpg" alt="A complex origami requiring a crease pattern."/>

Mistakes add up and inaccuracies can turn your art project into plain recycling.

To leapfrog the step of pre-creasing, I decided to create my own "pre-creased paper" by modeling a thin plane in SolidWorks and extruding even thinner cuts along the crease pattern. The specific model I decided to craft is called "Spring Into Action" by Jeff Beynon.

<img src="\media\Project Pics 2021\PlasticOrigami\springintoaction.jpg" alt="Paper model in question"/>

I was only able to print ~1/6th of the model due to size limitations of my trusty Prusa Mini.

For v0 of the plastic "Spring into Action", the Prusa Slicer Settings were set to:
- 2 bottom layer at 0.05mm.
- 2 extruded layers at 0.05mm each.

<img src="\media\Project Pics 2021\PlasticOrigami\plasticorigami1.png" alt=""/>
<img src="\media\Project Pics 2021\PlasticOrigami\springintoaction.png" alt=""/>

Results: Print bed isn't always completely level or adhesion in certain areas isn't always as good--this is extremely important when printing thin layers that are critical to the form and function of your product.

<img src="\media\Project Pics 2021\PlasticOrigami\plasticorigami3.png" alt="Plastic Sheet of *paper* "/>

I washed the print bed with soap and water to get rid of any oil that wouldn't allow the critical-to-function 1st layer to adhere.

For v1 of the plastic "Spring into Action", the Prusa Slicer Settings were set to:
- 1 bottom layer at 0.05mm.
- 1 extruded layers at 0.05mm each.

The result when collapsing was a MUCH thinner paper that responded more easily to folding. I was able to add another 2 "rings" to the model which was very satisfying.

<img src="\media\Project Pics 2021\PlasticOrigami\spring2.jpeg" alt="Fixed!"/>

I sent my results to Robert J. Lang himself while inquiring if he's worked on anything similar. <img src="\media\Project Pics 2021\PlasticOrigami\robertjlangresponse.PNG" alt="star struck!"/>
[He replied with a link to his Origami lamp that he designed](https://www.thingiverse.com/thing:3896846). 

This piqued another thought of curiosity...What if I modeled a lithophane onto the surface of this lamp and created a custom graphic to the panels of the base or shade?

I found the lamp model on Thingiverse and a free lithophane generator. I generated the STL of the beloved video game character "Donkey Kong" before adding it to the lamp model in SolidWorks. 

<img src="\media\Project Pics 2021\PlasticOrigami\dklithophane.PNG" alt="Donkey Kong December"/>

The extremely high mesh density of the .STL did not play nice with SolidWorks so I figured out a few mesh settings to allow me to actually manipulate the models:
- Import the STL as a surface grpahic
- Insert -> Mesh -> Decimate Mesh so the overall feature count is <=5,000 (depending on your computer specs)
- Export as new STL

Then you can edit lithophane STL with only minor issues extruding cuts through complex surface geometries. With complex geometries, SolidWorks will crash if extruding completely through certain areas.

I needed to cut extrude through the lithophane and generate planes in certain areas to fit the dimensions of the lamp panels. To work around this crashing error, I cut extrude to leave a small bridge of material between panels that would overlap with geometries in the lamp shade anyway.

I joined the two parts (panel-adjusted lithophane and lamp geometries) in an assembly before exporting to a final STL.

<img src="\media\Project Pics 2021\PlasticOrigami\dksolidworks.PNG" alt="Lithophane adjusted STL"/>

I set up the print and waited ~8 hours to find that my print bed was again a limiting factor in creating a "successful" lamp. Everything printed smoothly but the panels were far too thick in order to fold. The thinness of the creases were still too thick to fold. My lamp print ended up cracking as I attempted to fold it. The base layer was too thick.

I adjusted the 3D model such that the base layer of plastic was only 0.05mm, exactly like the "Spring into Action" model. After printing, it successfully collapsed.

<img src="\media\Project Pics 2021\PlasticOrigami\dk1.png" alt="Flat Lithophane Lamp"/>
<img src="\media\Project Pics 2021\PlasticOrigami\dk2.png" alt="Folded Lithophane Lamp"/>

Things I learned:
- SolidWorks STL manipulation
- FDM print tuning

Other applications of 3D printing origami is creating a low cost method to "test" folds. There are extremely intricate crease patterns on some models such as the scales of Ryujin 2.1, a Chinese style dragon designed by Kamiya Satoshi. Folders that attempt this model must use specific low-thickness paper that is malleable but also rigid enough to keep shape and not tear. These materials can get expensive--it might be benefical if folders are able to practice collapsing intricate folds on low-risk materials that are also easily replicable or iterable (with CAD).  
