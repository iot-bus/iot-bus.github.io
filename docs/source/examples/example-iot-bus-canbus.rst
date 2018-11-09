.. _example-iot-bus-canbus:

Iot-Bus CAN Bus Example
=======================

These two examples work together using Sandeep Mistry's excellent arduino-CAN library which can be 
found `here <https://github.com/sandeepmistry/arduino-CAN>`_. 


CAN Bus Send
------------

.. code-block:: c++

    #include <CAN.h>

    void setup() {
        Serial.begin(115200);
    
        // start the CAN bus at 1000 kbps
        if (!CAN.begin(1000E3)) {
            Serial.println("Starting CAN failed!");
            while (1);
        }
    }

Include the CAN Bus library and start it up at 1Mbps. 

.. code-block:: c++

    CAN.beginPacket(0x12);
    CAN.write('h');
    CAN.write('e');
    CAN.write('l');
    CAN.write('l');
    CAN.write('o');
    CAN.endPacket();

Send a regular CAN packet.

.. code-block:: c++

    CAN.beginExtendedPacket(0xabcdef);
    CAN.write('w');
    CAN.write('o');
    CAN.write('r');
    CAN.write('l');
    CAN.write('d');
    CAN.endPacket();

Send an extended CAN packet. The program loops continuously sending packets. The full example is shown below.   

.. code-block:: c++

    // Copyright (c) Sandeep Mistry. All rights reserved.
    // Licensed under the MIT license. See LICENSE file in the project root for full license information.

    #include <CAN.h>

    void setup() {
        Serial.begin(115200);
    
        // start the CAN bus at 1000 kbps
        if (!CAN.begin(1000E3)) {
            Serial.println("Starting CAN failed!");
            while (1);
        }
    }

    void loop() {
        // send packet: id is 11 bits, packet can contain up to 8 bytes of data
        Serial.print("Sending packet ... ");

        CAN.beginPacket(0x12);
        CAN.write('h');
        CAN.write('e');
        CAN.write('l');
        CAN.write('l');
        CAN.write('o');
        CAN.endPacket();

        Serial.println("done");

        delay(1000);

        // send extended packet: id is 29 bits, packet can contain up to 8 bytes of data
        Serial.print("Sending extended packet ... ");

        CAN.beginExtendedPacket(0xabcdef);
        CAN.write('w');
        CAN.write('o');
        CAN.write('r');
        CAN.write('l');
        CAN.write('d');
        CAN.endPacket();

        Serial.println("done");

        delay(1000);
    }


CAN Bus Receive
---------------

.. code-block:: c++

    #include <CAN.h>

    void setup() {
        Serial.begin(115200);
        while (!Serial);

        Serial.println("CAN Receiver");

        // start the CAN bus at 1000 kbps
        if (!CAN.begin(1000E3)) {
            Serial.println("Starting CAN failed!");
            while (1);
        }
    }

Include the CAN Bus library and start it up at 1Mbps. 

.. code-block:: c++

    // try to parse packet
    int packetSize = CAN.parsePacket();

    if (packetSize) {
        // received a packet
        Serial.print("Received ");

See if we have received a packet and get its size.

.. code-block:: c++

    if (CAN.packetExtended()) {
        Serial.print("extended ");
    }

Identify an extended packet.

.. code-block:: c++

    if (CAN.packetRtr()) {
        // Remote transmission request, packet contains no data
        Serial.print("RTR ");
    }

Check if it is a remote transmission request.

.. code-block:: c++

    Serial.print(CAN.packetId(), HEX);

Print out the packet id.

.. code-block:: c++

    Serial.println(CAN.packetDlc());

If it is a remote transmission request, find out the requested length.

.. code-block:: c++

    Serial.print(" and length ");
    Serial.println(packetSize);

    // only print packet data for non-RTR packets
    while (CAN.available()) {
        Serial.print((char)CAN.read());
    }
    Serial.println();
 
If it is a regular packet, get its size and read the packet. The full example is shown below.

.. code-block:: c++

    // Copyright (c) Sandeep Mistry. All rights reserved.
    // Licensed under the MIT license. See LICENSE file in the project root for full license information.

    #include <CAN.h>

    void setup() {
        Serial.begin(115200);
        while (!Serial);

        Serial.println("CAN Receiver");

        // start the CAN bus at 1000 kbps
        if (!CAN.begin(1000E3)) {
            Serial.println("Starting CAN failed!");
            while (1);
        }
    }

    void loop() {
        // try to parse packet
        int packetSize = CAN.parsePacket();

        if (packetSize) {
            // received a packet
            Serial.print("Received ");

            if (CAN.packetExtended()) {
                Serial.print("extended ");
            }

            if (CAN.packetRtr()) {
                // Remote transmission request, packet contains no data
                Serial.print("RTR ");
            }

            Serial.print("packet with id 0x");
            Serial.print(CAN.packetId(), HEX);

            if (CAN.packetRtr()) {
                Serial.print(" and requested length ");
                Serial.println(CAN.packetDlc());
            } else {
                Serial.print(" and length ");
                Serial.println(packetSize);

                // only print packet data for non-RTR packets
                while (CAN.available()) {
                    Serial.print((char)CAN.read());
                }
                Serial.println();
            }

            Serial.println();
        }
    }
