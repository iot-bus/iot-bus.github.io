.. _example-iot-bus-hello-world:

IoT-Bus Hello World Example
===========================

This example shows the simplest way to create a web-server and uses a truly asynchronous approach. 

.. code-block:: c++ 

    #include <WiFi.h>
    #include <AsyncTCP.h>
    #include <ESPAsyncWebServer.h>

The WiFi library is required to be able to connect to WiFi.
ESPAsyncWebServer provides the asynchronous web-server and AsyncTCP is required for an asynchronous TCP stack to support it.

.. code-block:: c++ 

    const char* ssid = "........";
    const char* password =  "........";

Enter the ssid and password of the local WiFi network you want to connect to.    

.. code-block:: c++ 

  Serial.begin(115200);
  
  WiFi.begin(ssid, password);
  
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }
  
  Serial.println(WiFi.localIP());

Start serial output, startup wireless and wait for connection. 
Print out the ip so you can connect to it from your browser.
This loop will never end if you do not have a correct ssid and password.

.. code-block:: c++ 

  server.on("/", HTTP_GET, [](AsyncWebServerRequest *request){
    request->send(200, "text/html", "<p>Hello World!</p>");
  });

  server.on("/html", HTTP_GET, [](AsyncWebServerRequest *request){
    request->send(200, "text/html", "<p>Some HTML!</p>");
  });

This section tells the server that on receiving an HTTP 
get request for '/' or for '/html' respond with a normal 
HTTP response (200) and provide some html response.

The examples provided with ESPAsyncWebServer are 
somewhat more sophisticated. Take a look at them.

.. code-block:: c++ 

    server.begin();

Start the web-server.

The full example.

.. code-block:: c++ 

    #include <WiFi.h>
    #include <AsyncTCP.h>
    #include <ESPAsyncWebServer.h>
    
    const char* ssid = "........";
    const char* password =  "........";
    
    AsyncWebServer server(80);
    
    void setup(){
    Serial.begin(115200);
    
    WiFi.begin(ssid, password);
    
    while (WiFi.status() != WL_CONNECTED) {
        delay(1000);
        Serial.println("Connecting to WiFi...");
    }
    
    Serial.println(WiFi.localIP());
    
    server.on("/", HTTP_GET, [](AsyncWebServerRequest *request){
        request->send(200, "text/html", "<p>Hello World!</p>");
    });

    server.on("/html", HTTP_GET, [](AsyncWebServerRequest *request){
        request->send(200, "text/html", "<p>Some HTML!</p>");
    });
    
    server.begin();
    }
    
    void loop(){
    }
