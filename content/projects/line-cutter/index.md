---
title: "Parachute Reefing Cutter"
date: 2021-05-09T13:48:04-05:00
draft: false
author: Matthew Morley
image: /projects/line-cutter/imgs/assem-top.jpg
tags: [Rocketry, PCB Design]
description:
toc: false
---

Reefing paracutes is important for AerospaceNU's projects. In our case, we're designing circumferentially reefed parachutes that can be deployed initially as drogue parachutes to slow the rocket's descent, and fully inflated closer to the ground to reduce drift due to wind. Reefing lines are cut using Nichrome wires when altitude or ambient light thresholds are reached.

In this project, I designed the Printed Circuit Board shown below. The PCB was designed in Eagle, and the housing in Solidworks. Initial prototypes were made on perfboard to validate the overall system and develop code before we moved to a custom PCB.

{{< load-photoswipe >}}
{{< gallery >}} 
    {{< figure src="/projects/line-cutter/imgs/lc-r1.jpg" caption="Rev 1">}}
    {{< figure src="/projects/line-cutter/imgs/daap.jpg" caption="Rev 2">}}
    {{< figure src="/projects/line-cutter/imgs/pcb-r2.jpg" caption="First PCB rev">}}
    {{< figure src="/projects/line-cutter/imgs/assem-top.jpg" caption="Final PCB top">}}
    {{< figure src="/projects/line-cutter/imgs/assem-bottom.jpg" caption="Final PCB bottom">}}
{{< /gallery >}}

{{< youtube Qcm_kyZd2H0 >}}
<p></p>

## Design

The board is based around the Nordic NRF52840, which has integrated Bluetooth communication. The nichrome wires, which actually cut the reefing lines, are powered by two MOSFETs that can each sink up to 20 amps from a 1S LiPo battery. The Micro USB port both provides communication via USB and battery charging.

The MS5607 barometer and ICM-20602 IMU communicate with the main processor over I2C. Finally, 128M of SPI flash memory allows us to record flight data and logs.

The design of the cutter went through multiple revisions, including a servo-actuated blade, before we settled on a nichrome-based design. In the current design, nichrome is tensioned against the reefing line by springs. The design was inspired by A Nichrome Burn Wire Release Mechanism for CubeSats (2012), in which a similar system was employed on CubeSats.

The line cutter has gone through multiple iterations so far. In addition to three PCB revisions and two perfboard prototypes, fellow AerospaceNU students have written three software revisions and four 3D-Printed case revisions.


{{< gallery >}} 
    {{< figure src="/projects/line-cutter/imgs/case-cad.png" caption="4th case revisison">}}
    {{< figure src="/projects/line-cutter/imgs/parachute.jpg" caption="Cutters on parachute">}}
{{< /gallery >}}


The PCBs are shown inside their cases in the above picture, taken at Aimsbury on 3/20/2021.  A line is wrapped around the circumference of the parachute to constrict the throat, and cut by either one of the two cutters. Only one cutter needs to cut in order for the parachute to disreef.

{{< gallery >}} 
    {{< figure src="/projects/line-cutter/imgs/schematic.png" caption="Schematic in Eagle">}}
    {{< figure src="/projects/line-cutter/imgs/ecad-top.png" caption="PCB layout, top">}}
    {{< figure src="/projects/line-cutter/imgs/ecad-bottom.png" caption="PCB layout, bottom">}}
{{< /gallery >}}

Formulas presented in Reefing Line Tension in CPAS Main Parachute Cluster (2013) were used to estimate tension in a circumferential reefing line given parameters like shroud length and the angles of the canopy at the throat. These tension estimates were used to select the cord actually used to reef the parachute. In a worst-case static scenario, the reefing line tension should be under 40lbs of tension; 0.8mm braided dyneema (rated for 200lb) is currently used for a safety factor of 5.

Drone tests were performed to validate code before launches. Below is shown data collected during one of these tests

<img src="/projects/line-cutter/imgs/drone-test.png" caption="Drone test data" width="100%"/>
