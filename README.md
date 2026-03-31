# G32 Connected Grill Monitor and Display MINI

[![GitHub release](https://img.shields.io/github/v/release/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/releases/latest)
[![GitHub Release Date](https://img.shields.io/github/release-date/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/releases)
[![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/t/sagdusmir/G32-Grill-Display-320x172-BT/main?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/commits/main/)
![GitHub license](https://img.shields.io/github/license/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=gnu&color=green)
[![Grill make](https://img.shields.io/badge/grill-OW_G32_Connected-critical)](https://www.grillsportverein.de/forum/threads/otto-wilde-g32-smarthome.369079/page-999)
[![HA support](https://img.shields.io/badge/Home_Assistant-recommended-informational?style=flat-square&logo=home-assistant&logoColor=white&color=orange)](https://home-assistant.io)

This repository is a stripped down version of https://github.com/sagdusmir/G32-Grill-Display-480x320-BTpref


Focus: **mobile, cloud-independent replacement** for the official Otto Wilde app / Grill Buddy — no cloud login, no Otto Wilde servers. Direct BLE connection to the grill (tested with firmware **v1.4.5**; older "v13" not compatible).

<img alt="Teaser Gauges" src="https://github.com/user-attachments/assets/7477aff2-aa70-4a29-8a00-d886d874ef73" width="200">
<img alt="Teaser Temperature Alarm" src="https://github.com/user-attachments/assets/67f30ca1-8170-49d3-b051-c44b80cde1a2" width="200">
<img alt="Teaser Info Page" src="https://github.com/user-attachments/assets/b5609668-ac7d-4246-a799-ebf88fbedc3b" width="200">
<img alt="Teaser Testing Case Design" src="https://github.com/user-attachments/assets/7748155b-8b2b-4c14-a970-0c6f3c926dd1" width="200">
<img alt="Teaser Testing Case Design Render" src="https://github.com/user-attachments/assets/e653098a-848d-4d84-96ad-7d0f5163ddc0" width="200">

Bare device during testing.<br>

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

- **Automatic detection** of a near by G32 Connected
- Real-time temperatures for up to **4 grill zones** + **4 external probes**
- **Gas level** monitoring (if GasBuddy is installed)
- **Alarms** — visual + optional buzzer for temperature limits and timer
- Touchscreen configuration
  - tap gauges to configure a temperature alarm
- Multiple **color schemes** (predefined + easy to add your own)
- **Connection & status icons** (BLE, WiFi, battery SOC)
- **Optional battery monitoring** the state of charge (SOC) of a connected battery can be displayed
- **Optional MEATER® integration** with **automatic detection** shows tip temperatures & battery SOC instead of G32 probes when connected. There is an alert if temperature specs are exceeded.
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
| USB 5V 2A Boost Converter + Charger circuit  | 1   | AliExpress                               |     ~2€ - 5€ |
| USB-C Connector                              | 1   | Amazon, eBay, AliExpress                 |       ~2€    |
| 2 pin Wire Connectors                        | n   | Amazon, eBay, AliExpress                 |       ~2€    |
| Diode                                        | 1   | eBay, somewhere online                   |       ~1€    |
| Screws	                                     | 4	 | hardware store, eBay, Amazon, AliExpress |       ~1€    |
| Buzzer	                                     | 1	 | Amazon, eBay, AliExpress                 |       ~1€    |
| some wires                                   | n   | AliExpress, Amazon, eBay                 |       ~2€    |
| Kapton tape or electrical tape               | ?   | AliExpress, Amazon, eBay                 |       ~0€    |
| Case                                         | 1   | a friend with a 3d printer               |    a beer    |
| USB-C Connection Cable                       | 1   | your existing collection of cables       |       ~0€    |


### Component Details

* __ESP32 Dev Board__<br>
  You need a "__Waveshare ESP32-C6-Touch-LCD-1.47__". It is equipped with an ESP32-C6, WiFi, Bluetooth, a 320x172 Pixel 1.47" touchscreen, and everything you need. No additional memory card required.


* __Battery__
  A 3.7V LiPo/Li-Ion Battery (1 cell) will power the ESP32 Dev Board. Because of space constraints I am going with a battery of type 702080  (7mm x 20mm x 80mm) with a capacity of 1500mAh.

* __Power Switch with Reverse Voltage Protection__<br>
  To minimize power draw, I am using a Pololu Mini Pushbutton Power Switch,Reverse Voltage Protection,LV (Pololu 2808) which should reduce power draw as much as possible. Unfortunately the module is a bit pricey.

* __5V 2A Boost Converter + Charger circuit__<br>
  I recommend using a cheap board that has an auto power-save feature. The one that I ultimately decided on goes under the name "Type-C USB 5V 2A Boost Converter Step-Up Power Module Lithium Battery Charging Protection Board LED Display USB Charger". The boost portion is actually not used because I wanted to keep it simple and have the SOC measurement working without adding another voltage divider for the voltage at the battery.
  Arduino PowerBoost 500C / 1000C modules seem to __NOT__ offer this feature. Those would completely drain the battery in a few days.

* __USB-C Connector__<br>
  To power the charger circuit it is very helpful to have a male USB-C plug breakout board to supply power. The solder pads / USB port on the backside of my pcb was only used for power output.

* __2 pin Wire Connectors__<br>
  I used a few micro JST1.25 2pin connectors (male + female) to keep things modular. At least battery should be easy do disconnect so you do not have to solder the wires while it is connected.

* __Diode__<br>
  A Schottky Diode with a low voltage drop of 0.3-0.4V (e.g. 1N5819) to separate the charging power path a bit from the rest because the documentation of most charge controllers will not be that detailed.

* __Buzzer__<br>
  A __passive__ piezo buzzer.<br>Configured pins are GPIO5 amd GPIO6. The buzzer should be rather small to fit inside tha case (e.g. ⌀13mm x 2.5mm or similar). The smaller the buzzer, the easier it is to mount the ESP32 Dev-Board in the enclosure. Even a "Universal Passive Buzzer 12085" (12mm x 8.5mm) will fit if you keep wires short.

* __Case__<br>
  There is a 3D model of a case in the `misc` folder. Using the case.m3f file is the easiest. If that does not work for you, you can give the two .stl files a try. I placed the main case with the bottom flat on the print bed. Enabled raft and manually added tree support from the bed to the underside of the power button, to the top of the usb-port cutout and in a straight vertical line in the middle of the back of the case so it does not tip over while printing. For the battery cover i placed the short staright edge on the build plate and manually added tree support to each untgerside of the clips and in a straight vertical line in the middle of the back to add some stability. I included some images that show where I painted support structures.

### Wiring

Important:<br>
the Pololu push button will point to the outside of the case, so make sure to have the wires on the opposite side pointing
towards the other comonents.
Space is limited, so connect the USB-C breakout board to the charger as shown in the wiring draft and solder wires from the
top of the pcb horizontally to the right (for both: charger module and USB-C breakout board). If the point in any other direction, you will struggle to fot everything in the case. 

- connect Pololu VOUT and GND to ESP32 BAT and GND
- connect Pololu VIN and GND in parallel with the battery to the battery pads of the charger module
- connect ESP32 VBUS and GND to the power input of the charger module with the Schottky diode as shown

The Pololu can be *carefully* slot into place (tight fit) with the wires pointing to the inside. The charger module with the installed USB plug should fit right inside the case (same orientation as in the wiring sketch). Place the piezo buzzer
on top and install the ESP32 Dev Board to close everything up. Use a bit of Kapton tape if exposed contacts might touch each other.

<img alt="wiring draft" src="https://github.com/user-attachments/assets/663e63a1-9d87-42c4-b06f-ce515e9edccc" width="200">

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
