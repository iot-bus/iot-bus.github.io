..  Copyright (c) 2014-present PlatformIO <contact@platformio.org>
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
       http://www.apache.org/licenses/LICENSE-2.0
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

.. _debugging_tool_iot-bus-jtag:

oddWires IOT-Bus Io
===================

.. image:: ../_static/iot-bus-io.jpg
  :target: http://www.oddwires.com/iot-bus-esp32-io/?utm_source=platformio&utm_medium=docs

This IoT-Bus module is the foundation of the IoT-Bus system.
`Vendor information... <http://www.oddwires.com/iot-bus-esp32-io/?utm_source=platformio&utm_medium=docs>`__

.. contents:: Contents
    :local:

Configuration
-------------

You can configure debugging tool using :ref:`projectconf_debug_tool` option in
:ref:`projectconf`:

.. code-block:: ini

    [env:myenv]
    platform = ...
    board = ...
    debug_tool = iot-bus-jtag

If you would like to use this tool for firmware uploading, please change
upload protocol:

.. code-block:: ini

    [env:myenv]
    platform = ...
    board = ...
    debug_tool = iot-bus-jtag
    upload_protocol = iot-bus-jtag

More options:

* :ref:`projectconf_section_env_debug`
* :ref:`projectconf_section_env_upload`

.. include:: _common_jtag_drivers.rst

Wiring Connections
------------------

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

    * - :ref:`framework_simba`
      - Simba is an RTOS and build framework. It aims to make embedded programming easy and portable.

