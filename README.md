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
