---
title: "Level 3 Rocket Design"
date: 2023-09-30T16:50:30-05:00
draft: false
author: Matt Morley
tags:
image: /posts/l3-design/imgs/3d-ork.png
description:
toc:
---

## Overall Design

The rocket design is based on Wildman's 5 inch diameter, fiberglass upscale [Estes Goblin kit](https://wildmanrocketry.com/collections/5-fiberglass/products/goblin-5). The fin shape is adjusted slightly from the kit, and carbon fiber layups added to the fins, to increase stiffness. I created a preliminary OpenRocket model based on the product page with best guesses at mass numbers and dimensions (below).

<img src="/posts/l3-design/imgs/openrocket.png" caption="OpenRocket design" width="100%"/>
<p></p>

The rocket is desiged to _just_ fit a 75mm/4 propellant grain rocket motor. This is the physically smallest motor size that's still technically an M-class, a requirement for the Level 3 certification flight. This does mean I've left myself ~2 inches in which I now need to fit a drogue parachute and recovery charges (which you can see just forward of the end of the motor above). Here are my high-level anticipated flight parameters:

| Parameter | Value |
| --: | :-- |
| Construction                   | 5 in fiberglass airframe |
| Rocket length                   | 61 in          |
| Rocket motor                  | AeroTech M1297-White Lighting (75mm, 4 grains) |
| Weight, wet                   | 10.4 kg          |
| Weight, dry                   | 5.8 kg           |
| Drag coefficient, CD          | 0.54             |
| Rail exit velocity, 10ft rail | 106 ft/s         |
| Maximum altitude              | 9400 ft AGL      |
| Maximum velocity              | 1233 ft/s        |
| Launch acceleration           | 18 G's           |
| Launch stability              | 1.55 Calibers, or 15% overall length    |
| Loaded CG location            | 37.6 in from tip |
| Loaded CP location            | 47 in from tip   |
| Drogue parachute & speed | 24in round, 80 ft/s |
| Main parachute & speed | 60in Iris (toroidal), 18 ft/s   |



The airframe was also roughly mocked up on Onshape using a higher-fidelity model of the rocket motor using manufacturer drawings. This overall just confirms the clearance we saw using OpenRocket. The switch band may also give me 1in extra clearance between motor forward closure and electronics bay as well -- we'll know once the kit arrives.

<p></p>
<img src="/posts/l3-design/imgs/onshape-airframe.png" caption="Onsahpe boilerplate design" width="100%"/>

## Recovery Setup

The rocket has a traditional head-end dual-deployment recovery setup, with a small drogue parachute in the motor section and a main parachute in the nosecone with a 7in-length avionics bay in the coupler. The drogue is a small parachute that deploys at apogee (the highest point of the flight) and reduces the rocket's vertical speed to ~50-100 ft/s. The main parachute is sized so that when it deploys near the ground, the rocket falls at ~20 ft/s. This process is shown in the gallery below for AerospaceNU's TRD from April 2022:

{{< load-photoswipe >}}
{{< gallery >}} 
    {{< figure src="/posts/l3-design/imgs/liftoff.jpg" caption="Liftoff">}}
    {{< figure src="/posts/l3-design/imgs/drogue.jpg" caption="Drogue(s) deployed!">}}
    {{< figure src="/posts/l3-design/imgs/main.jpg" caption="And main out!">}}
{{< /gallery >}}

The 7-inch long avionics bay (the grey cylinder just forward the motor in the picture above) provides sufficient real estate for two redundant dual-deployment recovery electronics as required by NAR for Level 3 certification flights, as well as space for additional payloads including GPS trackers to aid in recovery. Deployment will be controlled by 2 commercial dual-deploy altimeters (probably just Stratologgers?), and will also be test-flying the new LoRa-based miniature GPS trackers designed by me during the summer of 2023.

## Recovery Math

<img style="float: right; padding-left: 1em" src="../imgs/parachute-math.png" width="50%">

To try to get a rough order of magnitude for shock cord sizes, I calculated the force on a parachute that instantly inflated to full size at worst-case descent velocity (right). For our drogue parachute, that's the horizontal velocity of the rocket at apogee, which is influenced by the wind speed and initial launch angle. For our main parachute, it's a pessimistic guess at free-fall velocity. 

Based on this math, I proposed just using 1/4" Wildman Kevlar cord, which is rated to 4000 lb breaking strength, for both drogue and main parachute harnesses. This should be sufficiently overkill for snap loads and withstanding dynamic deployment events.

