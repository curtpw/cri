---
layout: default
---

Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](another-page).

There should be whitespace between paragraphs.

# []()Master Class Project: Neuro Plasma Hacker

## [](#master)Wearable Devices, Neural Network Mobile Apps, Controlling IoT 

Your goal is to **hack** an off the shelf **wearable device, send accelerometer data** from the hacked device **to a mobile app** which we will create, build and train a **neural network** in the mobile app to detect a specific set of wearable device data, and use the sensor data detection results **to control a modified plasma globe** connected to a Raspberry Pi over the internet. I also have a number of Arduino microcontrollers and a wide array of sensors (Heart Rate, gesture, proximity, accelerometer, gyrescope, GSR/EDA, pressure, stretch) for you to explore if you want something simple.

### []()Wearable Device

You will be hacking a fitbit clone containing a Nordic nRF52832 SoC (System On a Chip) with a 64Mhz ARM microprocesor. This Device contains a Kionics KX022 Accelerometer and a Bluetooth 4 BLE tranciever. You can write code for the device using the Arduino IDE with Sandeep's Arduino Core for Nordic chips. I use a Segger JLink to program these devices but and SWD programmer will work. Hacking hardware can be tricky because unlike an Arduino or ARM development board the device has been built from the ground up to serve a specific purpose.

1. Read a little about hacking Nordic wearables
2. Install Arduino IDE
3. Install Sandeep's Arduino Core for the nRF52832
4. Install 'Hello World' sample code and experiment with variouse ways of coding the wearable
5. Send accelerometer data over Bluetooth using a GATT notification


### []()Mobile App

You will create a mobile app using the Evothings protoyping tool for Apache Cordova. Cordova is a "hybrid" JavaScript development platform for building Android and iOS apps. This means that instead of writing Java for Android and Objective C for iOS you write a single body of code in JavaScript which Cordova converts into Java and Objective C. Evothings will allow you to run your Cordova code in the Evothings prototpyping app. This means you can run simple JavaScript on you laptop as a mobile app on your phone with native access to hardware!! You will need to connect to one of our wearable devices using Bluetooth and then pull data from the device using a GATT Notification Characteristic. You can use the Evothings console tool to monitor your app code the same way you would use the Chrome Dev Tools console during web development. Once you have your data its time to push it into a neural network. Synaptic a very easy to use framework for implementing MLP (Multi Layer Perceptron) neural nets in JavaScript. It is fairly simple compared to common data science tools but this very simplicity makes it perfect for real time data using minimal compuational resources (like a phone). Substantial training can be accomplished in seconds. 

1. Install Evothings on your laptop
2. Install the Evothings prototyping app on your mobile device
3. Read abouthe Synaptic MLP (Multi Layer Perceptron) neural network framework
4. Download the starter project and put it in your Evothings project folder
5. Look at the starter project files. This will include the Synaptic JS and some methods for connecting to devices over Bluetooth.
6. Get sensor data then build and train a neural network using streaming sensor data (you will want to collect and array of time series data)
7. Test your neural net on live data and see how your results differ depending on how close the current device position approximates the position the device was in during traiing.
8. Once you have results, its time to send them to our hacked plasma globe over the internet. We will be using a tool called Node-RED to connect our mobile app the the Raspberry Pi Zero Wireless over the internet.
9. Before you can install Node-RED you will need to install Node.js on your laptop
8. Install Node-RED, run the Node-RED application and open LOCAL HOST in a browser to view the Node-RED user interface

### []()Plasma Globe Raspberry Pi

I have soldered wires to the power switch of the Plasma Globe (yes, caps) so that the switch can be bypassed. These wires have been attached to a relay which is essentially a computer controlled switch. This relay will be attached to the GPIO (General Purpose Input Output pins). You will configure the Pi so that it can be accessed over the internet and made to turn the Plasma Globe on an off. If we are trying do display a non-binary value we might make the Plasma Globe turn on an off at variouse speeds - low speed for a low value and high speed or even always on for a high value. 

# []()CRI Project Proposals

## [](#empathy)Building Group Empathy with Sensors, Wearables and Biofeedback

In a society that constantly emphasizes the individual it can be difficult to step in a stranger's shoes and see things from their perspective. In this project we will step into stranger’s bodies. Several wearable devices will be built capable of exchanging data with each other over a network. Each device will sense viscerally experienced bio-signals, for example heartbeat and respiration. Each device will also be capable of providing biofeedback which mimic these bio-signals, for example haptic feedback which ebbs and flows as a breath is taken or a pulsing solenoid (linear actuator) which presses into the chest in time with a heart beat. When a single user is not facing any other users, the biofeedback functions play back the user’s own vital signs, making them more aware of their body. When two users are facing each other, they exchange data and feel each other’s vital signs as if they had stepped into each other’s body. When a plurality of users face a single user, all users feel that focal individual's vital signs, subsuming the group into that individual. A number of wearable form factors could be suitable, the chest and head would be ideal mounting points. These devices could be used in group therapy, team building or any number of other applications.

## [](#autism-audio)Audacious Audio for Autism and ADHD: Environmental Audio Acquisition, Processing and Delivery On a Wearable Device

Auditory overstimulation and sensory processing issues are a significant problem for Autistic and ADHD individuals. In this project we will build a wearable device which can acquire and distinguish between environmental audio sources using microphone arrays and directional microphones. The device will process and filter environmental audio data using a microcontroller, Raspberry Pi or similar. Once the desired audio has been isolated it will be delivered to the user in an inconspicuous low profile fashion, for example bone conduction transducers. When combined with low-profile transparent ear plugs or over-ear noise blocking earmuffs, this device should substantially increase the quality of life for those who use it.

## [](#eye-track)Smart Glasses for the Education and Mental Health

Eye movement and gaze direction can tell us an incredible amount of information about what a person is thinking and feeling. Eye activity can tell us if a student is generally inattentive and of course what they are specifically looking at. Eye movement may even be used to diagnose autism and ADHD. Despite this, it is a signal rarely if ever used in wearable devices. In this project we will build a low profile wearable eye activity and head tracker into a normal looking pair of eyeglasses. This device will be capable of measuring general levels of eye movement, rough gaze direction and angular position of the head. Because this device is low profile, simplified sensor strategies must be used instead of an eye facing camera. For example, infrared and high resolution proximity sensors to leverage the irregular color and shape of the eyeball. Low profile feedback about attentiveness or other detected behavior will be provided to the user - possibly haptic motors or strategically placed LEDs.



## [](#header-2)Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### [](#header-3)Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### [](#header-4)Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### [](#header-5)Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### [](#header-6)Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![](https://assets-cdn.github.com/images/icons/emoji/octocat.png)

### Large image

![](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
