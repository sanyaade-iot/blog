---
layout: post

title: Blink an LED with Javascript
cover_image: blog-cover.jpg

excerpt: Use SparkJS to easily connect to your Spark Core.

author:
  name: Christine Sunu
  twitter: christinesunu
  bio: Office Manager
  image: christine.jpg
---

Hello, friends! Christine here, newcomer to the Spark team. Despite being a javascript [dilettante](http://en.wikipedia.org/wiki/Dilettante), I was pretty excited to start playing with SparkJS, our new javascript library. It's easy to use, and if you're even a little familiar with javascript the code writes itself.

As an intro to SparkJS, I decided to go with the “Hello World” equivalent of the Spark universe: blinking an LED.

I wired my LED to the D0 pin like so:

<div class="full"><img src="{{ site.url }}/images/javascript-led-fritzing.png"></div>

The next thing for me to do (as always) was to connect my Spark Core to my Wi-Fi network. I connected with the Spark CLI. The basics of this are illustrated in the gif below (c/o Zach).

<img src="{{ site.url }}/images/setup.gif">

Connection success! (If you have trouble with this step, it’s good to go [here](http://docs.spark.io/connect/) for help.)

Next, the Javascript. SparkJS can run [in the browser](http://docs.spark.io/javascript/#installation-client-side) or on a server using Node.js; I've chosen the latter. I can install SparkJS with a simple:

```
npm install spark
```

Next, I wrote a script to blink the LED in javascript, based off of the `callFunction()` example in the SparkJS repository. In order to program using SparkJS, make sure you have the [spark module installed through node.](http://docs.spark.io/javascript/)

*NOTE*: This application assumes that you're running the built-in Tinker firmware that is pre-programmed on the Spark Core. If you're not, you can reinstall it with the Spark CLI by typing `spark flash {core_id} tinker`.

Having installed all the things I needed, I wrote a the LED-blinking script below:

<script src="https://gist.github.com/cmsunu28/c20fa5bf6f524f128d64.js"></script>


This may be a little bit overkill in terms of asynchrony handling, but I just wanted to demonstrate that SparkJS lets you use callbacks, promises, events, or any combination thereof.

I also employed `callFunction()` in two different ways: `spark.callFunction(core_id, command, input, callback)` before the device info is retrieved and `core.callFunction(command, input, callback)` after. As you can see, either works -- it just depends on whether you want to use it before or after you retrieve the devices.

This is fun and everything, but to really take advantage of SparkJS, I'd love to do something on the web with an HTTP request. I never check the weather, but I wanted to be reminded to take my umbrella in the case of rain. I decided to have my Core check it for me.

Using the Open Weather Map API and the node request module, I wrote a quick script to check for rain, which I can call once a day using cron. (Weather codes are [here](http://openweathermap.org/weather-conditions) in case you want to write your own script to identify clouds or clear skies!)

Video of result, and code below!

[video]

<script src="https://gist.github.com/cmsunu28/2eb3d875c1418255970c.js"></script>


Documentation on SparkJS is available here:

http://docs.spark.io/javascript/

Let us know what you think and share all your lovely projects on the [Spark Community](https://community.spark.io). Have fun!
