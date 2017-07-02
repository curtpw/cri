---
layout: default
---

![](https://curtpw.github.io/cri/images/cmicurt.jpg)

## []()**Master Class Project:**

# []()**Neuro Plasma Hacker**

## [](#master)*Wearable Devices, Neural Networks on Mobile Apps, Controlling IoT*

> Your goal is to **hack an off the shelf wearable device, send accelerometer data** from the hacked device **to a mobile app** which we will create, build **and train a neural network** in the mobile app to detect a specific set of wearable device data, and use the sensor data detection results **to control a modified plasma globe** connected to a Raspberry Pi over Bluetooth. I have divided the project into three separable parts. If all participants want to do mobile apps (the easiest from a hardware perspective) I can provide necessary sensor data for you. I also have a number of Arduino microcontrollers and a wide array of sensors (Heart Rate, gesture, proximity, accelerometer, gyroscope, GSR/EDA, pressure, stretch) for you to explore and play with if you want something simple.

[Part 1: Streaming Sensor Data From Wearable Device](#wearable-device)

[Part 2: MLP Neural Network of Mobile App Trained on Streaming Sensor Data](#mobile-app)

[Part 3: Relay on Raspberry Pi Controlled By Mobile App](#raspberry-pi)

[Alternate: Sensors on Arduino](#sensors)

All examples and documentation can be found here: [https://github.com/curtpw/masterclass-cri](https://github.com/curtpw/masterclass-cri)

~ Curt

**NOTE 1: Do you have little or no background in computer programming? Think you might end up spending hours trying to install obscure software, looking at code you don't understand, listenting to acronyms that might as well come from a random letter generator? DON'T WORRY!! If you are interested in the concepts, I can make this engaging for you - even if reading Foucault or Lacan seems easier that navigating the more technical material below. I promise. If you are looking for a place to start I recommend [Evothings](https://evothings.com/doc/index.html), especially [this example](https://evothings.com/doc/examples/cordova-accelerometer.html) which requires only a phone and involves no coding.** 

NOTE 2: I have prepared all materials for CRI using Windows 10 because many people without a technical background use Windows and I find it difficult to avoid because of how Nordic releases developer tools. I duel boot Linux on all my machines and can switch to Ubuntu if participants strongly prefer. 

## [](#wearable-device)**Wearable Device Streaming Sensor Data**
![](https://curtpw.github.io/cri/images/wearable.jpg)

You will be hacking a FitBit clone (the ID107 Plus) containing a Nordic nRF52832 SoC (System On a Chip) with a 64Mhz ARM microprocessor. This Device contains a Kionics KX022 Accelerometer and a Bluetooth 4 BLE transceiver. You can write code for the device using the Arduino IDE with Sandeep's Arduino Core for Nordic chips. I use a Segger JLink to program these devices but and SWD programmer will work. Hacking hardware can be tricky because unlike an Arduino or ARM development board the device has been built from the ground up to serve a specific purpose.

1. Read a little about hacking Nordic wearables
	* [Hackster.io tutorial on hacking an nRF51822 based ID107](https://www.hackster.io/smarty-the-team/smarty-the-watch-arduino-smartwatch-b9f7c4)
	* [Goran's tutorial on hacking the ID107](http://www.lemilica.com/smarty-the-watch-it-is-aliveeee/)
	* [Roger's blog post about the ID107 Plus w/ my microscope pics](http://www.rogerclark.net/new-nrf52832-based-smart-watch-available/)
2. Install Arduino IDE 
	* [Be sure to install version 1.6.13 of the Arduino IDE for Nordic compatibility](https://www.arduino.cc/en/Main/OldSoftwareReleases)
	* [Getting started with Arduino](https://www.arduino.cc/en/Guide/HomePage)
3. Install Sandeep's Arduino Core for the nRF52832
	* [Sandeep's Arduino Core for Nordic Semiconductor nRF5 based boards](https://github.com/sandeepmistry/arduino-nRF5)
4. Install 'Hello World' sample code (using provided J-Link programmer) and experiment with various ways of coding the wearable. You will need to install the provided "SoftDevice" (think of it as the connection between your application and the bootloader) before installing your application
	* [For Windows use nRFgo Studio](https://devzone.nordicsemi.com/blogs/840/nrfjprog-pynrfjprog-intro-mac-os-x-linux-now-suppo/)
	* [For Linux and Mac use nrfjprog](https://www.nordicsemi.com/eng/Products/2.4GHz-RF/nRFgo-Studio)
	* [nrfjprog in Python if you are so inclined](https://github.com/NordicSemiconductor/nRF5-universal-prog)
5. Use Nordic's nRF Connect diagnostic/development app to see what you are sending over Bluetooth
	* [nRF Connect on Google Playstore](https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp)
6. Send accelerometer data over Bluetooth using a GATT notification


## [](#mobile-app)**Mobile App with MLP Neural Network** 
![](https://curtpw.github.io/cri/images/neurophone.jpg)

You will create a mobile app using the Evothings prototyping tool for Apache Cordova. Cordova is a "hybrid" JavaScript development platform for building Android and iOS apps. This means that instead of writing Java for Android and Objective C for iOS you write a single body of code in JavaScript which Cordova converts into Java and Objective C. Evothings will allow you to run your Cordova code in the Evothings prototyping app. This means you can run simple JavaScript on you laptop as a mobile app on your phone with native access to hardware!! You will need to connect to one of our wearable devices using Bluetooth and then pull data from the device using a GATT Notification Characteristic. You can use the Evothings console tool to monitor your app code the same way you would use the Chrome Dev Tools console during web development. Once you have your data its time to push it into a neural network. Synaptic a very easy to use framework for implementing MLP (Multi Layer Perceptron) neural nets in JavaScript. It is fairly simple compared to common data science tools but this very simplicity makes it perfect for real time data using minimal computational resources (like a phone). Substantial training can be accomplished in seconds. 
_NOTE: There should be iOS equivalents of all the Android apps I've linked_

1. Install Evothings Workbench on your laptop
	* [Evothings webpage](https://evothings.com/doc/index.html)
	* [Evothings streaming data over Bluetooth example](https://evothings.com/doc/examples/arduino-ble.html)
2. Install Evothings Viewer (the Evothings prototyping app) on your mobile device
	* [About Evothings Viewer](https://evothings.com/doc/studio/evothings-viewer.html)
	* [Evothings Viewer on Google Playstore](https://play.google.com/store/apps/details?id=com.evothings.evothingsviewer&hl=en)
3. Read abouthe Synaptic MLP (Multi Layer Perceptron) neural network framework
	* [Synaptic.js webpage](http://caza.la/synaptic/#/)
	* [Neural networks in JavaScript](https://blog.webkid.io/neural-networks-in-javascript/)
4. Download the starter project and put it in your Evothings project folder
5. Look at the starter project files. This will include the Synaptic JS and some methods for connecting to devices over Bluetooth.
6. Decide how you want to use synaptic.js, write some code and test it by using the a BLE peripheral simulator app to send test data to your neural network app running in Evothings Viewer
	* [BLE Peripheral Simulator on Google Playstore](https://play.google.com/store/apps/details?id=io.github.webbluetoothcg.bletestperipheral)
7. Get sensor data then build and train a neural network using streaming sensor data (you will want to collect and array of time series data)
8. Test your neural net on live data and see how your results differ depending on how close the current device position approximates the position the device was in during training.

Once you have meaningful output from your neural net its time to send them to our hacked plasma globe over the internet. 

## [](#raspberry-pi)**Plasma Globe with Raspberry Pi**
![](https://curtpw.github.io/cri/images/plasma.jpg)

I have soldered wires to the power switch of the Plasma Globe (yes, caps) so that the switch can be bypassed. These wires have been attached to a relay which is essentially a computer controlled switch. This relay will be attached to the GPIO (General Purpose Input Output pins). You will configure the Pi so that it can be accessed over Bluetooth and made to turn the Plasma Globe on an off. If we are trying to display a non-binary value we might make the Plasma Globe turn on an off at various speeds - low speed for a low value and high speed or even always on for a high value. You may have trouble connecting to two devices at once (the hacker wearable and the Pi Zero) in which case you will have to switch disconnect from the one device before connecting to the other.

1.	If you have not already completed the mobile app above install Evothings as instructed above. A large portion of this project section also includes mobile app development using Evothings.
2.	Take a look at the Evothings Raspberry Pi example and download the example files
	* [Evothings Raspberry Pi example](https://evothings.com/doc/examples/rpi3-system-information.html)
3.	Learn about how you can use the Raspberry Pi GPIO (General Purpose Input Output) to control external electronics. The GPIOs are the two rows of metal pins (or two rows of sockets or two rows of unsoldered holes) on the back of the Pi.
	* [About the Raspberry Pi Zero Wireless](http://www.techrepublic.com/article/raspberry-pi-zero-wireless-the-smart-persons-guide/)
	* [How to setup a Raspberry Pi Node.js Webserver and control GPIOs](https://tutorials-raspberrypi.com/setup-raspberry-pi-node-js-webserver-control-gpios/)
	* [Bleno GitHub repository (What we will use, take a look at the examples)](https://github.com/sandeepmistry/bleno)
	* [Tutorial on Bleno with Pi](http://www.raspberry-pi-geek.com/Archive/2014/08/Getting-BLE-to-behave-on-the-Pi/(offset)/2)
	* [Tutorial1: Raspberry pi, Node.js and relay](https://github.com/brentnycum/garage-node)
	* [Tutorial2: Raspberry pi, Node.js and relay](https://www.hackster.io/uisli21/home-automation-using-raspberry-pi-and-nodejs-c308b9)
3.	Learn about using Evothings with a Pi
	* [Evothings Raspberry Pi example](https://evothings.com/doc/examples/rpi3-system-information.html)
4.	Write a node.js app for the raspberry pi which can read Bluetooth BLE information ("characteristics") from your Evothings mobile app. Use the provided example or write your own starting from the Bleno Git repo examples. Use 'forever' to run your app so that it stays up ([sudo] npm install forever -g).
5.	Once you have successfully turned the Plasma Globe on and off with your Evothings Viewer mobile app, combine your Evothings app for Raspberry Pi with an Evothings App for applying streaming sensor data to neural nets

#### []()Combine all of the above and then see who light up the Plasma Globe by matching the gesture (wearable device position) trained on the app neural net.

## [](#sensors)**Sensors and Arduino**
![](https://curtpw.github.io/cri/images/toolbox.jpg)

I have prepared several bread boards mounted with Arduino Nano microcontrollers. I have also brought a wide variety of sensors, most with wearable device applications, which can easily be connected to these Arduinos. Remember to use the 3 volt power pin on the arduino, not the 5 volt! 5v will kill some of the sensors and almost all the sensors will work with 3v.

* [Getting started with Arduino Nano](https://www.arduino.cc/en/Guide/ArduinoNano)

Sensors:
1.  Pulse Sensor: analog photoplethysmograph with broken out green LED and photo receptor for heart rate and heart rate variability
	* [Sensor homepage with lots of tutorials](https://pulsesensor.com/)

2.  MAX-30101: digital photoplethysmograph for heart rate and heart rate variability
	* [Maxim product page](https://www.maximintegrated.com/en/products/analog/sensors-and-sensor-interface/MAX30101.html)
	* [Sparkfun product page for MAX30105 (works with 30101)](https://learn.sparkfun.com/tutorials/max30105-particle-and-pulse-ox-sensor-hookup-guide)
	* [Sparkfun Arduino library and example code](https://github.com/sparkfun/SparkFun_MAX3010x_Sensor_Library)

3.	MPU-9250: combined accelerometer, gyroscope and magnetometer
	* [Sparkfun product page](https://www.sparkfun.com/products/13762)

4.  MPU-6050: combined accelerometer and gyroscope
	* [Arduino product page](https://playground.arduino.cc/Main/MPU-6050)
	* [Sparkfun product page](https://www.sparkfun.com/products/11028)

5.  APDS-9960: gesture detection, RGB color and proximity 
	* [Sparkfun product page](https://www.sparkfun.com/products/12787)

6.  Analog GSR(Galvanic Skin Response)/EDA(Electrodermal Activity) Sensor 
	* [Seeed product page](http://wiki.seeed.cc/Grove-GSR_Sensor/)

# []()**CRI Project Proposals**

## [](#empathy)**Building Group Empathy with Sensors, Wearables and Biofeedback**
![](https://curtpw.github.io/cri/images/empathy.jpg)

In a society that constantly emphasizes the individual it can be difficult to step in a stranger's shoes and see things from their perspective. In this project we will step into stranger’s bodies. Several wearable devices will be built capable of exchanging data with each other over a network. Each device will sense viscerally experienced bio-signals, for example heartbeat and respiration. Each device will also be capable of providing biofeedback which mimic these bio-signals, for example haptic feedback which ebbs and flows as a breath is taken or a pulsing solenoid (linear actuator) which presses into the chest in time with a heartbeat. When a single user is not facing any other users, the biofeedback functions play back the user’s own vital signs, making them more aware of their body. When two users are facing each other, they exchange data and feel each other’s vital signs as if they had stepped into each other’s body. When a plurality of users face a single user, all users feel that focal individual's vital signs, subsuming the group into that individual. A number of wearable form factors could be suitable, the chest and head would be ideal mounting points. These devices could be used in group therapy, team building or any number of other applications.

## [](#autism-audio)**Audacious Audio for Autism and ADHD: Environmental Audio Acquisition, Processing and Delivery On a Wearable Device**
![](https://curtpw.github.io/cri/images/hat.jpg)

Auditory overstimulation and sensory processing issues are a significant problem for Autistic and ADHD individuals. In this project we will build a wearable device which can acquire and distinguish between environmental audio sources using microphone arrays and directional microphones. The device will process and filter environmental audio data using a microcontroller, Raspberry Pi or similar. Once the desired audio has been isolated it will be delivered to the user in an inconspicuous low profile fashion, for example bone conduction transducers. When combined with low-profile transparent ear plugs or over-ear noise blocking earmuffs, this device should substantially increase the quality of life for those who use it.

## [](#eye-track)**Smart Glasses for the Education and Mental Health**
![](https://curtpw.github.io/cri/images/glasses.png)

Eye movement and gaze direction can tell us an incredible amount of information about what a person is thinking and feeling. Eye activity can tell us if a student is generally inattentive and of course what they are specifically looking at. Eye movement may even be used to diagnose autism and ADHD. Despite this, it is a signal rarely if ever used in wearable devices. In this project we will build a low profile wearable eye activity and head tracker into a normal looking pair of eyeglasses. This device will be capable of measuring general levels of eye movement, rough gaze direction and angular position of the head. Because this device is low profile, simplified sensor strategies must be used instead of an eye facing camera. For example, infrared and high resolution proximity sensors to leverage the irregular color and shape of the eyeball. Low profile feedback about attentiveness or other detected behavior will be provided to the user - possibly haptic motors or strategically placed LEDs.

## [](#about-me)**About Curt**

I usually find that more is learned about a person from family and childhood than a resume. I was named after my great grandfather Isaac Perry (his last name is my middle name). He owned a clock and watch repair shop in Elizabeth City, a town on the edge of the Great Dismal Swamp in North Carolina. During the Great Depression of the 1930s his shop was shuttered and he could find no work. To provide for my family he fixed and reloaded used, badly damaged shotgun and rifle casings and traded them to hunters in exchange for food. My father grew up in his workshop and I grew up in my father's workshop. My mother is a psychiatrist who graduated medical school at 21, four years younger than most people in her class. She decided to pursue psychiatry because mental health issues plagued the majority of her family (the majority are also physicians). Her mother, my grandmother, eventually killed herself. I have worked in the mental health space the majority of my career and spent a great deal of my free time in various volunteer capacities as well. You can also [look me up on LinkedIn.](https://www.linkedin.com/in/curtwhitepro/)

## []()Just for fun, some 'wearable device' Halloween / burning man costumes from years past:

[![](http://img.youtube.com/vi/E8d0ozE11r0/0.jpg)](http://www.youtube.com/watch?v=E8d0ozE11r0)

![](https://curtpw.github.io/cri/images/plasmagloberockstar.jpg)
