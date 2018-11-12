.. _iot-bus-mozilla-touch-switch:

Touch Switch Thing Tutorial
===========================

If you haven't already installed your IDE do so now. We are going to use PlatformIo. 
See the section on :ref:`Getting Started with PlatformIO <getting-started-with-platformio>` for details. 
If you prefer to use Arduino you can follow the instruction :ref:`here <getting-started-with-arduino>`.

Get the IoT-Bus examples from Github. Download or clone the PlatformIO examples from 
here `here <https://github.com/iot-bus/iot-bus-mozilla-iot-examples-platformio>`_. 
The Arduino examples can be found :ref:`here <https://github.com/iot-bus/iot-bus-mozilla-iot-examples-arduino>`

This tutorial requires an IoT-Bus Io ESP32 processor board and a simpler jumper lead connected to GPIO4. Once running you will be able to use a capacitive switch on a 
GPIO pin on the IoT-Bus Io to be exposed to the Mozilla-IoT browser interface. Holding the jumper wire will cause the switch to trip. You will need to have installed the 
Mozilla-IoT gateway on a Raspberry PI as described :ref:`here <getting-started-with-mozilla-iot>`.

.. code-block:: c++

    #include <Arduino.h>
    #include "Thing.h"
    #include "WebThingAdapter.h"

These lines include the Arduino framework and the Mozilla-IoT device and adapter libraries. 
If you are using the examples for Platformio, these libraries and their pre-requisites 
will automatically be installed in your project.

.. note:: The ESPAsyncWebServer and AsyncTCP libraries are pre-requisites and also need installing. 

.. code-block:: c++

    //TODO: Hard-code your WiFi credentials here (and keep it private)
    const char* ssid = ".........";
    const char* password = ".........";

Enter your WiFi ssid and password so that the IoT-Bus board can access your WiFi.

.. code-block:: c++

    // Uses a touch sensor to detect input and turn on a LED
    int ledPin = 5; // choose the pin for the LED
    int touchPin = 4; // choose the input pin - T0 is the same as GPIO4

These define the input pin and the local LED to show the status.

.. code-block:: c++

    const char* sensorTypes[] = {"binarySensor", nullptr};
    ThingDevice touch("Touch", "ESP32 Touch Input", sensorTypes);
    ThingProperty touched("true", "", BOOLEAN, "BooleanProperty");
    ThingPropertyValue sensorValue;

    WebThingAdapter* adapter;

This defines a pointer to a Mozilla-IoT adapter which is set when a new adapter is created in setup as below.  

.. code-block:: c++

        adapter = new WebThingAdapter("adapter", WiFi.localIP());        

.. code-block:: c++

    const char* sensorTypes[] = {"binarySensor", nullptr};
    ThingDevice touch("Touch", "ESP32 Touch Input", sensorTypes);
    ThingProperty touched("true", "", BOOLEAN, "BooleanProperty");
    ThingPropertyValue sensorValue;

These are the the lines of code that define the Mozilla-IoT Thing and its properties.

.. code-block:: c++

    const char* sensorTypes[] = {"binarySensor", nullptr};

This line defines an array of types ended by a null pointer. These types are @types, that is they are pre-defined types that 
the Mozilla-IoT platform understands semantically. That is, what they are and how to render and interface with them.  
In this case it is a binarySensor.  

.. code-block:: c++

    ThingDevice touch("Touch", "ESP32 Touch Input", sensorTypes);

This line defines a touch switch named Touch. Note the reference to sensorTypes which is what actually 
defines the device type or types. So we are saying Touch is a binarySensor. Officially these  are described as capabilities. You can find the current list available `here <https://iot.mozilla.org/schemas/>`_. 

.. code-block:: c++

    ThingProperty touched("true", "", BOOLEAN, "BooleanProperty");

This defines a property "true" which has a property type of BooleanProperty. Again, this is a predefined property type.     

.. note:: There is no connection between the property and the device or adapter at this point. 
Although there is no mention of an adapter here, it is an adapter that connects to a gateway and exposes its capabilities. 

.. code-block:: c++

    touch.addProperty(&touched);
    adapter->addDevice(&touch);
    adapter->begin();

