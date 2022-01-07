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

### 1. I would have to send the bot the link of the video I was currently watching and the timestamp of the video where/when I wanted it to resume playing.

I explored "true" text message API options like twilio but did not want to pay any premium for this app.

I worked around the above issue by using gmail and a free email API that would allow the bot to sign in to user accounts and manipulate emails within inboxes.

I set up a new email to act as the "server" or internet communication liason between my phone and my computer. I wrote the following code and adjusted the email account's security preferences within google to allow the bot to process any incoming messages.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">email</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">imaplib</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">webbrowser</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">re</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">time</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">urllib.request</span>

<span style="color: #008800; font-weight: bold">from</span> <span style="color: #0e84b5; font-weight: bold">plyer</span> <span style="color: #008800; font-weight: bold">import</span> notification

<span style="color: #008800; font-weight: bold">def</span> <span style="color: #0066BB; font-weight: bold">application</span>():
    <span style="color: #888888">#credentials</span>
    username <span style="color: #333333">=</span><span style="background-color: #fff0f0">&quot;YOUR EMAIL HERE@gmail.com&quot;</span>        <span style="color: #888888"># Enter your Email username here!!!</span>

    <span style="color: #888888">#generated app password</span>
    app_password<span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;YOUR PASSWORD&quot;</span>                      <span style="color: #888888"># Enter Your Email password here!!!</span>

    <span style="color: #888888"># Phone number</span>
    phone_number <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;1YOUR PHONE NUMBER&quot;</span>                   <span style="color: #888888"># Enter your Phone number here!!! 1(XXX)-(XXXX) No spaces or parenthesis.</span>

    <span style="color: #888888"># Gmail API Hosting: https://www.systoolsgroup.com/imap/</span>
    gmail_host<span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;imap.gmail.com&#39;</span>

    <span style="color: #888888">#set connection</span>
    mail <span style="color: #333333">=</span> imaplib<span style="color: #333333">.</span>IMAP4_SSL(gmail_host, <span style="color: #0000DD; font-weight: bold">993</span>)

    <span style="color: #888888">#login</span>
    mail<span style="color: #333333">.</span>login(username, app_password)

    <span style="color: #888888">#select inbox</span>
    mail<span style="color: #333333">.</span>select(<span style="background-color: #fff0f0">&quot;INBOX&quot;</span>)
</pre></div>


I then created a new contact in my iPhone with only the email filled in. Now when I text the contact, it sends a .txt file to the email containing any text or image information I had included from my phone.

### 2. The bot would process the text

The next step would be to process this text.

I decided to try and open a plain web URL which worked! I kept this conditional in the program--so now that whenever I text my phone a link, it would automatically open it in a web browser on my PC.

