# JeloLamp

Jelo Lamp by Sam Wing

Jelo Lamp is a bed-side table lamp programmed to be critical of screen-time before falling asleep. It competes with the attention of the screen on your phone, laptop or mobile device by turning on its LED whenever it senses a spike in lighting within the room. Rather than working with lighting thresholds, the light relies on INPUT smoothing to function in different settings without altering code.

Components:
-Arduino Uno
-Photocell
-12V White LED
-12V PN2222A Transistor
-12V DC Connector

Video Link: https://vimeo.com/163035732

The circuit is relatively easy to set up, 12V power is achieved through VIN pin of the arduino and controlled as an output via 12V Transistor. Otherwise the circuit is quite simple with 1 input pin for photocell through the 5V power of the Arduino.


/*

  Smoothing

  Reads repeatedly from an analog input, calculating a running average
  and printing it to the computer.  Keeps ten readings in an array and
  continually averages them.

  The circuit:
    * Analog sensor (potentiometer will do) attached to analog input 0

  Created 22 April 2007
  By David A. Mellis  <dam@mellis.org>
  modified 9 Apr 2012
  by Tom Igoe
  http://www.arduino.cc/en/Tutorial/Smoothing

  This example code is in the public domain.


*/


// Define the number of samples to keep track of.  The higher the number,
// the more the readings will be smoothed, but the slower the output will
// respond to the input.  Using a constant rather than a normal variable lets
// use this value to determine the size of the readings array.
const int numReadings = 10;

int readings[numReadings];      // the readings from the analog input
int readIndex = 0;              // the index of the current reading
int total = 0;                  // the running total
int average = 0;                // the average

int inputPin = A0;
int LEDPin = 12;

void setup() {
  // initialize serial communication with computer:
  Serial.begin(9600);
  // initialize all the readings to 0:
  for (int thisReading = 0; thisReading < numReadings; thisReading++) {
    readings[thisReading] = 0;
  }
  pinMode (LEDPin, OUTPUT);
}

void loop() {
  // subtract the last reading:
  total = total - readings[readIndex];
  // read from the sensor:
  readings[readIndex] = analogRead(inputPin);
  // add the reading to the total:
  total = total + readings[readIndex];
 

  // calculate the average:
  average = total / numReadings;
  // send it to the computer as ASCII digits
  Serial.print(average);
  Serial.print("   ");
  Serial.println(readings[readIndex]);
  delay(350);        // delay in between reads for stability 


  if (readings[readIndex] > average + 30 ) {
    digitalWrite (LEDPin, HIGH);
  }
  else {digitalWrite (LEDPin, LOW);
  }
  
  // advance to the next position in the array:
  readIndex = readIndex + 1;
  // if we're at the end of the array...
  if (readIndex >= numReadings) {
    // ...wrap around to the beginning:
    readIndex = 0;
  }
}





