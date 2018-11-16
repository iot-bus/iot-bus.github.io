.. _example-iot-bus-touch-draw:

IoT-Bus Touch Draw Example
=============================

This example demonstrates the use of both the IoT-Bus Display and the touchscreen. 
In this example we are using a forked version of Bodmer's `TFT_eSPI <https://github.com/iot-bus/TFT_eSPI>`_ library with User_Setup already setup for IoT-Bus Display which you can find here.  
We are also using a forked version of Paul Stoffgren's `XPT2046_Touchscreen <https://github.com/iot-bus/XPT2046_Touchscreen>`_ library which has been enhanced to perform mapping of raw touch Data to screen coordinates. 
It has also been modified to disable the PENIRQ line so that we use one less pin. 
You will find other examples in the examples repository that use Adafruit libraries that work in a very similar way.

.. code-block:: c++ 

    // include touchscreen library
    #include <XPT2046_Touchscreen.h>

    // Call up the TFT driver library
    #include <TFT_eSPI.h> // Hardware-specific library
    #include <SPI.h>

    // Invoke custom TFT driver library
    TFT_eSPI tft = TFT_eSPI();       // Invoke custom library

    // These pins are defined in User_Setup.h and have already been setup to be correct for the IoT-Bus Display

    //#define TFT_MISO 19
    //#define TFT_MOSI 23
    //#define TFT_SCLK 18
    //#define TFT_CS    5  // Chip select control pin
    //#define TFT_DC    27  // Data Command control pin
    //#define TFT_RST  -1  // Set TFT_RST to -1 if display RESET is connected to ESP32 board RST

    /* Create an instance of the touch screen library */
    #define CS_PIN  16

    XPT2046_Touchscreen ts(CS_PIN);  // Param 2 - NULL - No interrupts

In the initial section of the example we include the libraries required, 
declare both the display and touch screen for use. 
We also define the CS_PIN as required for the touchscreen to be GPIO 16.

There is no need to define the rest of the pins as that has been done for you 
in User_Setup.h which is part of the TFT_eSPI library.

.. code-block:: c++ 

    // touchscreen  calibration values
    #define X_MIN 256
    #define X_MAX 3632
    #define Y_MIN 274
    #define Y_MAX 3579

These calibration values will vary from display to display. 
You can use the draw-corners example to find out the values for each corner
and change them for your displays. The values here are likely to be OK for initial testing
but you will get more accurate results by performing your own calibration.

.. code-block:: c++ 

    pinMode(33, OUTPUT);
    digitalWrite(33, HIGH);

These lines are critical as GPIO 33 is used to power on the back-light. 
The back-light is driven through a transistor to avoid drawing too much current from the GPIO.

.. code-block:: c++ 

    ts.begin();
    ts.setCalibration(X_MIN, X_MAX, Y_MIN, Y_MAX);

    tft.init();

These lines initialize and calibrate the touchscreen and display.

.. code-block:: c++ 

    // Set the TFT and touch screen to landscape orientation
    tft.setRotation(1);
    ts.setRotation(1);

Rotation 0 and 2 are portrait and 1 and 3 are landscape. 
This example will work in any of the rotations so you can change them and see the effect.
Remember to keep them in sync or you will get strange effects.

.. code-block:: c++ 

    tft.setTextSize(1);
    tft.fillScreen(TFT_BLACK);
    tft.setTextColor(TFT_GREEN);

This sets the default font-seize, sets the background to black and sets the current
text color. Note that much better smooth fonts are easily usable - 
take a look at the TFT_eSPI library documentation.

.. code-block:: c++ 

    swatchWidth = ts.getWidth()/10;
    swatchHeight = 34;

This example dynamically determines the display width so that it works in any orientation.    

.. code-block:: c++ 
    
    tft.fillRect(i * swatchWidth, 0, swatchWidth, swatchHeight, colors[i]);

This fills a rectangle with a color.

.. code-block:: c++ 

    tft.setCursor(ts.getWidth()-swatchWidth*1.5, 3, 2); // x,y,font
    tft.setTextColor(TFT_WHITE);
    tft.print("Clear");

These lines position the cursor, set the text color and write some text 
at the cursor position.

.. code-block:: c++ 

    if (ts.touched()) 

Use the touched function to find out whether the display has been touched. 

.. code-block:: c++

    TS_Point p = ts.getMappedPoint();