But coming back on track, I needed it to open YouTube videos specifically. I created a conditional to read the funky shortened YouTube url and to open it in a browser.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%">    <span style="color: #888888"># count unread emails</span>
    return_code, data <span style="color: #333333">=</span> mail<span style="color: #333333">.</span>search(<span style="color: #007020">None</span>, <span style="background-color: #fff0f0">&#39;UnSeen&#39;</span>)
    mail_ids <span style="color: #333333">=</span> data[<span style="color: #0000DD; font-weight: bold">0</span>]<span style="color: #333333">.</span>decode()
    id_list <span style="color: #333333">=</span> mail_ids<span style="color: #333333">.</span>split()
    first_email_id <span style="color: #333333">=</span> <span style="color: #007020">int</span>(id_list[<span style="color: #0000DD; font-weight: bold">0</span>])
    latest_email_id <span style="color: #333333">=</span> <span style="color: #007020">int</span>(id_list[<span style="color: #333333">-</span><span style="color: #0000DD; font-weight: bold">1</span>])

    <span style="color: #888888">#select specific mails</span>
    _, selected_mails <span style="color: #333333">=</span> mail<span style="color: #333333">.</span>search(<span style="color: #007020">None</span>, <span style="background-color: #fff0f0">&#39;(FROM &quot;+&#39;</span><span style="color: #333333">+</span>phone_number<span style="color: #333333">+</span><span style="background-color: #fff0f0">&#39;@mailmymobile.net &quot;)&#39;</span>, <span style="background-color: #fff0f0">&#39;unseen&#39;</span>)  <span style="color: #888888"># You may have to change this code to match the email address of your phone number </span>

    <span style="color: #888888">#total number of mails from specific user</span>
    <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Total Unseen Messages from &quot;</span><span style="color: #333333">+</span> phone_number, <span style="color: #007020">len</span>(selected_mails[<span style="color: #0000DD; font-weight: bold">0</span>]<span style="color: #333333">.</span>split()))

    <span style="color: #008800; font-weight: bold">for</span> num <span style="color: #000000; font-weight: bold">in</span> selected_mails[<span style="color: #0000DD; font-weight: bold">0</span>]<span style="color: #333333">.</span>split():
        _, data <span style="color: #333333">=</span> mail<span style="color: #333333">.</span>fetch(num, <span style="background-color: #fff0f0">&#39;(RFC822)&#39;</span>)
        _, bytes_data <span style="color: #333333">=</span> data[<span style="color: #0000DD; font-weight: bold">0</span>]

        <span style="color: #888888">#convert the byte data to message</span>
        email_message <span style="color: #333333">=</span> email<span style="color: #333333">.</span>message_from_bytes(bytes_data)
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;</span><span style="color: #666666; font-weight: bold; background-color: #fff0f0">\n</span><span style="background-color: #fff0f0">===========================================&quot;</span>)

        <span style="color: #888888">#access data</span>
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Subject: &quot;</span>,email_message[<span style="background-color: #fff0f0">&quot;subject&quot;</span>])
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;To:&quot;</span>, email_message[<span style="background-color: #fff0f0">&quot;to&quot;</span>])
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;From: &quot;</span>,email_message[<span style="background-color: #fff0f0">&quot;from&quot;</span>])
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Date: &quot;</span>,email_message[<span style="background-color: #fff0f0">&quot;date&quot;</span>])
        <span style="color: #008800; font-weight: bold">for</span> part <span style="color: #000000; font-weight: bold">in</span> email_message<span style="color: #333333">.</span>walk():
            <span style="color: #008800; font-weight: bold">if</span> part<span style="color: #333333">.</span>get_content_type()<span style="color: #333333">==</span><span style="background-color: #fff0f0">&quot;text/plain&quot;</span> <span style="color: #000000; font-weight: bold">or</span> part<span style="color: #333333">.</span>get_content_type()<span style="color: #333333">==</span><span style="background-color: #fff0f0">&quot;text/html&quot;</span>:
                message <span style="color: #333333">=</span> part<span style="color: #333333">.</span>get_payload(decode<span style="color: #333333">=</span><span style="color: #007020">True</span>)
                <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Message: </span><span style="color: #666666; font-weight: bold; background-color: #fff0f0">\n</span><span style="background-color: #fff0f0">&quot;</span>, message<span style="color: #333333">.</span>decode())
                <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;==========================================</span><span style="color: #666666; font-weight: bold; background-color: #fff0f0">\n</span><span style="background-color: #fff0f0">&quot;</span>)
                
                link_pattern <span style="color: #333333">=</span> re<span style="color: #333333">.</span>compile(<span style="background-color: #fff0f0">r&#39;(?P&lt;url&gt;https?://[^\s]+)&#39;</span>)
                search <span style="color: #333333">=</span> link_pattern<span style="color: #333333">.</span>search(message<span style="color: #333333">.</span>decode())

                link_pattern <span style="color: #333333">=</span> re<span style="color: #333333">.</span>compile(<span style="background-color: #fff0f0">r&#39;http(?:s?):\/\/(?:www\.)?youtu(?:be\.com\/watch\?v=|\.be\/)([\w\-\_]*)(&amp;(amp;)?‌​[\w\?‌​=]*)?&#39;</span>)
                search2 <span style="color: #333333">=</span> link_pattern<span style="color: #333333">.</span>search(message<span style="color: #333333">.</span>decode())

                <span style="color: #008800; font-weight: bold">if</span> search <span style="color: #000000; font-weight: bold">is</span> <span style="color: #000000; font-weight: bold">not</span> <span style="color: #007020">None</span>:
                    <span style="color: #008800; font-weight: bold">if</span> search2 <span style="color: #000000; font-weight: bold">is</span> <span style="color: #000000; font-weight: bold">not</span> <span style="color: #007020">None</span>: <span style="color: #888888"># Checks if it&#39;s a YouTube Link</span>
                        title <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;YouTube Link received!&#39;</span>
                        message <span style="color: #333333">=</span> search2<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>)
                        notification<span style="color: #333333">.</span>notify(title <span style="color: #333333">=</span> title,
                                            message <span style="color: #333333">=</span> message,
                                            app_icon <span style="color: #333333">=</span> <span style="color: #007020">None</span>,
                                            timeout <span style="color: #333333">=</span> <span style="color: #0000DD; font-weight: bold">4</span>,
                                            toast <span style="color: #333333">=</span> <span style="color: #007020">False</span>)
                        
                        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Link found! -&gt; &quot;</span> <span style="color: #333333">+</span> search2<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>))

                        <span style="color: #888888"># url of the video</span>
                        url <span style="color: #333333">=</span> search2<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>)<span style="color: #333333">.</span>replace(<span style="background-color: #fff0f0">&#39;https://youtu.be/&#39;</span>, <span style="background-color: #fff0f0">&#39;&#39;</span>)
</pre></div>

This worked! But as of December 2021, YouTube disabled the autoplay feature AND the ability to easily share timestamps on mobile. I wanted the "continue on PC" process to be as seamless as possible.

### 3. The bot would open some kind of media player to play the video.

I first tried using VLC media player to open the YouTube video. This sort of worked but because VLC opened the video as a "stream", there was no way to pause, play, or scrub through the video.

With a bit of help from google, I found that if I embed the video in a frame within a browser, I'd be able to set it to autoplay, although it would only work without sound. I figured I could just switch the sound on via code immediately after it autplayed.
<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%">                <span style="color: #888888"># *** OPEN IFRAME IN BROWSER ***</span>
            
                        new_url <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;https://www.youtube.com/embed/&#39;</span><span style="color: #333333">+</span>url<span style="color: #333333">+</span><span style="background-color: #fff0f0">&#39;?autoplay=1&#39;</span>    <span style="color: #888888"># Add autoplay notation at the end of the URL.</span>
                                                                                        <span style="color: #888888"># Make sure to change settings in your web browser to allow autoplay as well.</span>
                        <span style="color: #008800; font-weight: bold">print</span>(new_url) <span style="color: #888888"># Print the URL to the shell for confirmation.</span>

                        index <span style="color: #333333">=</span> <span style="color: #007020">open</span>(<span style="background-color: #fff0f0">&quot;web_iframe_youtube.html&quot;</span>)<span style="color: #333333">.</span>read()<span style="color: #333333">.</span>format(video_url<span style="color: #333333">=</span>new_url) <span style="color: #888888"># opens the HTML Document as a long string. Looks for the {video_url} tag.</span>
                                                                                                 <span style="color: #888888"># Sets the {video_url} tag to the new URL as read from the email.</span>
                        <span style="color: #008800; font-weight: bold">print</span>(index)  <span style="color: #888888">#print new hyper-text-markup as confirmation.</span>

                        <span style="color: #007020">file</span> <span style="color: #333333">=</span> <span style="color: #007020">open</span>(<span style="background-color: #fff0f0">&quot;web_iframe_youtube.html&quot;</span>,<span style="background-color: #fff0f0">&quot;w&quot;</span>)      <span style="color: #888888"># Open the html file that hosts the video</span>
                        <span style="color: #007020">file</span><span style="color: #333333">.</span>write(index)                               <span style="color: #888888"># Write the new text (with the new video URL) to the web page.</span>
                        <span style="color: #007020">file</span><span style="color: #333333">.</span>close()

                        webbrowser<span style="color: #333333">.</span>open(<span style="background-color: #fff0f0">&quot;web_iframe_youtube.html&quot;</span>, new <span style="color: #333333">=</span> <span style="color: #0000DD; font-weight: bold">0</span>) <span style="color: #888888"># Open the video web page in a new browser tab</span>

                        time<span style="color: #333333">.</span>sleep(<span style="color: #0000DD; font-weight: bold">10</span>)  <span style="color: #888888"># wait 10 seconds for web page to load. If the video URL variable resets (see following) before the page loads, the video will not play.</span>

                        <span style="color: #888888"># Reset the video URL variable within the html file that hosts the video</span>
                        html_str <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;&quot;&quot;&lt;!DOCTYPE html&gt;</span>
<span style="background-color: #fff0f0">                        &lt;html&gt;</span>
<span style="background-color: #fff0f0">                                &lt;body&gt;</span>
<span style="background-color: #fff0f0">                                        &lt;center&gt;</span>
<span style="background-color: #fff0f0">                                        &lt;iframe width=&quot;1280&quot; height=&quot;720&quot; src=&quot;{video_url}&quot;&gt;</span>
<span style="background-color: #fff0f0">                                        &lt;/iframe&gt;</span>
<span style="background-color: #fff0f0">                                        &lt;/center&gt;</span>
<span style="background-color: #fff0f0">                                &lt;/body&gt;</span>
<span style="background-color: #fff0f0">                        &lt;/html&gt; &quot;&quot;&quot;</span>

                        <span style="color: #888888"># Open and write the new text</span>
                        <span style="color: #007020">file</span> <span style="color: #333333">=</span> <span style="color: #007020">open</span>(<span style="background-color: #fff0f0">&quot;web_iframe_youtube.html&quot;</span>,<span style="background-color: #fff0f0">&quot;w&quot;</span>)
                        <span style="color: #007020">file</span><span style="color: #333333">.</span>write(html_str)
                        <span style="color: #007020">file</span><span style="color: #333333">.</span>close()

                        <span style="color: #888888"># Shell Confirmation</span>
                        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;html file has been reset&quot;</span>)
                        
                    <span style="color: #008800; font-weight: bold">else</span>:
                        title <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;Web Link received!&#39;</span>
                        message <span style="color: #333333">=</span> search<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>)
                        notification<span style="color: #333333">.</span>notify(title <span style="color: #333333">=</span> title,
                                            message <span style="color: #333333">=</span> message,
                                            app_icon <span style="color: #333333">=</span> <span style="color: #007020">None</span>,
                                            timeout <span style="color: #333333">=</span> <span style="color: #0000DD; font-weight: bold">4</span>,
                                            toast <span style="color: #333333">=</span> <span style="color: #007020">False</span>)
                        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Link found! -&gt; &quot;</span> <span style="color: #333333">+</span> search<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>))
                        webbrowser<span style="color: #333333">.</span>open(search<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>))
                    
                <span style="color: #008800; font-weight: bold">else</span>:
                    <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;No web links were found.&quot;</span>)                

                <span style="color: #008800; font-weight: bold">break</span>
