---
title: "Rocket Test Stand DAQ (AerospaceNU)"
date: 2022-07-20T13:48:04-05:00
draft: false
author:
image: https://mir-s3-cdn-cf.behance.net/project_modules/fs/a7c016158393971.638a7102c2051.jpg
tags:
# image: /images/hero.png
description:
toc: False
---

{{< load-photoswipe >}}

## Summary

I designed this high-speed data acquisition board for AerospaceNU's liquid rocket engine test stand during Summer 2022. The electronics successfully gathered data during a hotfire test of our engine in October 2022. The PCB was designed to validate data acquisition designs for the club's eventual liquid-propelled rocket, and replace the interim breadboard solution designed during Spring 2022. 
<!-- The requirements for this PCB include:
| Requirement | Motivation |
| ----------- | ---------- |
| 12 pressure transduer inputs | Must fit at least 10 (currently on stand) + anticipated additions. Fewer can be used for flight |
| Inputs must be 0-5v or 4-20ma | Existing pressure sensors are a mix of both |
| 1 H-bridge loadcell input | Needed to verify engine design & math |
| 4 K-type thermocouple inputs | Need to sense temperature of parts of engine to verify regenerative cooling math |
| Interface with Pi | Needs to talk to existing central Raspberry Pi (which runs the stand), and be robust to EMI | -->

The design exceeded our requirements on connectivity, data acquisition rate, and resolution. The sensor board has inputs for:

- 15 pressure transducers, either 4-20mA or 0-5v (configurable), at up to 1.5KHz
- 4 type-K thermocouples
- 1 H-bridge loadcell (configurable gain)
- USB-CDC communication with central Raspberry Pi

{{< gallery dir="images/projects/test-stand-daq/gallery-1" />}} {{< load-photoswipe >}}

Schematic capture and PCB layout was done in KiCad 6 (my new favorite EDA program). The layout replication plugin was particularly handy in quickly replicating the input filter and switchover layout 15x.

The passives on the back of the PCB were assembled by JLCPCB, and ICs were hand-soldered. The MCP3564 ADC was particularly troublesome in its 3x3 mm (20-UQFN) package above -- note the adjacent 0603 capacitors for scale, themselves only 1.6mm x 0.8mm! 
