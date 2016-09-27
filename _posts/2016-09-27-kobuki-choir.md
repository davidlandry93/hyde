---
title: The Kobuki Choir
published: true
categories: projects
layout: post
---

As TAs for
the
[mobile robotics course](http://www2.ift.ulaval.ca/~pgiguere/cours/IntroRobotique/index.html) here
at Université Laval, my colleague and I were responsible for building a new
fleet of robots for the labs last summer. We were going to build robots based on the [kobuki](http://kobuki.yujinrobot.com/) platform for this purpose. Dealing with quotes and POs disappearing orders was
a lot of learning, but we were able to assemble the robots (almost) in time for the beginning 
of the semester. 

The shelves holding the finally assembled robots was quite a sight, and as any good grad students
we decided to put it to a good use... by making a Kobuki choir. Here's a video of the choir 
playing *Good Vibrations*, from the *Beach Boys*.


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
