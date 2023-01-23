---
title: "Rocket Test Stand DAQ (AerospaceNU)"
date: 2022-09-20T13:48:04-05:00
draft: false
author:
image: /images/projects/test-stand-daq/gallery-1/assembled-daq.jpg
tags:
# image: /images/hero.png
description:
toc: false
---

AerospaceNU's Project Redshift was gearing up for a second hot-fire test our liquid rocket engine. The data acquisition electronics used for our first test during summer 2022 was made using a collection of unreliable Arduino breakout boards, could only read temperature from grounded thermocouples, and read pressure from our 10 pressure transducers at 5hz -- much too slow to determine what exactly happened during the first test. We needed a solution that could read pressure sensors at faster than 100hz, was robust to accidental ESD damage, and properly support grounded thermocouples.

{{< figure src="images/projects/test-stand-daq/gallery-1/old-vs-new.png" caption="Update rate and data acquired from old vs new electronics" alt="">}}

I designed this high-speed data acquisition board for AerospaceNU's liquid rocket engine test stand during Summer 2022. The electronics successfully gathered data during a hotfire test of our engine in October 2022. The PCB was designed to validate data acquisition designs for the club's eventual liquid-propelled rocket, and replace the interim breadboard solution designed during Spring 2022. 

{{< load-photoswipe >}}
{{< gallery >}} 
  {{< figure src="images/projects/test-stand-daq/gallery-1/03_Electronics-plate.png" caption="DAQ on electronics board" alt="DAQ mounted to electronics plate">}}
  {{< figure src="images/projects/test-stand-daq/gallery-1/06_Installed in test stand.jpg" caption="DAQ in test stand" alt="Data aquisition PCB mounted in the rocket engine test stand on test day">}}
{{< /gallery >}}

The design exceeded our requirements on connectivity, data acquisition rate, and resolution. The sensor board has inputs for:

- 15 pressure transducers, either 4-20mA or 0-5v (configurable), at up to 1.5KHz
- 4 type-K thermocouples
- 1 H-bridge loadcell (configurable gain)
- USB serial communication with central Raspberry Pi

## Design

Requirements for the data acquisition system were determined working alongside my peers in AerospaceNU's Propulsion subgroup. We had to balance supporting future expansion with complexity and BOM cost, and a lot of these requirements were driven by hardware that was already installed on our test stand.

| Requirement | Motivation |
| ----------- | ---------- |
| 12 pressure transduer inputs | Must fit at least 10 (currently on stand) + anticipated additions. Fewer can be used for flight |
| Inputs must be 0-5v or 4-20ma | Existing pressure sensors are a mix of both |
| 1 H-bridge loadcell input | Needed to verify engine design & math |
| 4 K-type thermocouple inputs | Need to sense temperature of parts of engine to verify regenerative cooling math -- only technically need 2 |
| Interface with Pi | Needs to talk to existing central Raspberry Pi (which runs the stand), and be robust to EMI |

After requirement definition, part selection and schematic capture could begin. ADC options were limited due to chip shortage, but were able to find MCP3564 24-bit ADCs still in stock on DigiKey. We'd used them previously (for a rocket DAQ project), and had a known-working driver already written. We also chose to design around a COTS STM32 microcontroller breakout to further simplify the schematic and reduce part count. We also chose to stick with MAX31855 Type-K thermocouple interface IC, with proper ground isolation to let us use grounded thermocouples.

I designed the circuit board using KiCad 6, my new favorite EDA program.  The schematic itself involved a lot of duplicated subcircuits, and KiCad's layout replication plugin was particularly handy in quickly replicating the input filter and switchover layout 15 times. 

{{< gallery >}}
  {{< figure src="images/projects/test-stand-daq/gallery-1/00_PCB_front.jpg" caption="PCB front" alt="CAD render of the front of the final PCB design">}}
  {{< figure src="images/projects/test-stand-daq/gallery-1/01_PCB_back.png" caption="PCB back" alt="CAD render of the back of the final PCB design">}}
{{< /gallery >}}

<!-- {{< gallery dir="images/projects/test-stand-daq/gallery-1" />}} {{< load-photoswipe >}} -->

## Assembly and Test

The passives on the back of the PCB were assembled by JLCPCB, and ICs were hand-soldered. The MCP3564 ADC was particularly troublesome in its 3x3 mm (20-UQFN) package above -- note the adjacent 0603 capacitors for scale, themselves only 1.6mm x 0.8mm! 

{{< gallery >}}
{{< figure src="images/projects/test-stand-daq/gallery-1/04_ADC_soldering.jpg" caption="Soldering the MCP3564 ADC chip">}}
{{< /gallery >}}

More notes on:
- TC RF interference
- MCP3564 soldering debugging
- Embedded code
- Test results
