.. _iot-bus-overview:

Iot-Bus Overview
================

The oddWires IoT-Bus system is based on a low-cost, open design that includes multiple main boards 
including a minimalist, breadboard-friendly form factorthe IoT-Bus Io and a
version with a large prototyping area which enables a single-board IoT solution, the Proteus. 

Thhe IoT-Bus is designed to be "plug and play" - the new range of oddWires open IoT-Bus boards use the 
Espressif ESP32 microprocessor (240Mhz, 32-bit, 4MB) for rapid, low-cost IoT development and deployment. 

Our aim is to provide an open platform, easy to adopt and build on, adaptable, tested, with many solutions already available.
There are no lock-in costs, and overall it provide a low-cost solution for faster development of professional, 
educational and hobbyist applications. 

A variety of programming languages, environments and frameworks that work right out of the box with IoT-Bus and PlatformIO
supports most of them in a professional or serious educational or hobby environment. You can use either the esp-idf framework 
for a professional multi-tasking system based on freeRTOS or the popular Arduino environment for simplicity.

So take your choice! Other platforms include javascript by moddable, python by Micropython, or the mongoose server

IoT-Bus System
--------------

* Open Design
* Low-cost
*	Plug and Play, Expandable
*	Powerful 240MHz, 32-bit Processor with 4Mb of Flash Memory
*	Multiple Form Factor Main Boards (Io, Proteus) 
*	Connected in Many Ways (Wi-Fi, Bluetooth, BLE 4.0. LoRa and Canbus available options)
*	Integrated 2.4" Touch TFT QVGA Display Available 
* Solder-able Prototype Board with Controller
*	IOT-Ready, Relay and Motor Controller
*	Multiple open platforms
*	Supports C++, Micropython and javacsript

At the heart of the system is an ESP32 processor providing two SPI and an I2C interface with plenty of general purpose I/O. 
The Espressif ESP-WROOM-32 has been selected as the microcontroller enabling very low-cost deployment of production IoT devices. 
It offers 240Mhz, 32-bit processing with 4MB of flash as standard.

The first controller boards drive relays and motors and there are a wide range of connectivity options including
Wi-Fi, Bluetooth, CAN Bus, and LoRa.

Developing open IoT applications means being able to see the schematics for the hardware, using open tools,
frameworks and platforms and very importantly the cloud you use has to be open.

Mozilla IoT
-----------

We are partnering with mozilla to offer kits that can be used to quickly integrate with mozilla-iot. 
See our examples on github here. 

Two main-board form-factors
---------------------------

* Io - Very small and breadboard-friendly with option of male, female or both stackable headers
* Proteus - larger prototyping board for easier customization and pinout access

JTAG Debugging
--------------
Both the Io and Proteus processor boards can accept a specially designed JTAG board offering 
hardware debugging. Take a look at how easy it is to use with PlatformIO's Unified Debugger. 
Just plug it in and start debugging! No more printing to the terminal!

2.4" Touch TFT QVGA Display
---------------------------

There is a 320x240 QVGA TFT Touch Display offering plug and play display output and 
touch sensing together with a 4-bit SDMMC SD Card.

Two additional connectivity options
-----------------------------------

* CAN Bus - CAN Bus module
* LoRa - HOPE RFM95 integration

Two controller boards
---------------------

* Relay - opto-isolated relay board
* Motor - two stepper or four DC motor controller

Platforms
---------
.. list-table::
    :header-rows:  1

    * - Name
      - Description

    * - :ref:`espressif32`
      - Espressif Systems is a privately held fabless semiconductor company. They provide wireless communications and Wi-Fi chips which are widely used in mobile devices and the Internet of Things applications.

Frameworks
----------
.. list-table::
    :header-rows:  1

    * - Name
      - Description

    * - :ref:`arduino`
      - Arduino Wiring-based Framework allows writing cross-platform software to control devices attached to a wide range of Arduino boards to create all kinds of creative coding, interactive objects, spaces or physical experiences.

    * - :ref:`esp-idf`
      - Espressif IoT Development Framework. Official development framework for ESP32.