Most high power dual-deploy rockets also use shear pins (nylon bolts, usually) to hold together rocket sections during ascent, but break when it's time for parachutes to be deployed. To figure out what size/how many shear pins we should use, I assuemd my rocket bays would be perfectly sealed from air pressure changes as we ascend. Using the standard atmospheric model, the pressure difference between sea level and 10,000 ft altitude was determined to be 4.6 psi. Over a 5in-diameter bulkhead, this translates to a force of 90 lbf. 

A common size of shear pin used in hobby rocketry is #4 (~M3 for our metric friends), which shear at approximately 40lb. I proposed using 4x 4-40 shear pins for retaining the drogue and main parachute bays against this pressure difference. Starting points for black powder deployment charge sizing (and also shear pin size/quantity estimation) will be calculated using u/maxjet's awesome [charge size calculator](https://htmlpreview.github.io/?https://github.com/Max-q-rockets/Rocket-Calculators/blob/master/EjectionCalc3.html).

## Fin Flutter

Fin flutter: what it says on the box™

The core idea behind analyzing fins for failure modes like flutter or divergence is that as you start flying rockets faster and faster, eventually you can't keep assuming that your fins are just rigid control surfaces, and have to start worrying about the material properties of the fin and how it's attached to your airframe. One particularly fun effect that drops out of the math is the idea of fin flutter. Fin flutter is when axial vibration of the fin can be reinforced by the airflow going over it, leading to oscillations of increasing amplitude until the thing shakes itself apart. This divergent vibration can happen above a particular airspeed, dependant on fin geometry and material and things. Not an ideal thing for a fin to do. A very cool onboard video from another rocketeer demonstrating this (plus some bonus rolling shutter artifacts) is below.

{{< youtube pyct1Pii_cg >}}

It's really hard to estimate the airspeed at which fin flutter can exist without making some assumptions, or exhaustively characterizing your fin. Fin anabasis software like [AeroFinSim](https://www.aerorocket.com/finsim.html) makes some assumptions to linearize the problem, which gives us a conservative estimate for the speed above which fin flutter can occur.

The other fun fin failure mode is divergence, a radial twisting of the fin into the airflow such that its leading edge has an angle of attack and the fin material isn't sufficiently stiff to "pull" it back straight.

This video from a professor at Duke on YouTube, which I was sent by another rocketry friend, was a good introduction; Aeroelasticity is super cool. Note the demo towards the end, where they're able to test a fin at over 2x the linearly predicted flutter speed. The fin does vibrate, but it's not divergent -- its oscillations are bounded. The video explains this as unmodeled nonlinear effects which mean there's a grey zome between "my fin is capable of sustaining a vibration" and "my fin will fall apart".

{{< youtube BBD8IRWKrVU >}}

<p></p>

### Modeling with FinSim

To analyze my fins using FinSim, I trimmed down the height so they normal trapezoids instead of the cool Estes Goblin look. Initial simulations using the stock 1/8" G10 fiberglass fins that came with the kit were pretty sketchy, and showed fin flutter/divergence at just a few hundred ft/s. To get this velocity higher, we have a few different knobs we can turn, all of which fundamentally come back to increasing overall fin stiffness:

- Increase thickness
- Decrease fin height/semi-span
- Make the fin out of something stiffer

<img style="float: right; padding-left: 1em" src="../imgs/fg-flutter.png" width="50%">

I chose to sort of do all 3, by adding 4 layers of carbon fiber on top of the G10 fiberglass fin core and reducing the fin height down to 5in. Carbon fiber is much (~10x) stiffer than G10, and adding material on top also increases stiffness. This does mean we now have to deal with simulating a composite material made of fiberglass, carbon fiber, and two different kinds of epoxy. I get around this by running FinSim simulations assuming the fin is made entirely of fiberglass or epoxy, and using that as my worst-case. This worst-case, shown in the image to the right, shows 5 layers of G10 fiberglass simulating to a flutter velocity of Mach 1.3 and divergent of Mach 2.3 at sea level. Re-running this using material properties taken from Sollar's 3k twill + 820 resin system show a flutter of Mach 2.4 and divergence of Mach 4, which is well into overkill territory for a rocket going just barely Mach 1.


The big takeaways I have from my research and experiments with FinSim so far are:

- Fin flutter/divergence is a problem, but it's hard to actually predict when it'll happen
- Making your fin out of a stiffer material is helpful in increasing flutter/divergence velocities
    - Stiffness is part of why we see carbon fiber parts in high-performance rockets (plus being lightweight)
    - Corollary, G10 fiberglass is like a wet noodle in comparison
- Reducing fin height is also helpful
- Making your fin thicker is very helpful in increasing flutter/divergence velocities
  - Stiffness probably also scales with some power of thickness, like in Mechanics with simple beans

I'm excited to dig into playing with wet carbon fiber layups as I get started building soon!
