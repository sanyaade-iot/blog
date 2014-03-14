---
layout: post

title: Hacking a Question Block Lamp with the Spark Core
cover_image: blog-cover.jpg

excerpt: A simple hardware hack that turns your Question Block Lamp into a internet-connected task management notifier with the help of Asana and the Spark Core.  

author:
  name: Will Hart
  twitter: brandoaire
  bio: Design Engineer
  image: will.jpg
---

First blog post--woo!

Hello everyone--my name is Will, and I am a Design Engineer/China enthusiast for the Spark team.   I just finished a fun project with the Core, and I'd like to share it with you :-)

A few weeks ago, David, our awesome Senior Software with a borderline diagnosable addiction to Kickstarter, received his [Question Block Lamp](https://www.kickstarter.com/projects/1189253589/the-question-block-lamp) from our fellow hardware compatriots, 8-Bit Lit.  After plugging it in, we immediately realized its potential as a notification endpoint integrated with Spark's task management software of choice, [Asana](https://asana.com).  With a few quick hacks and some help from our community, I was able to make some pretty sweet upgrades:

  - The lamp automatically toggles state when a task is completed by a member of the Spark team through Asana

  - An integrated LCD will display the number of tasks completed today (`Tod:`), the total number of tasks completed by the Spark team (`Tot:`), and a congratulatory phrase for the individual who completed the most recent task.

  - A mute switch for those times when we're being excessively productive ;)

Here's the product of my labors:

<div class="full"><img src="{{ site.url }}/images/question-block-lamp.jpg">
</div>
---
##1. Required Materials
  - [Spark Core](www.spark.io)
  - [Question Block Lamp] (http://www.8bitlit.com/collections/question-block-lamps)
  - [16x2 LCD display (3.3V)] (http://www.seeedstudio.com/depot/LCD-16x2-Characters-White-Text-Blue-Background-p-1612.html?cPath=34_36)
  - [16x2 LCD bezel](http://www.digikey.com/product-search/en?WT.z_header=search_go&lang=en&site=us&keywords=PRD250LPW-ND&x=-1068&y=-51&formaction=on)
  - Small capacitor (0.01nF / 100pF)
  - Small resistor (100R or 220R)
  - [NPN transistor] (https://www.sparkfun.com/products/521)
  - [Rotary potentiometer] (https://www.sparkfun.com/products/9806)
  - [SPDT mute switch] (https://www.sparkfun.com/products/102)
  - [Standoffs and screws] (https://www.sparkfun.com/search/results?term=standoffs)
  - [Hot glue gun](http://bit.ly/Pu0duJ)
  - Screwdriver
  - [Proto- and/or breadboards] (https://www.sparkfun.com/products/8619)
  - [Soldering iron](https://www.sparkfun.com/products/10707)


##2. Hacking the Enclosure

The list of mechanical modifications to the lamp was short.  After using a flathead screwdriver to remove what I decided was the "front" panel, I used a dremel to cut a hole in the display for the LCD.  I mounted the bezel and LCD display using the standoffs, and boom!

The next small modification was to add a SPDT switch into the top face of the lamp so that the wonderful "da-ding" of accomplishment could be silenced if so desired.  I spread a little hot glue on the underside of the switch to keep it in place.

##3. Assembling the Electronics

<div class="full"><img src="{{ site.url }}/images/question-block-electronics.jpg">
</div>

There were three major sub-systems that needed to be wired up on the inside of the lamp.  Let's take 'em one at a time.

###+ Hooking up the LCD

Once the LCD was mounted, the first step was to connect it to the Core.  Fortunately, Spark has a over-achieving [community](http://community.spark.io), and I was able to find an existing entry for hooking up the hardware.  Check out the Fritzing diagram below for wiring up your 16x2 LCD.  I'll cover the software further down:

<div class="full"><img src="{{ site.url }}/images/core-lcd-fritzing.jpg">
</div>

###+ Hooking up the automatic toggle

The next part of the electronics modification was to engineer a way to trigger the capacitive touch sensor of the on-board microcontroller without physically interacting with the lamp.  It turns out, many microcontrollers can be turned into capacitive touch sensors by simply making use of two GPIO pins (one send, one receive), with a high value resistor and capacitive sensor between them.  Arduino has a [great explanation](http://playground.arduino.cc/Main/CapacitiveSensor?from=Main.CapSense#.UyDNa9xLMqw) of this neat configuration, which I highly suggest you check out.

In order to achieve an automatic, instead of manual, capacitive trigger, we simply connect pin A0 on the Core to the base of an NPN transistor through a 220R resistor.  We then connect the emitter to ground, and the collector to a small capacitor.  The additional capacitance provided by the circuit is enough to trigger the mechanism on the Question Block Light's internal PCB, and da-ding! We trigger the lamp.

<div class="full"><img src="{{ site.url }}/images/question-block-toggle.jpg">
</div>

###+ Hooking up the mute switch

The last step was to wire up the mute switch using a simple SPDT switch.  Simply unsolder the wire from "Speaker -" and connect it to one of two adjacent pins on the switch.  On the second pin, wire another jumper back to "Speaker -".

<div class="full"><img src="{{ site.url }}/images/question-block-speaker.jpg">
</div>

##4. Writing the Firmware

I threw together a pretty quick 135-line application that can expose a simple `Spark.function()` called `print_lcd()` that is triggered by an API call from the Spark Cloud.  Whenever the function is triggered, it does the following:

- Parse the incoming string for `today_count`, `total_count`, `user_id`, and `task_name` variables
- Look up the name of the task completer in a hard-coded database, based on the `user_id`
- Randomly select one of ten congratulatory phrases
    - "Good Job,"
    - "High Five"
    - "Nice Work"
    - "Killin It"
    - "Go Get Em"
    - "You's Bad"
    - "Ohhh Yeah"
    - "Hot Stuff"
    - "Well Done"
    - "#WishIWas"
- Toggles the capacitive trigger to change the state of the lamp
- Prints the congratulatory message to the LCD, and plays a "da-ding!"

The firmware also uses the [Liquid Crystal library](https://github.com/technobly/SparkCore-LiquidCrystal) developed by the incomparable [BDub](https://community.spark.io/users/bdub/activity) of [Spark Elite](https://community.spark.io/t/welcome-bdub-and-timb-as-moderators-and-spark-elite/3063) fame.  So, be sure to include the LiquidCrystal.h and LiquidCrystal.cpp files when you flash the firmware to your Core.

The question-block.ino firmware is included in the Gist below:

[https://gist.github.com/brandoaire/9518723](https://gist.github.com/brandoaire/9518723)

##5. Spinning up a Web App with Heroku
