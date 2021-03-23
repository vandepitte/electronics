# Program ATtiny85 For Beginners

The long story: https://www.arduino.cc/en/Tutorial/BuiltInExamples/ArduinoISP

## Prerequisites

* Breadboard
* Bunch of male to male dupont wires
* Arduino Uno (will be used as ISP)
* Arduino IDE installed

## Setup Arduino IDE

* Load Arduino ISP sketch: File > Examples > ArduinoISP > ArduinoISP
* Set Board: Tools > Board: Arduino Uno
* Set Port: Tools > Port

## Upload ArduinoISP sketch

## Setup ciruit

MISO, MOSI and SCK are availabe on multiple pins on Arduino UNO. Besides the AVR ISP
Using the Arduino Uno, there are 2 options. You either use the AVR ISP pins (the group of 6 pins on the Arduino Uno board labeled with ICSP) or you use the numbered pins on the board. Just use what you prefer on Arduino Uno. The AVR ISP pinout is described in the comments of the ArduinoISP sketch. Otherwise, use the following wiring instructions:

Arduino Uno -> ATtiny85:

* D10 (RESET) -> 1 (RESET)
* D11 (MOSI) -> 5 (MOSI)
* D12 (MISO) -> 6 (MISO)
* D13 (SCK) -> 7 (SCK)
* 5V -> 8 (VCC)
* GND -> 4 (GND)

TODO: circuit image

## Add Board

I will upload code to an ATtiny85. Therefor, I need to first install configurations (fuses?) for the right board. 

First configure the Boards Manager URL in Preferences: https://raw.githubusercontent.com/damellis/attiny/ide-1.6.x-boards-manager/package_damellis_attiny_index.json

Then add the Boards

* Tools > Board > Boards Manager...
* Search for attiny
* Click Install

## Configure Arduino IDE

* Set Arduino as ISP: Tools > Programmer > Arduino as ISP
* Set Board: Tools > Board: ATtiny
* Set Processor: Tools > Processor: ATtiny85
* Set Clock: Tools > Clock: 1Mhz is more than sufficient (not sure how much attiny85 takes) 
* Set Port: Tools > Port

## Burn bootloader? No

In instructions I found on the web, they say that you have to burn the bootloader. This seemed odd to me because the bootloader is in fact doing the job of an ISP: on startup it checks if there's new code and if so, it copies the code and runs it.

I tried uploading a sketch (next step) without burning a bootloader on a brand new ATtiny85 and it seems to work just fine.

I do think you need to burn the bootloader if you want to upload sketches without using the intermediate Arduino ISP.

## Upload the sketch


Take any sketch. The simplest to start with is the blink sketch. Just make sure you change LED_BUILTIN to an existing port on the ATtiny

I used a sketch to send an RF signal.

TODO: link to the code

What happens? 

TODO: find out what happens between IDE and Arduino Uno

1. Arduino Uno receives the sketch
1. Using RESET pin, Arduino Uno unlocks the bootloader section of the chip
2. Setting the fuses (configuration parameters) on the chip
3. Uploading the code on the chip
4. Locking back the bootloader section 

