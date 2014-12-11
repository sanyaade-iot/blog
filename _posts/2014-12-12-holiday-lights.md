---
layout: post

title: Holiday Cheer Lights
cover_image: blog-cover.jpg

excerpt: Power your lights with Holiday Cheer from the Internet!

author:
  name: David Middlecamp
  twitter: dmiddlecamp
  bio: Cloud Guy
  image: david.jpg
---

Happy Holidays from Spark!

Last week many of us Sparklers met eachother in person for the first time at our first big holiday party and hackathon!
It was awesome, and I hope you'll get to see all the results of the hackathon soon.  In decorating for the party, Christine
insisted our hacked ladder tree be internet connected, so we set off to work.  Here's what we built:

Internet connected cheer lights and buttons!

Since it was a party, I wanted the lights to be interactive, and not just from anywhere in the room, but from anywhere in the world!
I started with our 


Our firmware needed to be quick and easy to write.  We picked red and green as our base palette, and the firmware simply alternated colors,
randomly picking a low intensity.  The core would subscribe to the public "cheer" event stream, and go crazy when cheer was detected.  We
also built and spread out a few Cores around the office so that anyone hitting a button would generate holiday cheer and make the tree go wild.

You can find more build pictures, and full source code here at 

Happy Holidays!
David