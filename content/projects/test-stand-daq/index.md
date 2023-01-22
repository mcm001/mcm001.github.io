---
title: "Rocket Test Stand DAQ (AerospaceNU)"
date: 2022-07-20T13:48:04-05:00
draft: false
author:
image: https://mir-s3-cdn-cf.behance.net/project_modules/fs/a7c016158393971.638a7102c2051.jpg
tags:
# image: /images/hero.png
description:
toc:
---

## Summary

I designed this high-speed data acquisition board for AerospaceNU's liquid rocket engine test stand during Summer 2022. The electronics successfully gathered data during a hotfire test of our engine in October 2022.

The PCB was designed to validate data acquisition designs for the club's eventual liquid-propelled rocket, and replace the interim breadboard solution designed during Spring 2022. The requirements for this PCB include:

<!-- | Requirement | Motivation |
| ----------- | ---------- |
| 12 pressure transduer inputs | Must fit at least 10 (currently on stand) + anticipated additions. Fewer can be used for flight |
| Inputs must be 0-5v or 4-20ma | Existing pressure sensors are a mix of both |
| 1 H-bridge loadcell input | Needed to verify engine design & math |
| 4 K-type thermocouple inputs | Need to sense temperature of parts of engine to verify regenerative cooling math |
| Interface with Pi | Needs to talk to existing central Raspberry Pi (which runs the stand), and be robust to EMI | -->

The design exceeded our requirements on connectivity, data acquisition rate, and resolution. The sensor board has inputs for:

- 15 pressure transducers, either 4-20mA or 0-5v (configurable), at up to 1.5KHz
- 4 type-K thermocouples
- 1 loadcell (configurable gain)
- USB-CDC communication with central Raspberry Pi

<!-- The sensor board can be seen installed inside the electronics box of the test stand, which also houses power supplies and pneumatic solenoids for valve actuation. -->

<div class="col">
    <div class="row">
        <div class="col">
        <figure style="float: right;">
            <img src="https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/3dd643158393971.638a71025ff03.png" class="img-responsive rounded" style="">
            <figcaption>PCB (right) installed on electronics pan</figcaption>
        </figure>
        </div>
        <div class="col">
        <figure style="float: right; ">
            <img src="https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/3a4595158393971.638a71025f142.png" class="img-responsive rounded" style="">
            <figcaption>PCB (right) installed on electronics pan</figcaption>
        </figure>
        </div>
        <div class="col">
        <figure style="float: right; ">
            <img src="https://mir-s3-cdn-cf.behance.net/project_modules/1400_opt_1/0a60cd158393971.638a71025e0e6.jpg" class="img-responsive rounded" style="">
            <figcaption>PCB (right) installed on electronics pan</figcaption>
        </figure>
        </div>
    </div>
    <div class="row">
        <figure style="float: right; ">
            <img src="https://mir-s3-cdn-cf.behance.net/project_modules/2800_opt_1/0ec905158393971.638a7101db36b.jpg" class="img-responsive rounded" style="">
            <figcaption>PCB (right) installed on electronics pan</figcaption>
        </figure>
        <figure style="float: right; ">
            <img src="https://mir-s3-cdn-cf.behance.net/project_modules/2800_opt_1/8abc0a158393971.638a7101d9b23.jpg" class="img-responsive rounded" style="">
            <figcaption>Control system at a test, summer 2022</figcaption>
        </figure>
    </div>
</div>


Schematic capture and PCB layout was done in KiCad 6 (my new favorite EDA program). I used a layout replication plugin to quickly replicate the input filter and switchover layout 15x.

The passives on the back of the PCB (above, middle) were placed by JLCPCB, and ICs were hand-soldered. The MCP3564 was particularly troublesome in its 20-UQFN (3x3 mm) package (above, right; 0603 capacitors for scale).
