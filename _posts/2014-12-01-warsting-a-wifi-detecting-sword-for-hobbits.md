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

## Step 1: the ingredients

To make your own WarSting, you'll need two things: a [toy Sting](http://www.amazon.com/The-Bridge-Direct-Hobbit-Deluxe/dp/B008914XZA/), and a [Spark Core](https://store.spark.io).

**PICTURE OF SWORD**

A toy company named *The Bridge Direct, Inc.* sells, next to Power Rangers and Justin Bieber action figures, a $29.99 replica plastic Sting sword. *WITH LIGHTS AND SOUND!* This is a great hack because:

- It has lights and sound. When you press a button, the sword lights up blue, and when you slash the sword, it makes fun slashing sounds.
- It's pretty cheap.
- It's a sword.
- It's held together with screws, which gives us access to the internals.
- There's a bit of extra space in the hilt that we can cram stuff into.

The other thing you'll need is a Spark Core, which is a Wi-Fi dev kit - sort of like a Wi-Fi connected Arduino. It's a reprogrammable chip that has a Wi-Fi network and can interact with sensors and actuators, like the ones in the sword.

**PICTURE OF A CORE**

This is what we do, so we have a whole bunch of them sitting around. If you want a Core, you can get them on [our website](https://store.spark.io) for $39 each.

## Step 2: Disassemble the sword

All of the electronics in the sword are contained in the hilt, which can be accessed by unscrewing a couple of screws. Here's what you'll find inside:

**PICTURE OF A CORE**

There are basically four components that matter here:

- Two AA batteries, which power the electronics. Every AA battery provides 1.5V, so when two are placed in serial, you've got 3V.
- A couple of blue LEDs that are pointed up into the sword to make it glow
- A button on the front that turns on the sword
- A "vibration switch" that detects when the sword is swung. This is basically a spring inside a metal tube; when you swing the sword, the spring bends and hits the tube around it, which completes a circuit
- A tiny sound system that makes one of a few tinny *SLASH* and *CLANG* sounds when you swing the sword

## Step 3: Splice in the Core

## Step 4: Reprogram the Core with network-vanquishing firmware

## Step 5: Reassemble the sword

## Step 6: Conquer Wi-Fi networks
