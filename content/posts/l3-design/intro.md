---
title: "Level 3 Rocket - Intro"
date: 2023-09-17T16:50:30-05:00
draft: false
author: Matt Morley
tags:
image: /posts/l3-design/imgs/3d-ork.png
description:
toc:
---

This blog will cover the design and build process of my NAR Level 3 certification rocket. If you haven't yet, check out how I designed and built my Level 1 and 2 rockets [over on Behance](https://www.behance.net/gallery/116889687/L1L2-HPR-Certification-Attempt)! Follow along as I describe the [airframe design](../design) & analyses, build the airframe and electronics, and (soontm) take it for a test flight!

<!-- [build the rocket](../build) airframe & electronics, and (soontm) [take it for a test flight](../test). -->

## Motivation

During my first 3 years in AerospaceNU, Northeastern's rocketry club, we've regularly flown increasingly larger rocket motors and complex rockets. NAR limits the rocket motor impulse we can fly with Level 2 certifications to under 5,120 Newton-seconds, or an L-class motor (below). For our club to continue building large rockets and continue to set club speed and altitude records, we'll need to fly rockets above this limit. A Level 3 certification would allow me to fly rockets with up to 40,960 Newton-seconds of impulse (O-class)!

<img src="/projects/beanboozler/imgs/ldrs-40-assembly.jpg" caption="L265 rocket motor for scale" width="100%" class="center"/>
<span class="center"><i>L265 rocket motor for scale. Level 3 motors are up to 10x larger!</i></span>
<p></p>

The certification process through NAR (National Association of Rocketry) is [pretty straightforward](https://www.nar.org/high-power-rocketry-info/level-3-hpr-certification/). After gaining your Level 1 and 2 certifications, you'll need to identify a local member of the Level 3 Certification Committee, rocketeers who have proven their modeling skills and volunteer to mentor others, and propose the project to them. Once you get the go-ahead, you can start building the rocket, documenting the process as you go. Once the rocket's ready, you present design and build documentation to your L3CC mentor, and then successfully fly your rocket on a Level-3-class rocket motor. This class of rocket motor can get stupidly expensive -- they start at $350, and can cost over $2000. Rocketry is definitely my hobby with the worst dollars-per-second ratio, beating sailing by a good margin.

## High-Level Design

Some high-level specs of the rocket design are shown below. I'm aiming to keep the rocket below the 10,000 ft altitude ceiling at my local club in Vermont.

<img src="/posts/l3-design/imgs/onshape-airframe.png" caption="Onsahpe boilerplate design" width="100%"/>

<p></p>

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


My budget also ended up being fairly reasonable, thanks to leveraging supplies like parachutes and electronics from the AerospceNU lab. The whole project was funded by the club (and I guess transitively through my tuition), for which I am grateful.

| Item                                        | Cost   |
|---------------------------------------------|--------|
| M1297 AT 75mm-4 grain Reload                | $339   |
| CTI 75mm/4 Grain Motor Casing               | $0     |
| Goblin 5 Kit                                | $297   |
| 60in Toroidal Parachute                     | $0     |
| 21 in Drogue Parachute                      | $0     |
| Wildman Shipping                            | $93.70 |
| Soller 3k twill, 6 yards                    | $94.95 |
| Soller 820 epoxy + 824 slow hardener, quart | $59.98 |
| Peel ply, >1 yard                           | $23    |
| EasyMini Altimeters                         | $0     |
| 1s LiPo Batteries                           | $0     |
| Av-bay Threaded Rod & Hardware              | $0     |
| EggFinder Mini GPS tracker                  | $0     |
| Spray Paint                                 | $0     |
| Total                                       | $908   |

<style>
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 55%;
}
</style>
