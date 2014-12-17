---
layout: post

title: "WarSting: A Wi-Fi detecting hobbit sword"
cover_image: blog-cover.jpg

excerpt: We hacked a toy sword to make a WarDriving hacker... sword.

author:
  name: Zach Supalla
  twitter: zsupalla
  bio: CEO
  image: zach.jpg
---

Today, *The Hobbit: The Battle of Five Armies* hits the theaters. Bilbo, our favorite hairy-footed protagonist, will face formidable foes armed with his mythical sword, Sting.

<div class="full"><img src="{{ site.url }}/images/bilbo-sting.jpg"></div>

Sting's particular magic is that it glows blue whenever orcs or goblins are nearby. This is useful for hobbits, but in today's day and age, a real Sting would be unfortunately boring.

But what if Sting could detect unsecured Wi-Fi networks?

<div class="full"><img src="{{ site.url }}/images/sting-meme.jpg"></div>

To celebrate the launch of the new *Hobbit* flick, we made a version of Sting that turns blue near unsecured Wi-Fi networks. And when you slash the sword, Sting will jump on the network, and publish a message: "{YOUR WI-FI NETWORK} has been vanquished!"

**VIDEO OF THE AWESOMENESS**

This hack is inspired by one of our favorite recent projects, [WarKitteh](http://www.wired.com/2014/08/how-to-use-your-cat-to-hack-your-neighbors-wi-fi/), in which a Siamese cat named Coco was enlisted to wardrive his owner's neighborhood. Hobbits are known to travel further than the typical housecat, and therefore make great wardrivers.

## Step 1: the ingredients

To make your own WarSting, you'll need two things: a [toy Sting](http://www.amazon.com/The-Bridge-Direct-Hobbit-Deluxe/dp/B008914XZA/), and a [Spark Core](https://store.spark.io).

<div class="full"><img src="{{ site.url }}/images/knolling-sting-topdown.jpg"></div>

A toy company named *The Bridge Direct, Inc.* sells (next to Power Rangers and Justin Bieber action figures) [a $29.99 plastic replica Sting sword](http://www.amazon.com/gp/product/B008914XZA/). *WITH LIGHTS AND SOUND!* This is a great hack because:

- It has *lights and sound*. When you press a button, the sword lights up blue, and when you slash the sword, it makes fun slashing sounds. These functions are hackable.
- It's pretty cheap.
- It's a sword.
- It's held together with screws, which gives us access to the internals.
- There's a bit of extra space in the hilt that we can cram stuff into.

The other thing you'll need is a [Spark Core](https://store.spark.io), which is a Wi-Fi dev kit - sort of like a Wi-Fi connected Arduino. It's a reprogrammable chip that has a Wi-Fi network and can interact with sensors and actuators, like the ones in the sword.

<div class="full"><img src="{{ site.url }}/images/core-and-hilt.jpg"></div>

This is what we do, so we have a whole bunch of them sitting around. If you want a Core, you can get them on [our website](https://store.spark.io) for $39 each.

## Step 2: Disassemble the sword

All of the electronics in the sword are contained in the hilt, which can be accessed by unscrewing a couple of screws. Here's what you'll find inside:

<div class="full"><img src="{{ site.url }}/images/closeup-hilt.jpg"></div>

There are basically four components that matter here:

- Two AA batteries, which power the electronics. Every AA battery provides 1.5V, so when two are placed in serial, you've got 3V. If you use [Energizer Ultimate Lithium batteries](http://www.amazon.com/Energizer-L91BP-8-Ultimate-Lithium-Battery/dp/B0000DC4EL/), which run at 1.7V out of the box, you've got 3.4V, which is enough to get a bright blue light from the LEDs (3V will work but the light will be quite dim).
- A couple of blue LEDs that are pointed up into the sword to make it glow
- A button on the front that turns on the sword
- A "vibration switch" that detects when the sword is swung. This is basically a spring inside a metal tube; when you swing the sword, the spring bends and hits the tube around it, which completes a circuit
- A tiny sound system that makes one of a few tinny *SLASH* and *CLANG* sounds when you swing the sword

## Step 3: Splice in the Core

We want the Core to be in control of whether the LEDs are on and whether the little sound circuit is making a sound. We also want it to detect the signal from the vibration switch. Here's a diagram of our circuit:

<div class="full"><img src="{{ site.url }}/images/warsting-schematic.png"></div>

This is an overly simplistic diagram, and isn't a totally accurate picture of what's going on here. We're not hooking up to a single LED; we're hooking into a pre-existing subsystem which actually includes multiple LEDs. And we're also not hooking up to a speaker; we're hooking up to a whole system for producing sounds where simply sending voltage to a black box of a circuit will create a *SLASH* sound.

This hack is pretty straightforward; it's simply a matter of cutting the wires in the sword and soldering the wires to the pins of the Spark Core.


## Step 4: Reprogram the Core with network-vanquishing firmware

We've written a firmware application designed for the WarSting that scans for unsecured networks, makes sounds, blinks the LEDs, and publishes messages from the unsecured network. All in, it's about three hundred lines of code. Here's a sample in a gist:

<script src="https://gist.github.com/zsup/bfa7726adf375f4a744f.js"></script>

In addition to this firmware application, you'll have to include the `wifiscan.h` library, which scans for networks. The complete firmware can be found on our Github repo for WarSting:

[www.github.com/spark/warsting](http://www.github.com/spark/warsting)

## Step 5: Reassemble the sword

Put the sword back together. This is the opposite of step 2.

## Step 6: Vanquish Wi-Fi networks

Power up your new WarSting, and when the sword turns blue, start slashing! If you have a few unsecured networks nearby, WarSting will vanquish them one at a time, until they've all been vanquished, after which the sword will no longer glow blue.

## In conclusion

So there you have it! Enjoy your hobbit journey, and if you're interested in more fun projects, check out the [Spark project site on Hackster](https://spark.hackster.io) for all kinds of inspiration.
