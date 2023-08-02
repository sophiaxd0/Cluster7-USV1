# USV 1 Documentation

Team Members: Poorvi, Sam, Sophia, Solel

<img src="https://github.com/sophiaxd0/Cluster7-USV1/blob/main/IMG_1008.jpg" width="30%" height="30%" />

## Initial Research

When we got each part, we were pretty confused on what to do with them since we didn’t have any knowledge on pinouts, and many wires had cable grove adapters instead of regular female heads (which were needed to connect to the pins on the microcontroller)

We researched the pinout for the GPS, receiver, thrusters and radios, and also found the pinout for the Mateksys H743 

  (Later, we realized that we needed to solder the GPS and radio to jumper wires with female pin heads) 
## Given Instruments and Documentation Used

[Mateksys H743 V3 Flight Controller](http://www.mateksys.com/?portfolio=h743-wing-v2)

[SiK Telemetry Radios](https://ardupilot.org/copter/docs/common-sik-telemetry-radio.html)

[TGY-i6S Controller and Receiver](https://hobbyking.com/en_us/turnigy-tgy-i6s-mode-1-digital-proportional-radio-control-system-black.html)

M80 Pro GPS (switched from Readytosky NEO-M8N GPS)

## Given Hardware
Waterproof Electronics Box, 1.5kg thrusters, body board

## CAD Files

## Wiring Process
### Radios
We used the SiK v3 radios. One radio connects through USB to a PC running Mission Planner, and the other connects to the microcontroller

The microcontroller must be powered by a battery, not a computer, for the “boat” radio to work correctly 
When both are powered correctly, there should be a blinking green light. Once they are connected, there is a solid green light. Other lights (red or orange) will appear when the radios are communicating or Mission Planner is loading, but the green should always be on if the radios are powered correctly
For our group, the issue was that we clicked “Upload Firmware”, which changed the code within the radios to the wrong firmware. And the radios didn’t work :( 

**Do not click “Upload Firmware”**

Other issues that may affect radio connection: making sure the baud rate is 57600, having the same Net ID (choose any number), checking that Tx is connected to Rx and vice versa 

In general, use Mission Planner to check that both radios are on the same settings 

### Controller and Reciever

We followed the binding instructions from the TGY-i6S manual to connect them to each other

To connect the receiver, we used the SBUS receiver pins. Make sure the wires are connected to Rx6 (not a different Rx) on the microcontroller 

Later on, Dr Jay gave us a presentation on how to configure the switches on the controller to toggle between manual and autonomous drive (configurations both on the controller screen and Mission Planner)
### GPS
Wiring the GPS was pretty simple after finding the pinout, but we had issues with the GPS not showing up in Mission Planner

Many groups had malfunctioning GPS/compasses, so we ended up ordering new ones and they worked well. Sometimes, when a new GPS is connected, Mission Planner's config tab needs to be reset to the initial configurations. 

<img src="https://github.com/sophiaxd0/Cluster7-USV1/blob/main/IMG_4217.HEIC" />

## Board Design Process

## Mission Planner

## Final Project: ESP32 Camera 
