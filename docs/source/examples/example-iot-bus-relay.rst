.. _example-iot-bus-relay:

Iot-Bus Relay Example
=====================

It is very easy to use the IoT-Bus relay. Simply set the relay pin high to turn on the relay as the relay is active high. 
The full example is shown below.

.. code-block:: c++

    /*   
    Turns the Relay on for one second, then off for one second, repeatedly.   
    This example code is in the public domain.   
    */

    #include <arduino.h>

    #define RelayPin 17

    // the setup function runs once when you press reset or power the board
    void setup() {
        // initialize digital pin Relay_BUILTIN as an output.
        pinMode(RelayPin, OUTPUT);
        Serial.begin(115200);
        Serial.println("Hello world");
    }

    // the loop function runs over and over again forever
    void loop() {
        digitalWrite(RelayPin, HIGH);   // turn the Relay on (HIGH is the voltage level)
        delay(1000);                       // wait for a second
        digitalWrite(RelayPin, LOW);    // turn the Relay off by making the voltage LOW
        delay(1000);                       // wait for a second
    }
