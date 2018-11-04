.. _iot-bus-getting-started:

Choosing a Platform and Framework
=================================

One of the great things about IoT-Bus is that you're free to choose from a large number of platforms and
frameworks. You know that you want to create an IoT project but where do you start? 
In our view it very depends on what you know now. 


Arduino
-------

If you have never programmed or know nothing about embedded hardware then you may be best to 
start with Arduino as a framework and as an editor and programmer. 
Similarly, if you are in education and do not want to be explaining things to yous students about the IDE and 
just want to create very simple applications then again, you may pick
Arduino as a Framework and as your development environment. Many, many users have chosen Arduino overs the years 
and many still do. It's a great place to start. You'll find more projects on the web that Arduino based so if you want to find 
somebody that's done something similar to what you want to do. You'll probably find it as an Arduino project somewhere. 

PlatformIO
----------

On the other hand if you are a professional programmer or a serious hobbyist then you will 
probably pick PlatformIO. There are other environments that are just fine if you already use them like Eclipse or NetBeans.
But if you are investing your time and money in the future then PlatformIO is the way to go. 
It's also not hard to take that same project and import it into PlatformIO and take it from there.

Similarly, if maintaining source code integrity, versioning and testing and debugging  are becoming more important you as a Arduino user then take a look at PlatformIO. 
The advantage that PlatformIO has taken of leveraging an excellent open IDE from Microsoft and extending it, again, in open fashion to the embedded world
If you're a seasoned C++ programmer then PlatformIO and the esp-idf framework is probably the way to go. 

Now in terms of framework you again have a choice. Arduino or esp-idf are the c++ development choices. 
Arduino is simpler and more "black-box" - you can get going very quickly and without necessarily fully understanding 
everything you can get an IoT project up and running. However, if things like a multi-tasking environment and the availability of 
professional-class libraries and support are more important then esp-idf is more likely to be the framework for you. 
It is lower-level and you may have to do more work but you are also more likely to get a professional application as a result.

There is a "third-way" option of using Platformio as your development environment and using 
Arduino as your framework if you are a new user or already familiar with Arduino libraries. This option perhaps gives you the best of both worlds. 
You're able to get up and running quickly and it would be easier to move to esp-idf you should choose to.

MicroPython
-----------

Python is becoming ubiquitous (this documentation was produced using it!). 
And MicroPython is a great implementation of python for the embedded environment.
So if you are already familiar with python that's a great way to leverage the IoT-Bus system. 
We'll show you later in this section how to get started with it.

moddable
--------

Javascript is another great alternative. It's not only used in front-end code, there are 
dedicated servers for it and a whole development infrastructure that has sprung up around it.
And moddable is the company that just "does javascript right'. We'll show you later in this section how to get started with it.

MicroBlocks
------------

Lastly there are other choices that may be even better when teaching students graphically such as MicroBlocks which runs wonderfully on IoT-Bus
and does not require traditional line-by-line programming.


Mozilla-IoT
-----------

Now Mozilla IoT is not a platform in the same sense of others here. But it certainly is a platform for IoT and irrespective of the framework or the 
language you can take advantage of Mozilla IoT to discover, inspect and control your IoT devices. So if you're thinking about a smart-home, a home security project 
or simply want the ability to control a device at home from your phone or PC then do look at Mozilla IoT 


Summary
-------

So what would I do today? 

1. Buy a kit from oddWires. 

2. Choose a platform/framework. You can't really go wrong. Your investment in IoT-Bus will work in every case and you can change your mind!

3. Get started with IoT-Bus and Mozilla IoT!

