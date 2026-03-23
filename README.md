# G32 Connected Grill Monitor and Display MINI

[![GitHub release](https://img.shields.io/github/v/release/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/releases/latest)
[![GitHub Release Date](https://img.shields.io/github/release-date/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/releases)
[![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/t/sagdusmir/G32-Grill-Display-320x172-BT/main?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/commits/main/)
![GitHub license](https://img.shields.io/github/license/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=gnu&color=green)
[![Grill make](https://img.shields.io/badge/grill-OW_G32_Connected-critical)](https://www.grillsportverein.de/forum/threads/otto-wilde-g32-smarthome.369079/page-999)


This repository is a stripped down version of https://github.com/sagdusmir/G32-Grill-Display-480x320-BTpref


Focus: **mobile, cloud-independent replacement** for the official Otto Wilde app / Grill Buddy — no cloud login, no Otto Wilde servers. Direct BLE connection to the grill (tested with firmware **v1.4.5**; older "v13" not compatible).

<img alt="Teaser" src="https://github.com/user-attachments/assets/7477aff2-aa70-4a29-8a00-d886d874ef73" width="200">
Bare device during testing.<br>Wiring of buzzer, battery, charge circuit, and power button upcoming. A case will follow once everything else  has come together.

# Table of Contents

1. [Features](#features)
   - [Implemented functionality](#implemented-functionality)  
   - [What is missing?](#what-is-missing)
   - [Limitations](#limitations)
3. [Hardware](#hardware)
   - [BOM](#bom)
   - [Component Details](#component-details)
   - [Wiring](#wiring)
4. [Uploading the software to the ESP](#uploading-the-software-to-the-esp)
5. [Troubleshooting](#troubleshooting)
6. [Acknowledgments](#acknowledgments)
7. [Disclaimer](#disclaimer)

## Features

### Implemented functionality

- Real-time temperatures for up to **4 grill zones** + **4 external probes**
- **Gas level** monitoring (if GasBuddy is installed)
- **Alarms** — visual + optional buzzer for temperature limits and timer
- Touchscreen configuration
  - tap gauges to configure a temperature alarm
- Multiple **color schemes** (predefined + easy to add your own)
- **Connection & status icons** (BLE, WiFi, battery SOC)
- **Optional battery monitoring** the state of charge (SOC) of a connected battery can be displayed
- **Optional MEATER® integration** shows tip temperatures & battery SOC instead of G32 probes when connected. There is an alert if temperature specs are exceeded.
- **Optional Home Assistant** connectivity that exposes most of the measurements and allows confguring some settings of the device.

See [changelog.md](changelog.md).

### What is missing?
* **Meater 2 plus (aka PRO) support:** Meater 2 plus units are currently not supported
* **Gas Buddy:** calibration of a new gas bottle
* **G32 light:** setting the brightness level for turning on the light in the lid

### Limitations
* Everything that was mentioned above under [What is missing?](#what-is-missing)
* Volume level of the optional buzzer is a bit low.
* Meater probes can only connect to a single device at a time. However, this does not prevent using a Meater Block.


## Hardware
### BOM

| Component                                    | Qty | Source                                   | Costs        |
|----------------------------------------------|-----|------------------------------------------|--------------|
| ESP32 Dev Board                              | 1   | Amazon, AliExpress                       |   ~15€ - 20€ |
| Battery                                      | 1   | AliExpress                               |    ~8€ - 12€ |
| Power Switch with Reverse Voltage Protection | 1   | somewhere online                         |    ~5€ - 10€ |
| USB 5V 2A Boost Converter + Charger circuit  | 1   | Amazon, eBay, somewhere online           |   ~20€ - 30€ |
| Diode                                        | 2   | eBay                                     |       ~1€    |
| Screws	                                      | 4	  | hardware store, eBay, Amazon, AliExpress |       ~1€    |
| Buzzer	                                      | 1	  | Amazon, eBay, AliExpress                 |       ~1€    |
| some wires                                   | n   | AliExpress, Amazon, eBay                 |       ~2€    |
| USB-C Connection Cable                       | 1   | your existing collection of cables       |       ~0€    |


### Component Details

* __ESP32 Dev Board__<br>
  You need a "__Waveshare ESP32-C6-Touch-LCD-1.47__". It is equipped with an ESP32-C6, WiFi, Bluetooth, a 320x172 Pixel 1.47" touchscreen, and everything you need. No additional memory card required.


* __Battery__
  A 3.7V LiPo/Li-Ion Battery (1 cell) will power the ESP32 Dev Board. Because of space constraints I am going with a battery of type 702080  (7mm x 20mm x 80mm) with a capacity of 1500mAh.

* __Power Switch with Reverse Voltage Protection__<br>
  To minimize power draw, I am using a Pololu Mini Pushbutton Power Switch,Reverse Voltage Protection,LV (Pololu 2808) which should reduce power draw as much as possible.

* __5V 2A Boost Converter + Charger circuit__<br>
  The Dev-Board has no battery charger circuitry included. For charging the 3.7V LiPo battery, a Adafruit PowerBoost 500/1000 + Charger (Powerboost 500C / 1000C) is used. Do not confuse this with the "Basic" variant witchout charging.

* __Diode__<br>
  Two Schottky Diodes with a low voltage drop of 0.3-0.4V (e.g. 1N5819) to create clean power paths and prevent back-feeding.

* __Buzzer__<br>
  A __passive__ piezo buzzer.<br>Configured pins are GPIO5 amd GPIO6. The buzzer should be rather small to fit inside tha case (e.g. ⌀13mm x 2.5mm or similar).

### Wiring

__PLANNED__ and not tested:


## Uploading the software to the ESP

1. Install ESPHome CLI
   ```bash
   pip install esphome
   ```
2. Clone this repository and change directory into that folder
   ```bash
   git clone https://github.com/sagdusmir/G32-Grill-Display-320x172-BT.git && cd G32-Grill-Display-320x172-BT
   ```
3. Connect the ESP32-C6 1.47 Inch Display Development Board via USB
4. Compile and flash the software
   ```bash
   esphome run g32-display-mini.yaml
   ```
   You may be asked how the connection should be established.
5. You might need to reset the device after flashing to get the display to work (push the RST button).

## Troubleshooting

1. During validation of the yaml file, you might see something like `[max_connections] is an invalid option for [esp32_ble]`. The "max_connections" option has been moved from "esp32_ble_tracker:" to "esp32_ble:". Both variants are included in the YAML and you need to switch to the other variant by adding / removing a comment (#). Do not mess up the indentation. This is caused by a breaking change in esphome.

2. If compiling and flashing the ESP32 succeeds, but the screen is looking distorted (the left portion is partially readable while the right portion shows mostly pixel noise"), simply look at the "dimensions" in the "display" section and swap the values for "width:" and "height:". This is caused by a breaking change in esphome.

3. If you get A LOT of strange syntax errors, try to clean up the configured build folder via
   ```bash
   esphome clean g32-display-mini.yaml
   ```





## Acknowledgments
This project would not have been possible without the work of the community. Special thanks go to:

[Esaracci](https://community.home-assistant.io/u/esaracci/) (using this hardware with esphome)

[Pulpyy](https://community.home-assistant.io/u/pulpyy) (using this hardware with esphome)

[JBecker32/G32-Display-480x320-BT](https://github.com/JBecker32/G32-Display-480x320-BT) (the original software project)

[fschwarz86/g32](https://github.com/fschwarz86/g32)

[ralmoe/g32-docker-client](https://github.com/ralmoe/g32-docker-client)

[MortenVinding/MEATER.yaml](https://gist.github.com/MortenVinding/a513c0094d0df41a4425612257b3cabc) (Meater® accuracy)


## Disclaimer
This is third-party software developed by the community and is not officially developed or supported by Otto Wilde GmbH. Use at your own risk.

__This project is provided for educational and experimental purposes only.__


All hardware designs, schematics, code, instructions, and documentation are offered AS IS without any warranty of any kind, express or implied.
YOU BUILD AND USE THIS AT YOUR OWN RISK.
The author(s) and any contributors are not responsible for any injury, death, property damage, fire, electrical shock, data loss, voided warranties, legal violations, or any other consequences — direct, indirect, incidental, or consequential — that may result from building, modifying, or using this project or any derivative work.
Always follow local electrical/safety/building codes.


If you're not experienced with mains voltage, high current, lithium batteries, lasers, moving parts, etc., consult a qualified professional before proceeding.
Proceed only if you accept full personal responsibility.
