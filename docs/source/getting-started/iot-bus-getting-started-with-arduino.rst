.. _getting-started-with-arduino:

Getting Started with Arduino
============================

To get started with Arduino we are fist going to install Arduino. Then we install the platform package for Espressif32. 
Finally, we plug in an IoT-Bus processor and run the Blink example.

1. Installation

    On this page `Arduino Software <https://www.arduino.cc/en/Main/Software>`_ you will find links for each major 
    operating system. Download it and follow the instructions.

2. Install the Espressif32 platform package
    
    Start Arduino and open Preferences window.
    Enter https://dl.espressif.com/dl/package_esp32_index.json into Additional Board Manager URLs field. You can add multiple URLs, separating them with commas.
    Open Boards Manager from Tools > Board menu and install esp32 platform (select ESP32 Dev Module from Tools > Board menu after installation).

3. Run the Blink example
    
    a. Open the Blink example from the Examples menu. It looks like this:

    code-block: c++


    b. ...

The other way to use the Arduino framework is to use PlatformIO. See Getting Started with PlatformIO for details.    