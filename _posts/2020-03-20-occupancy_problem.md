---
layout: post
title: The Occupancy Problem
---

Occupancy detection is a surprisingly difficult problem. Unless you've tried to solve it yourself, you may not realize why so many have struggled. Let's talk about why.

<video autoplay="" muted="" loop="" playsinline="" class="padded rounded" width="100%">
  <source src="/post_files/doorsummary.mp4" type="video/mp4">
  Sorry, your browser doesn't support embedded videos.
</video>

As humans, we're constantly observing what's happening around us, thinking about it, and then reacting to that stimulus. For example, if you see a tomato flying towards you, you'll process what's happening and then react by ducking. A smart home is no different. All intelligent systems must see, think, and act in that order. Current smart home systems are heavily optimized on acting: turn the lights on, change the temperature, or unlock the door. We still have to see that it's too dark and ask our home to do something for us.

In order to truly automate this workflow, we need the home to see that we're in the dark first. A lux sensor can tell the system that it's dark, but we don't want the lights to turn on for an empty room. How does your home know someone is there?

## Enter the humble motion sensor.

Motion sensors have been around for decades. They use passive infrared (_PIR_) to detect large changes in heat across their field of view. This works very well for detecting when somebody moves, and uses surprisingly little power, so they can last on tiny batteries for over a year.

<img src="/post_files/motion_sensor.jpg" alt="Motion sensor" width="200px" height="150px" />
<p class="caption">You can usually recognize them by their round fresnel lens.</p>

Detecting motion to determine occupancy makes sense on paper, but quickly falls apart in the real world. For example, if you're standing still, the sensor will lose track of you. It's impossible to know if you're still in the room or not, which is why all motion sensors use a timer to reset themselves if no motion is detected for some amount of time. If you've ever had to wildly wave your arms around to turn the lights back on in an office or bathroom, you've experienced the limitation of this approach. It's even worse in the bedroom, where the lights will turn on the middle of the night if you toss over. On the flip side, the sensor has to wait until the timer runs out to be sure the room is empty after you leave, creating a lag in your home's responsiveness.

## Track people with cameras.

If the issue is lack of object permanence, let's use cameras to track people. They can see exactly what's happening, and machine vision algorithms have gotten good enough to accurately identify humans in a video, solving a lot of the false positive issues.

<div class="padded"><img src="/post_files/cameras.jpg" alt="Smart home cameras" class="rounded" /></div>

Unfortunately, this comes at a significant cost to privacy. Few people want a camera watching them sleep or shower. Cameras also lose track of you the moment you walk out of their field of view.

## Track your phone's location.

Hopefully by now, you're seeing that tracking humans is not easy. That's why a lot of people resort to tracking your phone instead. Bluetooth (_BLE_) or Ultra Wideband (_UWB_) beacons ping your phone, telling it where you are based on the closest beacon. This approach is persistent and protects your privacy!

<div class="padded"><img src="/post_files/ble.jpg" alt="Detecting your phone via Bluetooth" class="rounded" /></div>

But what happens if you leave your phone on the charger? Unfortunately, the system falls apart because it's only able to track your phone, not you. It also doesn't work for guests or kids who may not have smartphones.

## Hire a bouncer.

By now, we've seen how motion is not the same thing as occupancy, cameras sacrifice too much privacy, and anything that tracks your phone will eventually fail. If only we could have a bouncer at the door who just told us how many people are in the room...

Well, we can! We can count entries and exits into a room to know how many people are still in the room without ever seeing the room itself.

<video autoplay="" muted="" loop="" playsinline="" class="padded rounded" width="100%">
  <source src="/post_files/doorstats.mp4" type="video/mp4">
  Sorry, your browser doesn't support embedded videos.
</video>

This is the approach we took with [Hiome Door](https://hiome.com). It's the first sensor for your home that can count entries and exits to know the final occupancy state of your room. Hiome works for everyone, including guests and kids, even if you're not carrying anything. And it enables your home to react to you in milliseconds!

To protect privacy even more, we didn't stop there. We also used a thermal sensor to detect heat signatures instead of a camera so that your privacy is protected even in the doorway. Second, we built Hiome with absolutely zero cloud components, so your data stays within your home.

<div class="padded">
  <img src="/post_files/thermal.png" alt="Raw thermal data" class="rounded" />
  <p class="caption">This is everything that Hiome sees.</p>
</div>

Having a good sensor is just the first step in building a truly intelligent home, but it is a crucial one to get right. If you can't see what's happening, it's very difficult to react appropriately.
