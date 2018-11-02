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

This IoT-Bus module ...

`See it in the oddWires store... <http://www.oddwires.com/proteus-iot-bus-esp32-microprocessor-wi-fi-and-bluetooth-with-prototype-board-form-factor/>`__

.. contents:: Contents
    :local:


Pins Used
---------

need editing

.. list-table::
  :header-rows:  1

  * - IOT-Bus JTAG Pin
    - Board JTAG Pin
    - Description
  * - 2
    - VCC
    - Positive Supply Voltage — Power supply for JTAG interface drivers
  * - 1
    - GND
    - Digital ground
  * - 16
    - TDI
    - Test Data In pin
  * - 14
    - TMS
    - Test Mode State pin
  * - 15
    - TCK
    - JTAG Return Test ClocK
  * - 13
    - TDO
    - Test Data Out pin
  * - 3
    - RESET
    - Connect this pin to the (active low) reset input of the target CPU

.. begin_platforms

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


