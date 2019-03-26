# Arduino IDE and Board Setup

## 1. How to install the Arduino IDE and configure to the proper settings
1. Goto [https://www.arduino.cc/en/main/software](https://www.arduino.cc/en/main/software) 
2. Download the IDE

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/IDEDownload.png?raw=true">

3. Open the IDE

## 2. How to add ESP8266 library to the IDE
1. Click on File > Preferences
* On OSX, Click on Arduino (at the top), then Preferences
2. Enter `http://arduino.esp8266.com/versions/2.2.0/package_esp8266com_index.json` in the "Additional Boards Manager URLs:" field

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/PereferencesWindow.png?raw=true">

3. Tools > Boards > Board Manager
4. Filter for `ESP8266`

<img src="https://github.com/Snappsu/Coding-Bootcamp/blob/master/pics/BoardManager.png?raw=true">

5. Install the latest version of the library
6. Click on Tools > Boards > NodeMCU 1.0...

## 3. If there is extra plugin need and where to download the plugin

## 4. How to upload sketches to the module

# Tutorials and Examples

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
[Sketch File](https://github.com/Snappsu/Coding-Bootcamp/blob/master/sketches/BlinkingLightSketch.ino) [Raw Text](https://raw.githubusercontent.com/Snappsu/Coding-Bootcamp/master/sketches/BlinkingLightSketch)