</pre></div>
   
It works!

<img src="\media\Project Pics 2021\PlasticOrigami\dollarkoi.jpg" alt="Case in point"/>

### 4. The bot needs to repeat the process and continue checking for emails
<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">while</span> <span style="color: #0000DD; font-weight: bold">1</span>:
    application()
    time<span style="color: #333333">.</span>sleep(<span style="color: #0000DD; font-weight: bold">10</span>)
</pre></div>

Things I learned:
- Various elements of Python IoT scripting

Full Code:
<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">email</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">imaplib</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">webbrowser</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">re</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">time</span>
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">urllib.request</span>

<span style="color: #008800; font-weight: bold">from</span> <span style="color: #0e84b5; font-weight: bold">plyer</span> <span style="color: #008800; font-weight: bold">import</span> notification

<span style="color: #008800; font-weight: bold">def</span> <span style="color: #0066BB; font-weight: bold">application</span>():
    <span style="color: #888888">#credentials</span>
    username <span style="color: #333333">=</span><span style="background-color: #fff0f0">&quot;YOUR EMAIL HERE@gmail.com&quot;</span>        <span style="color: #888888"># Enter your Email username here!!!</span>

    <span style="color: #888888">#generated app password</span>
    app_password<span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;YOUR PASSWORD&quot;</span>                      <span style="color: #888888"># Enter Your Email password here!!!</span>

    <span style="color: #888888"># Phone number</span>
    phone_number <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;1YOUR PHONE NUMBER&quot;</span>                   <span style="color: #888888"># Enter your Phone number here!!! 1(XXX)-(XXXX) No spaces or parenthesis.</span>

    <span style="color: #888888"># Gmail API Hosting: https://www.systoolsgroup.com/imap/</span>
    gmail_host<span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;imap.gmail.com&#39;</span>

    <span style="color: #888888">#set connection</span>
    mail <span style="color: #333333">=</span> imaplib<span style="color: #333333">.</span>IMAP4_SSL(gmail_host, <span style="color: #0000DD; font-weight: bold">993</span>)

    <span style="color: #888888">#login</span>
    mail<span style="color: #333333">.</span>login(username, app_password)

    <span style="color: #888888">#select inbox</span>
    mail<span style="color: #333333">.</span>select(<span style="background-color: #fff0f0">&quot;INBOX&quot;</span>)

    <span style="color: #888888"># count unread emails</span>
    return_code, data <span style="color: #333333">=</span> mail<span style="color: #333333">.</span>search(<span style="color: #007020">None</span>, <span style="background-color: #fff0f0">&#39;UnSeen&#39;</span>)
    mail_ids <span style="color: #333333">=</span> data[<span style="color: #0000DD; font-weight: bold">0</span>]<span style="color: #333333">.</span>decode()
    id_list <span style="color: #333333">=</span> mail_ids<span style="color: #333333">.</span>split()
    first_email_id <span style="color: #333333">=</span> <span style="color: #007020">int</span>(id_list[<span style="color: #0000DD; font-weight: bold">0</span>])
    latest_email_id <span style="color: #333333">=</span> <span style="color: #007020">int</span>(id_list[<span style="color: #333333">-</span><span style="color: #0000DD; font-weight: bold">1</span>])

    <span style="color: #888888">#select specific mails</span>
    _, selected_mails <span style="color: #333333">=</span> mail<span style="color: #333333">.</span>search(<span style="color: #007020">None</span>, <span style="background-color: #fff0f0">&#39;(FROM &quot;+&#39;</span><span style="color: #333333">+</span>phone_number<span style="color: #333333">+</span><span style="background-color: #fff0f0">&#39;@mailmymobile.net &quot;)&#39;</span>, <span style="background-color: #fff0f0">&#39;unseen&#39;</span>)  <span style="color: #888888"># You may have to change this code to match the email address of your phone number </span>

    <span style="color: #888888">#total number of mails from specific user</span>
    <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Total Unseen Messages from &quot;</span><span style="color: #333333">+</span> phone_number, <span style="color: #007020">len</span>(selected_mails[<span style="color: #0000DD; font-weight: bold">0</span>]<span style="color: #333333">.</span>split()))

    <span style="color: #008800; font-weight: bold">for</span> num <span style="color: #000000; font-weight: bold">in</span> selected_mails[<span style="color: #0000DD; font-weight: bold">0</span>]<span style="color: #333333">.</span>split():
        _, data <span style="color: #333333">=</span> mail<span style="color: #333333">.</span>fetch(num, <span style="background-color: #fff0f0">&#39;(RFC822)&#39;</span>)
        _, bytes_data <span style="color: #333333">=</span> data[<span style="color: #0000DD; font-weight: bold">0</span>]

        <span style="color: #888888">#convert the byte data to message</span>
        email_message <span style="color: #333333">=</span> email<span style="color: #333333">.</span>message_from_bytes(bytes_data)
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;</span><span style="color: #666666; font-weight: bold; background-color: #fff0f0">\n</span><span style="background-color: #fff0f0">===========================================&quot;</span>)

        <span style="color: #888888">#access data</span>
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Subject: &quot;</span>,email_message[<span style="background-color: #fff0f0">&quot;subject&quot;</span>])
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;To:&quot;</span>, email_message[<span style="background-color: #fff0f0">&quot;to&quot;</span>])
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;From: &quot;</span>,email_message[<span style="background-color: #fff0f0">&quot;from&quot;</span>])
        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Date: &quot;</span>,email_message[<span style="background-color: #fff0f0">&quot;date&quot;</span>])
        <span style="color: #008800; font-weight: bold">for</span> part <span style="color: #000000; font-weight: bold">in</span> email_message<span style="color: #333333">.</span>walk():
            <span style="color: #008800; font-weight: bold">if</span> part<span style="color: #333333">.</span>get_content_type()<span style="color: #333333">==</span><span style="background-color: #fff0f0">&quot;text/plain&quot;</span> <span style="color: #000000; font-weight: bold">or</span> part<span style="color: #333333">.</span>get_content_type()<span style="color: #333333">==</span><span style="background-color: #fff0f0">&quot;text/html&quot;</span>:
                message <span style="color: #333333">=</span> part<span style="color: #333333">.</span>get_payload(decode<span style="color: #333333">=</span><span style="color: #007020">True</span>)
                <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Message: </span><span style="color: #666666; font-weight: bold; background-color: #fff0f0">\n</span><span style="background-color: #fff0f0">&quot;</span>, message<span style="color: #333333">.</span>decode())
                <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;==========================================</span><span style="color: #666666; font-weight: bold; background-color: #fff0f0">\n</span><span style="background-color: #fff0f0">&quot;</span>)
                
                link_pattern <span style="color: #333333">=</span> re<span style="color: #333333">.</span>compile(<span style="background-color: #fff0f0">r&#39;(?P&lt;url&gt;https?://[^\s]+)&#39;</span>)
                search <span style="color: #333333">=</span> link_pattern<span style="color: #333333">.</span>search(message<span style="color: #333333">.</span>decode())

                link_pattern <span style="color: #333333">=</span> re<span style="color: #333333">.</span>compile(<span style="background-color: #fff0f0">r&#39;http(?:s?):\/\/(?:www\.)?youtu(?:be\.com\/watch\?v=|\.be\/)([\w\-\_]*)(&amp;(amp;)?‌​[\w\?‌​=]*)?&#39;</span>)
                search2 <span style="color: #333333">=</span> link_pattern<span style="color: #333333">.</span>search(message<span style="color: #333333">.</span>decode())

                <span style="color: #008800; font-weight: bold">if</span> search <span style="color: #000000; font-weight: bold">is</span> <span style="color: #000000; font-weight: bold">not</span> <span style="color: #007020">None</span>:
                    <span style="color: #008800; font-weight: bold">if</span> search2 <span style="color: #000000; font-weight: bold">is</span> <span style="color: #000000; font-weight: bold">not</span> <span style="color: #007020">None</span>: <span style="color: #888888"># Checks if it&#39;s a YouTube Link</span>
                        title <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;YouTube Link received!&#39;</span>
                        message <span style="color: #333333">=</span> search2<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>)
                        notification<span style="color: #333333">.</span>notify(title <span style="color: #333333">=</span> title,
                                            message <span style="color: #333333">=</span> message,
                                            app_icon <span style="color: #333333">=</span> <span style="color: #007020">None</span>,
                                            timeout <span style="color: #333333">=</span> <span style="color: #0000DD; font-weight: bold">4</span>,
                                            toast <span style="color: #333333">=</span> <span style="color: #007020">False</span>)
                        
                        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Link found! -&gt; &quot;</span> <span style="color: #333333">+</span> search2<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>))

                        <span style="color: #888888"># url of the video</span>
                        url <span style="color: #333333">=</span> search2<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>)<span style="color: #333333">.</span>replace(<span style="background-color: #fff0f0">&#39;https://youtu.be/&#39;</span>, <span style="background-color: #fff0f0">&#39;&#39;</span>)
                        
                <span style="color: #888888"># *** OPEN IFRAME IN BROWSER ***</span>
            
                        new_url <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;https://www.youtube.com/embed/&#39;</span><span style="color: #333333">+</span>url<span style="color: #333333">+</span><span style="background-color: #fff0f0">&#39;?autoplay=1&#39;</span>    <span style="color: #888888"># Add autoplay notation at the end of the URL.</span>
                                                                                        <span style="color: #888888"># Make sure to change settings in your web browser to allow autoplay as well.</span>
                        <span style="color: #008800; font-weight: bold">print</span>(new_url) <span style="color: #888888"># Print the URL to the shell for confirmation.</span>

                        index <span style="color: #333333">=</span> <span style="color: #007020">open</span>(<span style="background-color: #fff0f0">&quot;web_iframe_youtube.html&quot;</span>)<span style="color: #333333">.</span>read()<span style="color: #333333">.</span>format(video_url<span style="color: #333333">=</span>new_url) <span style="color: #888888"># opens the HTML Document as a long string. Looks for the {video_url} tag.</span>
                                                                                                 <span style="color: #888888"># Sets the {video_url} tag to the new URL as read from the email.</span>
                        <span style="color: #008800; font-weight: bold">print</span>(index)  <span style="color: #888888">#print new hyper-text-markup as confirmation.</span>

                        <span style="color: #007020">file</span> <span style="color: #333333">=</span> <span style="color: #007020">open</span>(<span style="background-color: #fff0f0">&quot;web_iframe_youtube.html&quot;</span>,<span style="background-color: #fff0f0">&quot;w&quot;</span>)      <span style="color: #888888"># Open the html file that hosts the video</span>
                        <span style="color: #007020">file</span><span style="color: #333333">.</span>write(index)                               <span style="color: #888888"># Write the new text (with the new video URL) to the web page.</span>
                        <span style="color: #007020">file</span><span style="color: #333333">.</span>close()

                        webbrowser<span style="color: #333333">.</span>open(<span style="background-color: #fff0f0">&quot;web_iframe_youtube.html&quot;</span>, new <span style="color: #333333">=</span> <span style="color: #0000DD; font-weight: bold">0</span>) <span style="color: #888888"># Open the video web page in a new browser tab</span>

                        time<span style="color: #333333">.</span>sleep(<span style="color: #0000DD; font-weight: bold">10</span>)  <span style="color: #888888"># wait 10 seconds for web page to load. If the video URL variable resets (see following) before the page loads, the video will not play.</span>

                        <span style="color: #888888"># Reset the video URL variable within the html file that hosts the video</span>
                        html_str <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;&quot;&quot;&lt;!DOCTYPE html&gt;</span>
<span style="background-color: #fff0f0">                        &lt;html&gt;</span>
<span style="background-color: #fff0f0">                                &lt;body&gt;</span>
<span style="background-color: #fff0f0">                                        &lt;center&gt;</span>
<span style="background-color: #fff0f0">                                        &lt;iframe width=&quot;1280&quot; height=&quot;720&quot; src=&quot;{video_url}&quot;&gt;</span>
<span style="background-color: #fff0f0">                                        &lt;/iframe&gt;</span>
<span style="background-color: #fff0f0">                                        &lt;/center&gt;</span>
<span style="background-color: #fff0f0">                                &lt;/body&gt;</span>
<span style="background-color: #fff0f0">                        &lt;/html&gt; &quot;&quot;&quot;</span>

                        <span style="color: #888888"># Open and write the new text</span>
                        <span style="color: #007020">file</span> <span style="color: #333333">=</span> <span style="color: #007020">open</span>(<span style="background-color: #fff0f0">&quot;web_iframe_youtube.html&quot;</span>,<span style="background-color: #fff0f0">&quot;w&quot;</span>)
                        <span style="color: #007020">file</span><span style="color: #333333">.</span>write(html_str)
                        <span style="color: #007020">file</span><span style="color: #333333">.</span>close()

                        <span style="color: #888888"># Shell Confirmation</span>
                        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;html file has been reset&quot;</span>)
                        
                    <span style="color: #008800; font-weight: bold">else</span>:
                        title <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;Web Link received!&#39;</span>
                        message <span style="color: #333333">=</span> search<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>)
                        notification<span style="color: #333333">.</span>notify(title <span style="color: #333333">=</span> title,
                                            message <span style="color: #333333">=</span> message,
                                            app_icon <span style="color: #333333">=</span> <span style="color: #007020">None</span>,
                                            timeout <span style="color: #333333">=</span> <span style="color: #0000DD; font-weight: bold">4</span>,
                                            toast <span style="color: #333333">=</span> <span style="color: #007020">False</span>)
                        <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;Link found! -&gt; &quot;</span> <span style="color: #333333">+</span> search<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>))
                        webbrowser<span style="color: #333333">.</span>open(search<span style="color: #333333">.</span>group(<span style="color: #0000DD; font-weight: bold">0</span>))
                    
                <span style="color: #008800; font-weight: bold">else</span>:
                    <span style="color: #008800; font-weight: bold">print</span>(<span style="background-color: #fff0f0">&quot;No web links were found.&quot;</span>)                

                <span style="color: #008800; font-weight: bold">break</span>
            
<span style="color: #008800; font-weight: bold">while</span> <span style="color: #0000DD; font-weight: bold">1</span>:
    application()
    time<span style="color: #333333">.</span>sleep(<span style="color: #0000DD; font-weight: bold">10</span>)
</pre></div>
