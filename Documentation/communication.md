Communication

This document describes how the communication is working on the new CarCOntroller.

The following interfaces are available for communication:
- I2C on display for backward compatibility with the old CC
- USB for configuration, debugging and firmware updates
- CAN bus for communication with other devices
- ST-link programming header


Can BUS
-------

Can bus is the main interface for communication with other devices.
This could be the BMS, a new display or other devices that are connected to the car.

Note: When not using a BMS, the CarController will provide the information about the current SOC and other important information via CAN bus by itself as it contains a minimal BMS functionality.

The working principle is to make information about power draw, current SOC and other important information available via CAN bus.

The CarController receives and relays information from other devices e.g. a BMS. It will expose as much information as possible alowing other devices to control the car and make decisions based on the information provided by the CarController.
It also provides interfaces to control the car e.g. forward/reverse, buzzer and so on.

Todo: Insert diagram of the communication flow
BMS Information -> CAN bus -> CarController <--> CAN bus <--> Request SOC <--> Module

USB
---

Simple CP2102 USB to UART bridge connected to UART on MCU.
Contains a CLI for configuration and debugging.
Can also be firmware upgraded.

I2C
---
Simple I2C interface, only available for the display.
Drives the old SAA1064 display drivers together with adress select pin for changing adressing of the SAA1064 pins due to 
using all available adresses for the SAA1064 drivers.

