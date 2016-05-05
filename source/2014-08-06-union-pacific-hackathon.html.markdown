---
title: Union Pacific Hackathon
date: 2014-08-06
tags: hackathon, union pacific
category: hackathon
---

This past weekend, I had the privilege of competing in Union Pacific's first Intern Hackathon. The 24-hour event, filled with teamwork, caffeine, and unhealthy coding binges was, without a doubt, the highlight of my summer.


###Hacking to Safety
After all nine teams set up their battlestations, the Hackathon problems were passed out. Our team chose "The Dangers of Highway-Rail Crossings". The problem listed statistics of the highway-rail crossing accidents that occur each year and greatly stressed the dangers these crossings present.
READMORE

Let me quickly introduce the team.


+ Cindy Chen - Electrical Engineer
+ Flavia Roma - Computer Science Engineer
+ Noah (me) - Computer Science Engineer

Covering hardware, Cindy had experience __programming SDR__ (Software Defined Radio) and was very interested in implementing signal processing into our solution.

Covering software, Flavia had a lot of __Java and scripting experience__, which we knew would help collect and organize any data we were given.

Covering mobile development, I had __iOS and Android experience__, which we knew would make our solution appealing for its ease of use and extendability.

###Our Solution
We called the product __Track Safety__: a three-part safety solution designed to decrease the number of highway-rail crossing accidents each year.

First, an antenna is attached to the raspberry pi, which detects a train's EOT (End of Train signal) sent out every 60 seconds. This signal is used to send information between the end car and the locomotive at a set frequency. We simply listened for this frequency with a specific gain setting, waiting for the RSSI of the signal at that frequency to reach our set value.

Second, a script is executed in response to receiving the EOT that sends an iBeacon advertisement to mobile devices.

Third, nearby iPhones receive a push notification, warning them that a train will be crossing soon and that the area is now dangerous. If a user presses the notification to open the app, he/she will see the phone's current location and all the Union Pacific-owned highway-rail crossings in the state of Nebraska.

Pretty straightforward, right? But given 24 hours and the goal of presenting a live demo, the project quickly became more and more stressful.

####Software Defined Radio

We used GNURadio to implement SDR. Thankfully, Cindy had experience programming custom blocks to interpret the radio signals. Our hope was to run both the SDR receiver and iBeacon BLE advertisements from the raspberry pi, but we were only able to achieve the latter. After reading a handful of tutorials, it seemed that the only way to install GNURadio on Raspibian was to download the source and compile the code with cmake. The source files take 24+ hours to compile, so we decided to run GNURadio from our linux laptop connected to the pi as a temporary solution. We hoped that stressing that this is a Proof of Concept and there is room for extendibility will let this laptop+pi solution stand strong.


####BLE Advertisement

We used a $10 Bluetooth 4.0 USB module powered by BlueZ to advertise iBeacon messages. There are some pretty straightforward tutorials online for getting the pi to send these advertisements. I wrote bash scripts to start and stop the advertisements so that the process would be as automated as possible. The hardest part of this process was testing that the pi was sending the advertisements. Thankfully, I found RadiusNetworks' Locate app, which allowed me to specify custom UUID, major, and minor values. For a free solution, RadiusNetworks' app is a godsend.

####iOS Application

Union Pacific's IT dept. absolutely loves PhoneGap for its ease of use and simple cross-platform solution. We did not use PhoneGap, however, because our main goal was sending a push notification to the user's phone while the application is in the background. There are multiple PhoneGap plugins on GitHub that support iBeacon moitoring and ranging, but from what I can tell, there is not an easy method for implementing background iBeacon monitoring using PhoneGap.

So insead, I used Xcode to program the native application. Starting with RadiusNetworks' background example, I built the app layer by layer.
+ Layer 1 - iBeacon Scanning
+ Layer 2 - Push Notification
+ Layer 3 - Google Map API

pics

###Tips for the Future
The main thing I learned from this event was: __Your presentation will make or break you__. I saw great products flop and I saw not-so-great products look pretty awesome. The key is to tell a memorable story with your product. When you go on stage to present, it will be the very first time the judges see your project. By this time, you are so focused on your solution, that you can easily forget the big picture and may find yourself stressing low-level functions of your product that won't mean much to the judging panel. This doesn't mean keep the back-end a secret -- but be sure to stress __why the back-end is necessary to solve the problem__.

This brings me to my second tip: __Don't waste time on things the audience won't see__. I found myself wasting a lot of time optimising the push notification service on the iOS app. Those 2-3 hours I spent messing with that code added nothing to our final presentation because it was 100% back-end. Our product is a Proof of Concept -- it doesn't matter if there are memory leaks!

###Overview
By the end of the 24 hours, my major complaint was "Why do I have work tomorrow?" It seems really unfair that you lose your whole weekend to a programming event, but I quickly stopped complaining once my head hit the pillow. I highly recommend participating in a Hackathon. I think the best part of an event like this is realising that you were able to team up and create a functioning product in just one day.

[1]:https://twitter.com/NoahTrust