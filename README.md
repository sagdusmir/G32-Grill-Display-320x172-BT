# G32 Connected Grill Monitor and Display MINI

[![GitHub release](https://img.shields.io/github/v/release/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/releases/latest)
[![GitHub Release Date](https://img.shields.io/github/release-date/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/releases)
[![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/t/sagdusmir/G32-Grill-Display-320x172-BT/main?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/commits/main/)
![GitHub license](https://img.shields.io/github/license/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=gnu&color=green)
[![Grill make](https://img.shields.io/badge/grill-OW_G32_Connected-critical)](https://www.grillsportverein.de/forum/threads/otto-wilde-g32-smarthome.369079/page-999)


Focus: **mobile, cloud-independent replacement** for the official Otto Wilde app / Grill Buddy — no cloud login, no Otto Wilde servers, Home Assistant totally optional. Direct BLE connection to the grill (tested with firmware **v1.4.5**; older "v13" not compatible).

<img alt="Teaser" src="https://github.com/user-attachments/assets/0f5f5065-4ec5-47f8-8567-3b7de9df23e4" width="200">
Assembled device with the case for attaching it to OW Module handles.

# Table of Contents

1. [Features](#features)
   - [Implemented functionality](#implemented-functionality)  
   - [What is missing?](#what-is-missing)
   - [Limitations](#limitations)
3. [Hardware](#hardware)
   - [BOM](#bom)
   - [Component Details](#component-details)
4. [Uploading the software to the ESP](#uploading-the-software-to-the-esp)
5. [Troubleshooting](#troubleshooting)
6. [Impressions](#impressions)
7. [Acknowledgments](#acknowledgments)
8. [Disclaimer](#disclaimer)

## Features

### Implemented functionality

- TODO

See [changelog.md](changelog.md).

### Limitations
* Everything that was mentioned above under [What is missing?](#what-is-missing)
* The UI might be a bit laggy at times - so touch input will take a second to have any effect. Suggestions on how to improve this further are welcome.
* Volume level of the optional buzzer / speaker is a bit low. This is the reason there is no volume control in the settings.
* Meater probes can only connect to a single device at a time. However, this does not prevent using a Meater Block.


## Hardware
### BOM

TODO


### Component Details

TODO


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

## Troubleshooting

1. During validation of the yaml file, you might see something like `[max_connections] is an invalid option for [esp32_ble]`. The "max_connections" option has been moved from "esp32_ble_tracker:" to "esp32_ble:". Both variants are included in the YAML and you need to switch to the other variant by adding / removing a comment (#). Do not mess up the indentation. This is caused by a breaking change in esphome.

2. If compiling and flashing the ESP32 succeeds, but the screen is looking distorted (the left portion is partially readable while the right portion shows mostly pixel noise"), simply look at the "dimensions" in the "display" section and swap the values for "width:" and "height:". This is caused by a breaking change in esphome.

3. If you get A LOT of strange syntax errors, try to clean up the configured build folder via
   ```bash
   esphome clean g32-display-mini.yaml
   ```


## Impressions
<small>These images show different versions of the software - so some details might be inconsistent.</small>


<img alt="device_assembly" src="https://github.com/user-attachments/assets/8faf2f34-4d98-47f2-9512-1f92ef224469" width="400">
<img alt="BTpref-retro2 0 0-main_view_cyan" src="https://github.com/user-attachments/assets/eca960b4-9641-4546-98c3-ed16e00ab826" width="400">

<img alt="BTpref-retro2 0 1-main_view_red_light" src="https://github.com/user-attachments/assets/b4afa697-324f-45b4-bcb8-1dc0c5bc71a7" width="265">
<img alt="BTpref-retro2 0 1-main_view_white" src="https://github.com/user-attachments/assets/27741973-4c46-4147-9b32-293e49b56a55" width="265">
<img alt="BTpref-retro2 0 0-main_view_amber" src="https://github.com/user-attachments/assets/6b80e574-6c00-42c9-ad54-8ba93f749827" width="265">
<img alt="BTpref-retro2 0 0-temp_alarm" src="https://github.com/user-attachments/assets/73363a1c-2063-4b14-b969-901baaf50088" width="265">
<img alt="BTpref-retro2 0 0-timer" src="https://github.com/user-attachments/assets/fe0e1212-1340-475d-b816-25a6abb685c0" width="265">
<img alt="BTpref-retro2 0 0-mac_address" src="https://github.com/user-attachments/assets/bd0b3435-790f-4acd-af92-3104471958ae" width="265">
<img alt="BTpref-retro2 3 0-wifi" src="https://github.com/user-attachments/assets/35becd29-fdcb-43d7-98a9-295b38a00ef4" width="265">
<img alt="BTpref-retro2 4 3-options" src="https://github.com/user-attachments/assets/981a29ef-3c3d-4a92-9003-8a9c90a8ab68" width="265">
<img alt="BTpref-retro2 3 1-warnings" src="https://github.com/user-attachments/assets/6b73301e-6cd6-405d-8f65-c555cd4398c3" width="265">
<img alt="BTpref-retro2 2 0-display" src="https://github.com/user-attachments/assets/8848e7dd-ddc9-4c12-a840-eedf1176ef42" width="265">
<img alt="BTpref-retro2 0 0-meater" src="https://github.com/user-attachments/assets/344972be-d253-450e-8157-0753d1509755" width="265">
<img alt="BTpref-retro2 4 3-version" src="https://github.com/user-attachments/assets/4b1173f1-c7a9-4835-a2b9-284c4aa8aa36" width="265">
<img alt="BTpref-retro2 4 0-reduced-temp-alarm-info" src="https://github.com/user-attachments/assets/94bd44cf-5bbd-4d45-9673-ba5b1ec7d3ea" width="265">
<img alt="BTpref-retro2 4 1-battery-3000mAh" src="https://github.com/user-attachments/assets/7e3d7d21-d101-47aa-9158-14b8208d6a8e" width="265">
<img alt="In action 1" src="https://github.com/user-attachments/assets/2cc83a7c-75c3-4c01-b1db-8f422a5380da" width="265">
<img alt="In Action 2" src="https://github.com/user-attachments/assets/6baaa8af-9068-4675-aac9-c1b00c2df483" width="265">



## Acknowledgments
This project would not have been possible without the work of the community. Special thanks go to:

[JBecker32/G32-Display-320x172-BT](https://github.com/JBecker32/G32-Display-320x172-BT) (the original software project)

[fschwarz86/g32](https://github.com/fschwarz86/g32)

[ralmoe/g32-docker-client](https://github.com/ralmoe/g32-docker-client)

[MortenVinding/MEATER.yaml](https://gist.github.com/MortenVinding/a513c0094d0df41a4425612257b3cabc) (Meater® accuracy)

[so99hero/Standalone Case JC3248W535C](https://www.thingiverse.com/thing:7127557)


## Disclaimer
This is third-party software developed by the community and is not officially developed or supported by Otto Wilde GmbH. Use at your own risk.

__This project is provided for educational and experimental purposes only.__


All hardware designs, schematics, code, instructions, and documentation are offered AS IS without any warranty of any kind, express or implied.
YOU BUILD AND USE THIS AT YOUR OWN RISK.
The author(s) and any contributors are not responsible for any injury, death, property damage, fire, electrical shock, data loss, voided warranties, legal violations, or any other consequences — direct, indirect, incidental, or consequential — that may result from building, modifying, or using this project or any derivative work.
Always follow local electrical/safety/building codes.


If you're not experienced with mains voltage, high current, lithium batteries, lasers, moving parts, etc., consult a qualified professional before proceeding.
Proceed only if you accept full personal responsibility.
