.. _iot-bus-jtag:

JTAG
====

.. image:: ../_static/iot-bus-jtag.jpg
    :align: left
    :alt: Io
    :scale: 50%
    :target: ../_static/iot-bus-jtag.jpg

.. raw:: html
  
    <p style="clear: both;">  

This IoT-Bus module provides JTAG debugging for the
:ref:`iot-bus-io` and :ref:`iot-bus-proteus`
boards (can be used with other boards too, see wiring connections below).

Both the Io and Proteus processor boards can accept a specially designed JTAG board offering 
hardware debugging. Our JTAG board is based on the FT232H and it enables comprehensive JTAG debugging support. 
You can use OpenOCD and GDB in combination to use it but our recommendation is to use PlatformIO. 
PlatformIO has taken away all the hard work of configuring OpenOCD and GDB. You simply select it is your debugging choice as described 
`here <https://docs.platformio.org/en/latest/plus/debug-tools/iot-bus-jtag.html>`_. 
Take a look at how easy it is to use with `PlatformIO's Unified Debugger <https://docs.platformio.org/en/latest/plus/debugging.html>`_. 
Just plug it in and start debugging! No more printing to the terminal!

`Buy it in the oddWires store... <http://www.oddwires.com/iot-bus-esp32-jtag/>`__

PlatformIO Configuration
------------------------

You can configure the debugging tool using the debug_tool option in
platformio.ini. If you are using an Io board (iotbusio in Platformio) or a Proteus board (iotbusproteus in PlatformIO) 
then you do not need to explicitly set debug_tool as it will be set implicitly:

.. code-block:: ini

    [env:myenv]
    platform = ...
    board = ...
    debug_tool = iot-bus-jtag

Pins Used
---------

.. list-table::
  :header-rows:  1

  * - IOT-Bus JTAG Pin
    - Board JTAG Pin
  * - 3V3
    - Positive Supply Voltage — Power supply for JTAG interface drivers
  * - GND
    - GND - Digital Ground    
  * - 12
    - TDI - Test Data In pin   
  * - 14
    - TMS - Test Mode State pin  
  * - 15
    - TCK - JTAG Return Test Clock    
  * - 13
    - TDO - Test Data Out pin   
  * - EN
    - RESET


Schematic
---------

.. image:: ../_static/iot-bus-jtag-v1.0-schematic.png
    :align: left
    :alt: IoT-Bus Io Schematic
    :scale: 8%
    :target: ../_static/iot-bus-jtag-v1.0-schematic.png

Click image to enlarge.

Platforms
---------
.. list-table::
    :header-rows:  1

    * - Name
      - Description

    * - :ref:`platform_espressif32`
      - Espressif Systems is a privately held fabless semiconductor company. They provide wireless communications and Wi-Fi chips which are widely used in mobile devices and the Internet of Things applications.

Frameworks
----------
.. list-table::
    :header-rows:  1

    * - Name
      - Description

    * - :ref:`framework_arduino`
      - Arduino Wiring-based Framework allows writing cross-platform software to control devices attached to a wide range of Arduino boards to create all kinds of creative coding, interactive objects, spaces or physical experiences.

    * - :ref:`framework_espidf`
      - Espressif IoT Development Framework. Official development framework for ESP32.

