.. _example-iot-bus-blink:

IoT-Bus Blink Example
======================

This very simple example needs little explanation. The first line includes the Arduino framework.

.. code-block:: c++

    #include <arduino.h>

The next line defined the GPIO of the pin of the onboard LED.

.. code-block:: c++

    #define LEDPin 5

This line sets the GPIO pin into output mode.

.. code-block:: c++

    pinMode(LEDPin, OUTPUT);  

This line turns on the LED.     

.. code-block:: c++     

    digitalWrite(LEDPin, HIGH); 

This line turns off the LED.         

.. code-block:: c++  

    digitalWrite(LEDPin, LOW); 

This line creates  1 second delay.

.. code-block:: c++  

    delay(1000);  

The full example.

.. code-block:: c++  

    #include <arduino.h>

    #define LEDPin 5

    // the setup function runs once when you press reset or power the board
    void setup() {
        // initialize digital pin as an output.
        pinMode(LEDPin, OUTPUT);
    }

    // the loop function runs over and over again forever
        void loop() {
        digitalWrite(LEDPin, HIGH);   // turn the LED on (HIGH is the voltage level)
        delay(1000);                       // wait for a second
        digitalWrite(LEDPin, LOW);    // turn the LED off by making the voltage LOW
        delay(1000);                       // wait for a second
    }
