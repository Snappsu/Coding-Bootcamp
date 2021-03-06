# Table of Contents
## Getting Started

0. Setting Up The Computer
1. Installing the Arduino IDE
2. Adding ESP8266 Library to the IDE
3. Adding Extra Plugins
4. Configuring the Upload Settings
5. Uploading a sketch to the module

## Samples

1. Blank Sketch
2. Blinking Light
3. WiFi Access Point

# Getting Started
<h2 style="color: #e22; text-align: center;">WARNING:</h2>
In order to complete this guide, you will need administrative powers in order to install the required drivers.

## 0. Setting Up The Computer
1. Install the USB drivers for the NodeMCU
* For Windows...
* For OS X, I have the files hosted [here](https://github.com/Snappsu/Coding-Bootcamp/tree/master/drivers/OSX), then download and install the pkg and dmg. The computer will have to restart at least once. Security may stop drivers from loading, so open System Preferences, click "Security & Privacy", and allow the two drivers to run.

## 1. Installing the Arduino IDE
1. Go to [https://www.arduino.cc/en/main/software](https://www.arduino.cc/en/main/software) 
2. Download and install the IDE
* On Windows, get the ZIP file download to avoid having to enter an admin password

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/IDEDownload.png?raw=true">

3. Open the IDE

## 2. Adding ESP8266 Library to the IDE
1. Click on File > Preferences
* On Windows, click on 'File' (at the top of the window), then 'Preferences'
* On OS X, click on 'Arduino' (at the top), then 'Preferences'
2. Enter `http://arduino.esp8266.com/versions/2.2.0/package_esp8266com_index.json` in the "Additional Boards Manager URLs:" field

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/PereferencesWindow.png?raw=true">

<span style="color:#f90">Note:</span> The "Sketchbook Location" is where your code will be saved. You can change it to wherever you want.

3. Tools > Boards > Board Manager
4. Filter for `ESP8266`

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/BoardManager.png?raw=true">

5. Install the latest version of the library

## 3. Adding Extra Plugins (and Where to Download Them)

## 4. Configuring the Upload Settings
1. Plug in the NodeMCU in to the PC

### 4.1 Picking the Board
1. At the top, click on "Tools"
2. Hover over "Board: ..."
3. Select "NodeMCU 1.1 (ESP-12E Module)"

### 4.2 Picking the upload speed
1. At the top, click on "Tools"
2. Hover over "Upload Speed: ..."
3. Select "115200"

### 4.3 Picking the CPU frequency
1. At the top, click on "Tools"
2. Hover over "CPU Frequency: ..."
3. Select "80 MHz"

### 4.4 Picking the flash size
1. At the top, click on "Tools"
2. Hover over "Flash Size: ..."
3. Select "4M (3M SPIFFS)"

### 4.5.1 Picking the port
1. At the top, click on "Tools"
2. Hover over "Port: ..."
3. Select the module's port
* On Windows, look for something called "COMX" where "X".
* On OS X, look for something with "wchusbserial", then proceed to step 5. If you get an error involving "wrong direction/command", try selecting the next port.

<span style="color:#f90">Note:</span> If you're having trouble finding the right port, try unplugging the module, observing the list of avaiable ports, then pluging in the module into the same port, and looking for any differences.

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/UploadSettings.png?raw=true">

When you open the tools menu, it should look like this, though the "port" may be different.

## 5. Uploading a sketch to the module

1. At the top left, click the arrow pointing right.

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/UploadButton.png?raw=true">

2. If everything is correct the bottom of IDE should look like this.

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/ConsoleUpload.png?raw=true">

# Samples

## Blank Arduino Sketch
```ino
void setup() {
  // put your setup code here, to run once:

}
void loop() {
  // put your main code here, to run repeatedly:

}
```

## Blinking Light

```ino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```
[[Sketch File](https://github.com/Snappsu/Coding-Bootcamp/blob/master/sketches/BlinkingLightSketch.ino)] [[Raw Text](https://raw.githubusercontent.com/Snappsu/Coding-Bootcamp/master/sketches/BlinkingLightSketch.ino)]

## Wifi Access Point
```ino
#include <ESP8266WiFi.h>
#include <WiFiClient.h>
#include <ESP8266WebServer.h>
 
// Replace with your network credentials
const char* ssid = "WiFi_Name_Here";
const char* password = "WiFi_Password_Here";
 
ESP8266WebServer server(80);   //instantiate server at port 80 (http port)
 
String page = ""; //Creates the HTML Page
int LEDPin = 2;
void setup(void){
  //the HTML of the web page
  page = "<h1>Simple NodeMCU Web Server</h1><p><a href=\"LEDOn\"><button>ON</button></a>&nbsp;<a href=\"LEDOff\"><button>OFF</button></a></p>";
  //make the LED pin output and initially turned off
  pinMode(LEDPin, OUTPUT);
  digitalWrite(LEDPin, LOW);
   
  delay(1000);
  Serial.begin(115200);
  WiFi.softAP(ssid, password); //begin WiFi access point
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
  Serial.println(WiFi.softAPIP()); 
   
  server.on("/", [](){
    server.send(200, "text/html", page);
  });
  server.on("/LEDOff", [](){
    server.send(200, "text/html", page);
    digitalWrite(LEDPin, HIGH);
    delay(1000);
  });
  server.on("/LEDOn", [](){
    server.send(200, "text/html", page);
    digitalWrite(LEDPin, LOW);
    delay(1000); 
  });
  server.begin();
  Serial.println("Web server started!");
}
 
void loop(void){
  server.handleClient();
}
```
[[Sketch File](https://github.com/Snappsu/Coding-Bootcamp/blob/master/sketches/WiFiAccessPoint.ino)] [[Raw Text](https://raw.githubusercontent.com/Snappsu/Coding-Bootcamp/master/sketches/WiFiAccessPoint.ino)]
