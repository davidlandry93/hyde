---
title: The Kobuki Choir
published: true
categories: projects
layout: post
---

As TAs for
the
[mobile robotics course](http://www2.ift.ulaval.ca/~pgiguere/cours/IntroRobotique/index.html) here
at Université Laval, my colleague and I were responsible of building a new
fleet of robots last summer. We were going to build robots based on
the [Kobuki](http://kobuki.yujinrobot.com/) platform for this purpose. Dealing
with quotes and POs and disappearing orders was a lot of learning, but we were able
to assemble the robots (almost) in time for the beginning of the semester.

The shelves holding the finally assembled robots was quite a sight, and as any good grad student
we decided to put them to a good use... by making a Kobuki choir. Here's a video of the choir 
playing *Good Vibrations*, from the *Beach Boys*. Please excuse the voice over, this is us
discussing the mixing and other things (in French).

<iframe width="560" height="315" src="https://www.youtube.com/embed/EdcHZQI19Hk" frameborder="0" allowfullscreen></iframe>


## How it works

Alexandre started from the top and wrote the (very appropriately named)
`kent_nagano.py` file, containing the logic that would dispatch the individual
notes to the Kobukis. It reads `.midi` files that have been converted to `.xml`
beforehand. We couldn't find a python 3 library that could read `.midi` files.
The `.xml` file contains a series of *start playing this note* and *stop
playing this note* events. The file is parsed, the notes are all combined and
sorted by timestamp. We use the parsing step to do some basic mixing, like 
changing the stave of some tracks, of doubling the melody track to make it 
easier to hear. 


The communication is very straightforward. `kent_nagano` opens TCP
connections to every individual robots. The TCP server on every Kobuki would
accept 2 bytes messages. The first byte tells what note to play, the second byte
is used to tell the kobuki to start or stop playing it. That means the timing of
the notes is handled completely by `kent_nagano`. We did not find that latency
was a problem. The message `0xFFFF` was reserved to tell the Kobuki that the
song is over and that it should get ready to play a new one.


Once the message is sent over the Kobuki's onboard computer, we use the serial
protocol to interact with the mobile platform. The Kobuki accepts messages to
play a note at a certain frequency. Using this message we can only play notes up
to 255 ms long. However by sending the same message repeatedly we can play
longer notes. The other serial message we use is the one for the leds; one of
the led indicates if a TCP connection is established (for debugging purposes).
The red led indicates a note is being played, for that nice Christmas tree
effect.

You can have a look at
the [source code](https://github.com/davidlandry93/choir) if you are
interested. I doubt many people have access to that many Kobukis, but I guess that
the important is that we had a whole lot of fun putting this together.
