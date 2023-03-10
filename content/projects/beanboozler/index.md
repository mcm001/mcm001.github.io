---
title: "\"Beanboozler\" High-Power Model Rocket (AerospaceNU)"
date: 2022-09-19T13:48:04-05:00
draft: false
author: Matthew Morley
image: /projects/beanboozler/imgs/beanboozler-crmrc-9-17.jpg
tags: [SOLIDWORKS, Rocketry, Avionics, Python]
description:
toc: false
---

Beanboozler was designed to test the custom rocket avionics suite designed by AerospaceNU in flight regimes close to those they'll experience when controlling our eventual liquid-fueled rocket. I lead the design and fabrication, along with small group of teammates.

To achieve these requirements, we designed, built and successfully flew a 2.6in diameter, 5ft tall, fiberglass rocket designed to fly our avionics and data acquisition hardware at speeds up to Mach 1.5. The small rocket size made packaging all of the required electronics a challenge, and we went through multiple iterations before setting on a design. After a successful shakedown flight during Spring 2022, Beanboozler achieved an apogee of 15,584ft and a speed of Mach 1.05 at Lucerne Lake in CA summer of 2022.

Banboozler is my first fiberglass airframe rocket, was my first to fly on an L-class rocket motor, and my first rocket to fly supersonic.

{{< gallery >}} 
    {{< figure src="/projects/beanboozler/imgs/ldrs-40-assembly.jpg" caption="Assembling the rocket motor">}}
    {{< figure src="/projects/beanboozler/imgs/ldrs-40-hero.jpg" caption="Retreating from the rocket">}}
    {{< figure src="/projects/beanboozler/imgs/ldrs-40-launch.jpg" caption="Beanboozler in the Mojave desert">}}
{{< /gallery >}}

Beanboozler's mechanical design was done with a mix of SOLIDWORKS and OpenRocket, with additional fin strength calculations performed with FinSim. The embedded software for the flight computer was written in a mix of C and C++, and the groundstation UI in Python.

{{< youtube vqHFHmUJTq4 >}}

<p class="pt-2"></p>

## Design

<img src="/projects/beanboozler/imgs/openrocket.png" caption="OpenRocket design" width="100%"/>
<p></p>

Beanboozler was designed to carry AerospaceNU's custom flight computer (called the FCB) and a commercial backup computer, a backup GPS tracker, camera, and our nosecone avionics suite -- all inside of a rocket just 2.5in in diameter. The rocket's small size presented unique fabrication and packaging challenges as we balanced battery capacity and telemetry radio placement with design loading constraints.


<img src="/projects/beanboozler/imgs/assembled-sled.jpg" style="width: 70%;">

The main avionics bay (above) holds the FCB (which has a GPS and radio telemetry), as well as a redundant commercial altimeter. The nosecone (below) contains the additional redundant GPS tracker, as well as our nosecone sensor suite including pitot tube to measure rocket velocity, thermocouples to measure aerodynamic heating, as well as IMUs and barometers. 

{{< load-photoswipe >}}
{{< gallery >}} 
    {{< figure src="/projects/beanboozler/imgs/nosecone-assembled.jpg" caption="Assembled nosecone sled">}}
    {{< figure src="/projects/beanboozler/imgs/nc-cad-2.png" caption="Nosecone front view">}}
    {{< figure src="/projects/beanboozler/imgs/nc-cad-1.png" caption="Nosecone back view">}}
{{< /gallery >}}

The avionics bay went through multiple iterations in Solidworks, evolving from a single monolithic 3d-printed brick (left) to a sled-based design (right). A single off-center threaded rod takes the loading from parachute ejection. This increases the off-axis loading on the bay, but gets our threaded rod placed further away from the telemetry antenna (which improves radio range).

{{< gallery >}} 
    {{< figure src="/projects/beanboozler/imgs/ebay-cad-1.png" caption="V1 monolithic design">}}
    {{< figure src="/projects/beanboozler/imgs/ebay-cad-2.png" caption="V2 design">}}
    {{< figure src="/projects/beanboozler/imgs/ebay-cad-3-front.png" caption="V3, front view">}}
    {{< figure src="/projects/beanboozler/imgs/ebay-cad-3.png" caption="V3, back view">}}
{{< /gallery >}}

<!-- The rocket ejection system (black powder charges ignited with electric matches) was ground tested to ensure the rocket would properly seperate in flight. The videos below show the drogue (lower) and main (upper) bays successfully separating with 0.2 and 0.4 grams of black powder. -->

<!-- TODO -- gotta put the videos in here -->
