.. _iot-bus-proteus:

Proteus
=======

.. image:: ../_static/iot-bus-proteus.jpg
    :align: left
    :alt: Proteus
    :scale: 50%
    :target: http://www.oddwires.com/proteus-iot-bus-esp32-microprocessor-wi-fi-and-bluetooth-with-prototype-board-form-factor/

.. raw:: html
  
  <p style="clear: both;">    

This board is larger and designed to make it possible to add your own circuitry to make a complete IoT solution on one board.
It includes a dual-core 240 MHz ESP32 with WiFi and Bluetooth. You can use the WiFi both in station (device) mode and access point mode. 
It includes traditional Bluetooth as well as BLE 4.0. On-board is a 3.3V regulator and a battery charging device that enabled you 
to switch between using USB or battery power. 
  
The battery is automatically charged in the USB is plugged in. A status light shows if it is charging or fully charged. All ESP32 pins bar the flash pins are exposed 
and available for your use. 
  
The board includes a large prototyping area that includes room for traditional DIP and through-hole components as well 
as SMD parts such as SOIC and  SOT-23. A user LED and switch is included but not connected to any pins so you can use them how you wish. Two level shifters are included 
so you can interface with 5V devices. 
  
The Proteus includes both 3.3V and 5V rails. Both these rails are available whether powered by the USB or the battery 
as the 5V is derived from the lower voltage. 

`Buy it in the oddWires store... <http://www.oddwires.com/proteus-iot-bus-esp32-microprocessor-wi-fi-and-bluetooth-with-prototype-board-form-factor/>`__

Pins Used
---------

.. list-table::
  :header-rows:  1
  :widths: 20 80

  * - Pin
    - Description
  
  * - None
    - No pins are utilized by the Proteus board 

Schematic
---------

.. image:: ../_static/iot-bus-proteus-v1.1-schematic.png
    :align: left
    :alt: IoT-Bus Io Schematic
    :scale: 10%
    :target: ../_static/iot-bus-proteus-v1.1-schematic.png  

Platforms
---------
.. list-table::
    :header-rows:  1

    * - Name
      - Description

    * - :ref:`platform_espressif32`
      - Espressif Systems is a privately held fabless semiconductor company. 
        They provide wireless communications and Wi-Fi chips which are widely used in mobile devices and the 
        Internet of Things applications.

Frameworks
----------
.. list-table::
    :header-rows:  1

    * - Name
      - Description

    * - :ref:`framework_arduino`
      - Arduino Wiring-based Framework allows writing cross-platform 
        software to control devices attached to a wide range of Arduino boards to 
        create all kinds of creative coding, interactive objects, spaces or physical experiences.

    * - :ref:`framework_espidf`
      - Espressif IoT Development Framework. Official development framework for ESP32.


