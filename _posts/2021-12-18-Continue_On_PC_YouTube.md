---
title: Building a Pyton Based "Continue on PC" Feature for YouTube
author: Sam Johnson
blurb: Spotify has an amazing feature. YouTube is missing it. Let's change that with Python.
layout: blog
image: 
---
## Project Details:
#### Co: Me <br>Supervisor: Me <br>Dates Active: December 2021
<br>
I use Spotify, a music streaming service very consistently. My favorite feature of the app is the ability to "Continue on PC". I'll be driving in the car with my music playing, then when getting home I can seamlessly switch to playing where I left off on my PC.

I also happen to be an avid user of YouTube, again, consuming content on both my phone and PC. If I decide to use either my phone or PC, it's tedious to switch between the two if I want to watch the same video. There is also a treasure trove of music mixes that are not available on Spotify. If I want to resume playing music on my PC, this app will give me the option to do it on YouTube.

When I move from my phone to my PC I have to:
- Search for the video.
- Find the timestamp of where I left off.

After doing these steps many times, I realized I could break it down further into logical steps and automate it with Python.

In designing a python app/bot to solve this issue, I figured out the following process and wrote code as necessary.

## 1. I would have to send the bot the link of the video I was currently watching and the timestamp of the video where/when I wanted it to resume playing. ##

I explored "true" text message API options like twilio but did not want to pay any premium for this app.

I worked around the above issue by using gmail and a free email API that would allow the bot to sign in to user accounts and manipulate emails within inboxes.

I set up a new email to act as the "server" or internet communication liason between my phone and my computer. I wrote the following code and adjusted the email account's security preferences within google to allow the bot to process any incoming messages.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%">user login code
test
hello world
</pre></div>

I then created a new contact in my iPhone with only the email filled in. Now when I text the contact, it sends a .txt file to the email containing any text or image information I had included from my phone.

## 2. The bot would process the text ##

The next step would be to process this text.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #333333">&gt;</span> include text <span style="color: #000000; font-weight: bold">and</span> code explanation
</pre></div>

I decided to try and open a plain web URL which worked! I kept this conditional in the program--so now that whenever I text my phone a link, it would automatically open it in a web browser on my PC.

But coming back on track, I needed it to open YouTube videos specifically. I created a conditional to read the funky shortened YouTube url and to open it in a browser.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #333333">&gt;</span> include conditional
</pre></div>

This worked! But as of December 2021, YouTube disabled the autoplay feature AND the ability to easily share timestamps on mobile. I wanted the "continue on PC" process to be as seamless as possible.

## 3. The bot would open some kind of media player to play the video. ##

I first tried using VLC media player to open the YouTube video. This sort of worked but because VLC opened the video as a "stream", there was no way to pause, play, or scrub through the video.

With a bit of help from google, I found that if I embed the video in a frame within a browser, I'd be able to set it to autoplay, although it would only work without sound. I figured I could just switch the sound on via code immediately after it autplayed.

It works!

<img src="\media\Project Pics 2021\PlasticOrigami\dollarkoi.jpg" alt="Case in point"/>

## 4. The bot needs to repeat the process and continue checking for emails ##

Things I learned:
- Various elements of Python IoT scripting
