.. _getting-started-with-platformio:

Getting Started with PlatformIO
===============================

Thank you for choosing PlatformIO IDE for VSCode

1. `Download <https://code.visualstudio.com/>`_ and install official Microsoft's Visual Studio Code, PlatformIO IDE is built on top of it.

2. Open VSCode Extension Manager and search for official platformio-ide extension:

    .. image:: ../_static/platformio-ide-vscode-pkg-installer.png
        :align: center
        :alt: VSCode Extensions Installer
        :width: 100%

3. Install PlatformIO IDE.
You can find details on using PlatformIO with the IoT-Bus Io board `here <https://docs.platformio.org/en/latest/boards/espressif32/iotbusio.html>`_.

4. Git clone or download the IoT-Bus examples from `Github <https://github.com/iot-bus/iot-bus-examples-platformio>`.

5. Plug in IoT-Bus Io. Open the iot-bus-blink example and run. Onboard LED should blink once a second. When you create a new PlatformIO application simply select the oddWires IoT-Bus Io as the board. 
This will also ensure you have the correct default debugger when using the IoT-Bus JTAG board.

6. To debug, simply plug in a JTAG board connect up the USB cable to the JTAG board and start debugging. No configuration of OpenOCD or GDB required.