This will get an x, y and z value. Although it is not used here you could see how 
hard the press was by comparing the z value. Note that x and y are relative to the current 
origin which will vary by rotation. Note that the origin is always in the top left corner of 
the display as is traditional with graphical displays.  

In the remainder of the loop() function, some hit-testing is performed and 
if the press is on a color of the palette, the 
current color is changed. If the clear button is pressed, 
then the screen is cleared to the current color. Otherwise the point is drawn.

The full example is shown below.

.. code-block:: c++ 

    // include touchscreen library
    #include <XPT2046_Touchscreen.h>

    // Call up the TFT driver library
    #include <TFT_eSPI.h> // Hardware-specific library
    #include <SPI.h>

    // Invoke custom TFT driver library
    TFT_eSPI tft = TFT_eSPI();       // Invoke custom library

    // These pins are defined in User_Setup.h and have already been setup to be correct for the IoT-Bus Display

    //#define TFT_MISO 19
    //#define TFT_MOSI 23
    //#define TFT_SCLK 18
    //#define TFT_CS    5  // Chip select control pin
    //#define TFT_DC    27  // Data Command control pin
    //#define TFT_RST  -1  // Set TFT_RST to -1 if display RESET is connected to ESP32 board RST

    /* Create an instance of the touch screen library */
    #define CS_PIN  16

    XPT2046_Touchscreen ts(CS_PIN);  // Param 2 - NULL - No interrupts

    int color = TFT_WHITE;     //Starting paint brush color

    // Palette button colour sequence
    unsigned int colors[10] = {TFT_RED, TFT_GREEN, TFT_BLUE, TFT_BLACK, TFT_CYAN, TFT_YELLOW, TFT_WHITE, TFT_MAGENTA, TFT_BLACK, TFT_BLACK};

    // touchscreen  calibration values
    #define X_MIN 256
    #define X_MAX 3632
    #define Y_MIN 274
    #define Y_MAX 3579

    int swatchWidth;
    int swatchHeight;

    void setup()
    {
    Serial.begin(115200);

    pinMode(33, OUTPUT);
    digitalWrite(33, HIGH);

    ts.begin();
    ts.setCalibration(X_MIN, X_MAX, Y_MIN, Y_MAX);

    tft.init();
    
    // Set the TFT and touch screen to landscape orientation
    tft.setRotation(3);
    ts.setRotation(3);

    tft.setTextSize(1);
    tft.fillScreen(TFT_BLACK);
    tft.setTextColor(TFT_GREEN);

    swatchWidth = ts.getWidth()/10;
    swatchHeight = 34;
    
    //Draw the palette
    for (int i = 0; i < 10; i++)
    {
        tft.fillRect(i * swatchWidth, 0, swatchWidth, swatchHeight, colors[i]);
    }

    //Draw the clear screen button
    tft.setCursor(ts.getWidth()-swatchWidth*1.5, 3, 2); // x,y,font
    tft.setTextColor(TFT_WHITE);
    tft.print("Clear");
    tft.drawRect(0, 0, ts.getWidth()-1, swatchHeight, TFT_WHITE);

    // Plot the current colour in the screen clear box
    tft.fillRect(ts.getWidth() - swatchWidth, 20, 12, 12, color);
    }

    /* Main program */
    void loop()
    {
    // Check if the touch screen is currently pressed
    // Raw and coordinate values are stored within library at this instant

    if (ts.touched()) 
    {
        Serial.println("touched");
        // Read the current X and Y axis as mapped co-ordinates at the last touch time

        TS_Point p = ts.getMappedPoint();

        // mapped pixel
        Serial.print(p.x); Serial.print(","); Serial.println(p.y);
        
        // Detect paint brush color change
        if (p.y < swatchHeight + 2)
        {
            if (p.x / swatchWidth > 7)
            {
                // Clear the screen to current color
                tft.fillRect(0, swatchHeight, ts.getWidth(), ts.getHeight()-1, color);
                Serial.println("clear screen to current color");
            }
            else
            {
                color = colors[p.x / swatchWidth];
                // Update the current color in the clear box
                tft.fillRect(ts.getWidth() - swatchWidth, 20, 12, 12, color);
                Serial.println("Update the current color in the clear box");
            }
        }
        else
        {
            // draw a point
            tft.fillCircle(p.x, p.y, 2, color);
            Serial.println("fillcircle");
        }
    }
    }
