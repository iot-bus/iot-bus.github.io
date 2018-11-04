.. _getting-started-with-micro-python:

Getting Started with Micro-Python
=================================

MicroPython is a lean and efficient implementation of the Python 3 programming language that includes a small 
subset of the Python standard library and is optimized to run on micro-controllers and in constrained environments. 
You can find out more `here <https://micropython.org/>`_. 
You can download the firmware from `this location <http://micropython.org/download>`_. 

For convenience, this is a link to an ESP32 binary: esp32-20180924-v1.9.4-575-g6ea6c7cc9.bin

You will need esptool.py (available `right here <https://github.com/espressif/esptool>`_). If you are putting MicroPython on for the first time then you should first erase the entire flash using:

.. code-block:: none

    esptool.py --chip esp32 erase_flash

Program your board using the esptool.py program, and put the firmware starting at address 0x1000. For example:

.. code-block:: none

    esptool.py --chip esp32 --port /dev/ttyUSB1 write_flash -z 0x1000 esp32-20180511-v1.9.4.bin