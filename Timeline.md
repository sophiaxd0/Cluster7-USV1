# USV 1 Documentation

Team Members: Poorvi, Sam, Sophia, Solel

<img src="https://github.com/sophiaxd0/Cluster7-USV1/blob/main/images/usv1.jpg" width="30%" height="30%" />

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
[Camera Encloser](https://cad.onshape.com/documents/38377454961fcb99414ea19a/w/7607531d0b753042a246faf8/e/cd5d48836e7511ebab62a972?renderMode=0&uiState=64c92cd7a62ede3a7bc46788)

[Battery Box](https://cad.onshape.com/documents/52999a36e4d2f8787a262807/w/c4f805fec19dec18ea58386f/e/69482a6c11e3da87f98eadfe)

[Fin](https://cad.onshape.com/documents/23a63c0613274fd4bb029624/w/80638e86d99e1df4d45739fd/e/1327aad2d719c418d190c8e9)

[Board Encloser](https://cad.onshape.com/documents/0dca681ce908ec9cd0f42ce7/w/a8749228c95b8654e84dff5e/e/cc40f212ca8882072b8bcd19)


## Electronics
### Flight Controller
In general, the H743 was easy to use since all the pins are labelled. Some pins, especially ground and signal pins, would break if too much force was applied while wiring

Also, pay attention to which side the front of the flight controller is, so that when screwing it down to the box, the orientation is correct and you don't need to correct it through Mission Planner 
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

Later on, Dr Jay gave us a presentation on how to calibrate the controller and configure the switches on the controller to toggle between manual and autonomous drive (configurations both on the controller screen and Mission Planner)
### GPS
Wiring the GPS was pretty simple after finding the pinout, but we had issues with the GPS not showing up in Mission Planner

Many groups had malfunctioning GPS/compasses, so we ended up ordering new ones and they worked well. Sometimes, when a new GPS is connected, Mission Planner's config tab needs to be reset to the initial configurations. 

### Electronics Box
<img src="https://github.com/sophiaxd0/Cluster7-USV1/blob/main/images/electronics_box.jpg" width = "30%" height = "30%" />

### Thrusters
The thrusters also had to be soldered in order to connect to the board correctly. In Misson Planner's Servo Output tab, we set the pins connected to each thruster to "ThrottleRight" and "ThrottleLeft". In order to figure out right and left, observe which motor spins clockwise and counterclockwise. If Mission Planner doesn't allow changing Servo Outputs, check the arming settings in the Config tab. 

## Board Design Process

To make our USV, we first had to make sure our electronics were protected and stable. We 3-D printed a GPS enclosure, battery container, and microcontroller enclosure to secure our software inside our waterproof box. Later, we used tape and velcro to secure items after we switched our gps and needed to attach our radios.  We then soldered new wires to our microcontroller, GPS, thrusters, and battery so all items could be connected. Next, we 3-D printed new mounts and drilled through our board to attach our two thrusters, and a buoy mount. Although we attempted to use velcro to attach our box to the board, we switched to screws later for more stability. We also used cable glands to get wires from our thrusters into the box. In our final week, we attached a fin to gain more stability in our steering. 


## Mission Planner
Once we had all the instruments attached and calibrated, we created a route with the Plan tab of Mission Planner. 

Clicking on the map will create a new waypoint. To loop the waypoints, set the last waypoint to "Do Jump", the first column to 1(for Waypoint 1) and the repeats column to -1 for infinite repetitions. 

<img src="https://github.com/sophiaxd0/Cluster7-USV1/blob/main/images/waypoints.png" width="50%" height="50%"/>

## Final Project: ESP32 Camera 
<img src = "https://github.com/sophiaxd0/Cluster7-USV1/blob/main/images/camera.jpg" width="30%" height="30%"/>
For the lake test, we used the CameraWebServer example from the ESP32Lab library. However, this requires WiFi and we weren't able to set up a router. 

For the rest of this project, we wanted to use the camera to detect trash on the lake, so we trained an object detection model following [this tutorial](https://eloquentarduino.com/esp32-camera-object-detection/). This model is very easy to use, but isn't as powerful compared to YOLO or R-CNN models, so if we had more time to implement/a more powerful camera, we would have tried one of those. 

Object Detection Data

<img src = "https://github.com/sophiaxd0/Cluster7-USV1/blob/main/images/serial_detection.jpg" width="30%" height="30%"/>

Since the data from that tutorial prints into the Serial Monitor, which can't be seen when the ESP32 is not connected to the computer through USB, we used [this Web Server tutorial](https://randomnerdtutorials.com/esp32-web-server-sent-events-sse/#demonstration) and slightly modified it to our purposes. However, running the server requires WiFi and makes the detection very slow, so we would probably just use radio communication in the future. 
