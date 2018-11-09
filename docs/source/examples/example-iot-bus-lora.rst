.. _example-iot-bus-lora:

IoT-Bus LoRa Example
====================

These two examples work together using Sandeep Mistry's excellent arduino-LoRa library which can be 
found `here <https://github.com/sandeepmistry/arduino-LoRa>`_. 


LoRa Sender
-----------

.. code-block:: c++

    #include <SPI.h>
    #include <LoRa.h>

    #define DIO0 35
    #define SS   5
    #define RESET 17

    int counter = 0;

    void setup() {
        LoRa.setPins(SS, RESET, DIO0);

These lines include the libraries required and define the DIO0, SS and RESET pins required to use the IoT-BUs LoRa board.

.. code-block:: c++

    if (!LoRa.begin(915E6)) {
        Serial.println("Starting LoRa failed!");
        while (1);
    }

These lines attempt to start LoRa and will go no further if failure.    

.. code-block:: c++

    // send packet
    LoRa.beginPacket();
    LoRa.print("hello ");
    LoRa.print(counter);
    LoRa.endPacket();

These lines send a packet. The packet is transmitted on endPacket(). The complete example is shown below.

.. code-block:: c++

    #include <SPI.h>
    #include <LoRa.h>

    #define DIO0 35
    #define SS   5
    #define RESET 17

    int counter = 0;

    void setup() {
        LoRa.setPins(SS, RESET, DIO0);
        Serial.begin(115200);
        while (!Serial);

        Serial.println("LoRa Sender");

        if (!LoRa.begin(915E6)) {
            Serial.println("Starting LoRa failed!");
            while (1);
        }
    }

    void loop() {
        Serial.print("Sending packet: ");
        Serial.println(counter);

        // send packet
        LoRa.beginPacket();
        LoRa.print("hello ");
        LoRa.print(counter);
        LoRa.endPacket();

        counter++;

        delay(5000);
    }

LoRa Receiver
-------------   

.. code-block:: c++

    #include <SPI.h>
    #include <LoRa.h>

    #define DIO0 35
    #define SS   5
    #define RESET 17

    int counter = 0;

    void setup() {
        LoRa.setPins(SS, RESET, DIO0);

These lines include the libraries required and define the DIO0, SS and RESET pins required to use the IoT-BUs LoRa board.

.. code-block:: c++

    if (!LoRa.begin(915E6)) {
        Serial.println("Starting LoRa failed!");
        while (1);
    }

These lines attempt to start LoRa and will go no further if failure.    

.. code-block:: c++

    // try to parse packet
    int packetSize = LoRa.parsePacket();
    if (packetSize) {
        // received a packet
        Serial.print("Received packet '");

These lines will check if a packet has been received and get its size.

.. code-block:: c++

    // read packet
    while (LoRa.available()) {
        Serial.print((char)LoRa.read());
    }

These lines will read the packet until there's no more data.

.. code-block:: c++

    Serial.println(LoRa.packetRssi());

This line will print out the signal strength indicator.    

.. code-block:: c++

    #include <SPI.h>
    #include <LoRa.h>

    #define DIO0 35
    #define SS   5
    #define RESET 17


    void setup() {

        LoRa.setPins(SS, RESET, DIO0);
        Serial.begin(115200);
        while (!Serial);

        Serial.println("LoRa Receiver");

        if (!LoRa.begin(915E6)) {
            Serial.println("Starting LoRa failed!");
            while (1);
        }
    }

    void loop() {
        // try to parse packet
        int packetSize = LoRa.parsePacket();
        if (packetSize) {
            // received a packet
            Serial.print("Received packet '");

            // read packet
            while (LoRa.available()) {
                Serial.print((char)LoRa.read());
            }

            // print RSSI of packet
            Serial.print("' with RSSI ");
            Serial.println(LoRa.packetRssi());
        }
    }
