.. _example-iot-bus-motor:

Iot-Bus Motor Example
=====================

This example use the Adafruit_Motorshield library which you can find `here <https://github.com/adafruit/Adafruit_Motor_Shield_V2_Library>`_ 
to control a stepper motor on the IoT-Bus Motor board.

.. code-block:: c++

    /* 
    This is a test sketch for the iot-bus motor board
    */

    #include <Wire.h>
    #include <Adafruit_MotorShield.h>
    #include "utility/Adafruit_MS_PWMServoDriver.h"

    // Create the motor shield object with the default I2C address

    Adafruit_MotorShield AFMS = Adafruit_MotorShield(0x5F); 

Include necessary libraries and create a motor controller at address 0x5F. You can 
change the solder jumpers on the board for another address between 0x40 and 0x5F.

.. code-block:: c++

    // Connect a stepper motor with 200 steps per revolution (1.8 degree)
    // to motor port #2 (M3 and M4)
    Adafruit_StepperMotor *myMotor = AFMS.getStepper(200, 1);

Create a motor to refer to motor 2 on the motor board.

.. code-block:: c++

    AFMS.begin();  // create with the default frequency 1.6KHz
    //AFMS.begin(1000);  // OR with a different frequency, say 1KHz

Start up the motor.

.. code-block:: c++

    Serial.println("Single coil steps");
    myMotor->step(100, FORWARD, SINGLE); 
    myMotor->step(100, BACKWARD, SINGLE); 

    Serial.println("Double coil steps");
    myMotor->step(100, FORWARD, DOUBLE); 
    myMotor->step(100, BACKWARD, DOUBLE);
    
    Serial.println("Interleave coil steps");
    myMotor->step(100, FORWARD, INTERLEAVE); 
    myMotor->step(100, BACKWARD, INTERLEAVE); 
    
    Serial.println("Microstep steps");
    myMotor->step(50, FORWARD, MICROSTEP); 
    myMotor->step(50, BACKWARD, MICROSTEP);

Move the stepper motor forward and backward in different ways. The full example is shown beow.

.. code-block:: c++

    /* 
    This is a test sketch for the iot-bus motor board
    */

    #include <Wire.h>
    #include <Adafruit_MotorShield.h>
    #include "utility/Adafruit_MS_PWMServoDriver.h"

    // Create the motor shield object with the default I2C address

    Adafruit_MotorShield AFMS = Adafruit_MotorShield(0x5F); 

    // Connect a stepper motor with 200 steps per revolution (1.8 degree)
    // to motor port #2 (M3 and M4)
    Adafruit_StepperMotor *myMotor = AFMS.getStepper(200, 1);

    void setup() {
    Serial.begin(115200);           
    Serial.println("Stepper test!");

    AFMS.begin();  // create with the default frequency 1.6KHz
    //AFMS.begin(1000);  // OR with a different frequency, say 1KHz
    
    myMotor->setSpeed(10);  // 10 rpm   
    }

    void loop() {
        Serial.println("Single coil steps");
        myMotor->step(100, FORWARD, SINGLE); 
        myMotor->step(100, BACKWARD, SINGLE); 

        Serial.println("Double coil steps");
        myMotor->step(100, FORWARD, DOUBLE); 
        myMotor->step(100, BACKWARD, DOUBLE);
        
        Serial.println("Interleave coil steps");
        myMotor->step(100, FORWARD, INTERLEAVE); 
        myMotor->step(100, BACKWARD, INTERLEAVE); 
        
        Serial.println("Microstep steps");
        myMotor->step(50, FORWARD, MICROSTEP); 
        myMotor->step(50, BACKWARD, MICROSTEP);
    }