These three lines add the touched property to the led, then add the touch device to the adapter and then start the adapter. 
Once the adapter has started it can be recognized by the gateway.  

Most of the rest is boiler plate, but do note that you'll want to take note of the ip address that is displayed on the serial monitor once
WiFi has started because you can use that ip address to get the raw json response provided by the device once it is up and running. This is useful for debugging
because you can see exactly what will be provided to the gateway.

.. code-block:: c++

    int val = touchRead(T0); // get value using T0 / GPIO4

    Serial.println(val);  
    if (val < threshold){
        sensorValue.boolean = true;
        digitalWrite(ledPin, HIGH);
    }
    else{
        sensorValue.boolean = false;
        digitalWrite(ledPin, LOW);
    }
    touched.setValue(sensorValue);
    adapter->update();
    delay(300);

.. note:: sensorValue must not be allocated on the stack. 
It must be in a location that can be referred to asynchronously, so we have allocated it globally for simplicity. 
You'll get a memory trap if you allocate it on the stack.   

In the main loop we read the touch value and check against a threshold. We could also change this to reflect a multi-level value 
rather than a binary value if we wished. The ED and sensorValue are set to reflect the reading of T0 and the adapter is updated.

.. note:: T0 is the same as GPIO 4, either way of referencing the pin is fine.

So now we have run through the code, let's create a Thing and add it to the gateway.

Creating a Thing
----------------

Start up the previously installed and configured Mozilla-IoT gateway on your Raspberry Pi and look for this screen.

.. image:: ../_static/mozilla_add_things.png
    :align: center
    :alt: Mozilla Add Things
    :width: 100%

Your Thing should be found. Save it and click Done. You should now be able to click on the thing an get a display like this:

.. image:: ../_static/mozilla_touch.png
    :align: center
    :alt: Mozilla LED
    :width: 100%

The LED should respond to you turning it off and on in the Mozilla IoT interface! 
There are lots more examples in the Github file you downloaded or cloned. 

The full code is shown below.

.. code-block:: c++

    #include <Arduino.h>
    #include <Thing.h>
    #include <WebThingAdapter.h>

    /*
    Simple binary sensor example using ESP32 capacitive touch input
    This example code is in the public domain.
    */

    //TODO: Hard-code your WiFi credentials here (and keep it private)
    const char* ssid = "........";
    const char* password = "........";

    // Uses a touch sensor to detect input and turn on a LED
    int ledPin = 5; // choose the pin for the LED
    int touchPin = 4; // choose the input pin - T0 is the same as GPIO4

    WebThingAdapter* adapter;

    const char* sensorTypes[] = {"binarySensor", nullptr};
    ThingDevice touch("Touch", "ESP32 Touch Input", sensorTypes);
    ThingProperty touched("true", "", BOOLEAN, "BooleanProperty");
    ThingPropertyValue sensorValue;

    int threshold = 40;

    void setup() {
        Serial.begin(115200);

        // Start WiFi
        WiFi.mode(WIFI_STA);
        WiFi.begin(ssid, password);
        Serial.println("");

        // Wait for connection
        while (WiFi.status() != WL_CONNECTED) {
            delay(500);
            Serial.print(".");
        }

        Serial.println("");
        Serial.print("Connected to ");
        Serial.println(ssid);
        Serial.print("IP address: ");
        Serial.println(WiFi.localIP());

        // Initialize MOZ IoT thing
        adapter = new WebThingAdapter("adapter", WiFi.localIP());
        touch.addProperty(&touched);
        adapter->addDevice(&touch);
        adapter->begin();

        pinMode(ledPin, OUTPUT); // declare LED as output   
    }

    void loop() {

        int val = touchRead(T0); // get value using T0 / GPIO4

        Serial.println(val);  
        if (val < threshold){
            sensorValue.boolean = true;
            digitalWrite(ledPin, HIGH);
        }
        else{
            sensorValue.boolean = false;
            digitalWrite(ledPin, LOW);
        }
        touched.setValue(sensorValue);
        adapter->update();
        delay(300);
    }