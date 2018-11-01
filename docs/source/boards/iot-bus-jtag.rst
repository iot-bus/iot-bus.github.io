.. _iot-bus-jtag:

JTAG
====

.. image:: ../_static/iot-bus-jtag.jpg
  :target: http://www.oddwires.com/iot-bus-esp32-jtag/?utm_source=platformio&utm_medium=docs

This IoT-Bus module provides JTAG debugging for the
:ref:`iot-bus-io` and :ref:`iot-bus-proteus`
boards (can be used with other boards too, see wiring connections below).
The board uses the FT232H to provide a USB controller with JTAG
support. Both debugging and flashing is possible using this port.
`Vendor information... <http://www.oddwires.com/iot-bus-esp32-jtag/?utm_source=platformio&utm_medium=docs>`__

.. contents:: Contents
    :local:

PlatformIO Configuration
------------------------

You can configure the debugging tool using the debug_tool option in
platformio.ini:

.. code-block:: ini

    [env:myenv]
    platform = ...
    board = ...
    debug_tool = iot-bus-jtag

Pins Used
---------

You only need to make any connections if you are using the JTAG modules outside of the IoT-BUs system.

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
  * - 12
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

