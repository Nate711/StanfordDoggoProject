![hero](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/hero.jpg)

# End-of-life notice
Thank you everyone for your interest and support over the last 6 years for this project! 

We are hard at work building a new robot, Pupper v3, and so would like to stop supporting this project. Thanks for your understanding! Pupper v3 is fully open source and build instructions will be released in the coming months. You can find preliminary information here https://pupper-v3-documentation.readthedocs.io/en/latest/index.html 

![20240701_232332](https://github.com/stanfordroboticsclub/StanfordQuadruped/assets/1295426/96d09d2b-9d99-4a0b-b30b-6e317d7b286b)

![20240701_231506](https://github.com/stanfordroboticsclub/StanfordQuadruped/assets/1295426/d9875ccf-be3f-496c-a22b-aaab4f5fc9fd)

![IMG_2942](https://github.com/stanfordroboticsclub/StanfordQuadruped/assets/1295426/c6f1de38-a013-402b-a1e2-f924573ec48e)

Quick specs for Pupper v3
* Powerful 400W GIM4305 brushless motors
* Raspberry Pi 5
* Reinforcement learning locomotion policy out-of-the-box
* Luxonis SR depth camera
* LCD screen for debugging and facial expressions
* Roughly $1000 BOM


# The Stanford Doggo Project
## Overview Of Stanford Doggo
Stanford Doggo is a highly agile robot designed to be an accessible platform for legged robot research. The robot currently holds the record (among all robots) for the highest vertical jumping agility<sup>1</sup> and can jump twice as high as any existing quadruped robot! Weighing in at a little less than 5kg, Stanford Doggo is easy and safe to develop on, but at the same time, don't expect Stanford Doggo to carry heavy loads or climb super aggressive terrain. If you use a portion of this project or want further technical details, please cite our paper presented at ICRA 2019: https://ieeexplore.ieee.org/document/8794436 (freely available on arxiv: https://arxiv.org/abs/1905.04254). The project is generously supported by Stanford Student Robotics http://roboticsclub.stanford.edu/.

<sup>1</sup>[Vertical jumping agility] = [maximum vertical jump height] / [time from onset of actuation to apogee of jump]

## Building Doggo
We hope you build your own Stanford Doggo! In the Hardware folder of this repository we've linked the Fusion 360 CAD model and it includes all the parts you'll need to source. Many of the custom pieces are either 3d printed or waterjet (instead of manually milled for instance), which means you will only have to do post-processing work. For example, the primary links on each waterjet leg assembly require you to drill and tap a hole for a set screw. If you need help, please reference the CAD, submit an issue to this github repo, or email the owner, nathan kau [at] stanford [dot edu].

You can find a work-in-progress bill of materials here: https://docs.google.com/spreadsheets/d/1MQRoZCfsMdJhHQ-ht6YvhzNvye6xDXO8vhWQql2HtlI/edit#gid=726381752. Please don't hesitate to ask for help!

## Doggo Software
The brains of Stanford Doggo are split between the ODrive motor controllers and the central Teensy microcontroller. To run Doggo, you'll need to flash the our custom ODrive firmware onto the four motor controllers in the robot and then configure them using the doggo_setup.py script included in that repository. Quick note, if you have a different mechanical design than Doggo, make sure to update the gear_ratio parameter in the code or via odrivetool. After uploading the firmware and configuring, you'll next want to upload the Doggo Arduino code to the central microcontroller. This code is responsible for switching between different states and sending the right position commands to the robot. When you power on the robot, the four legs will first do a calibration routine so that the motors and encoders become synced up, and then the robot will enter an idle mode. Once in idle, you can send serial commands over the wireless xbee network to command Doggo to trot, jump, etc. Please reference the Doggo software repo for more information.

## Help
We encourage you to submit issues to this github, or email the owner, nathan kau [at] stanford [dot edu]. 

# A blog post about Doggo
Hi all, I thought I'd share more about the Stanford Doggo Project, which you might have seen in Oskar's New Year's update! We're a group of undergrad and grad students in Stanford Student Robotics and have been working on legged robots for the last year and a half. Our latest robot, Stanford Doggo, is a shoebox-sized quadruped robot that can walk, trot, pronk, and jump around.

I think this video gives the best overview of what Doggo is:

https://www.youtube.com/watch?v=cJxotk4lR90

And my favorite video, Doggo doing a backflip:

https://www.youtube.com/watch?v=aZylPK7SbV0

I&rsquo;ve been seeing a ton of amazing projects here on the forum and on the ODrive Discord channel, so I wanted to make a blog post explaining how Doggo works. I hope people might be able to learn something from this post, and perhaps even build their own Doggo and improve upon it. The whole project is open-source (links below) with CAD, code, and firmware available on Github. The robot code runs on a Teensy 3.5, and we use ODrives for motor control so I imagine a lot of people here could jump right in. We've also tried to make the robot inexpensive to build in your own lab, school, or home, and we absolutely welcome people to contribute to the project. 

## Relevant links:
GitHub project repository: https://github.com/Nate711/StanfordDoggoProject
Full, downloadable Fusion 360 CAD: https://a360.co/2OBxTbH
Teensy code: https://github.com/Nate711/Doggo
ODrive fork: https://github.com/Nate711/ODrive

# Mechanical Design

## Coaxial mechanism
The coaxial mechanism that drives each leg is definitely the most complex mechanical component of the robot. It has also been the most troublesome. The way it works is that we have two TMotor MN5212 motors mounted on the carbon fiber side panel. We also have a 3D printed bearing block that has two bearings to hold the outer coaxial tube. (Refer to the cutaway CAD view below). The two motors transfer power to the coaxial shafts via 6mm wide, 3mm pitch GT2 belts between a 16T pulley and a 48T pulley. We didn&rsquo;t have room in our mass budget for regular, off-the-shelf pulleys, so we printed our own using the Xometry SLS service. As a side note, we learned to always specify to the service that the pulleys must be printed up. If the parts are printed at an angle, the geometry of the pulley teeth gets distorted because of the off-angle layers. Above the pulleys we have a waterjet aluminum bracket to maintain belt tension and thereby prevent skipping during high-torque situations. That said, it was a real pain to find the best center-to-center distance for the bracket because the slop in the connection between the motors and small pulleys, and the slop in the connection between the larger pulleys and the shafts meant that the center-to-center distance for the top bracket had to be 0.5mm larger than the nominal center-to-center distance prescribed by the belt supplier (SDP-SI). The biggest problem with this assembly was that the higher the belt tension, the more friction we had in the assembly. Higher friction means worse tracking performance for the motors, and also worse sensitivity to touch-down events and the like. On our next robot, we&rsquo;re hoping to have smoother, more precisely machined pulleys, and less slop in the coaxial assembly.

#### CAD diagram
![hero](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/diagram.jpeg)

#### IRL
![diagram](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/coax.jpeg)

#### In operation
https://www.youtube.com/watch?v=6PL3aur4g4c

## Legs

Doggo has four, 2DOF legs of the SCARA flavor. By SCARA flavor I mean that each leg is a five bar linkage and the two upper links are driven co-axially. The actual leg links were waterjet cut by Big Blue Saw, which is a great online service (although make sure to upload all your parts in one DXF to save money). The waterjet parts were actually precise enough that we did not need to ream the holes for the bearings.

### Joints
For each joint, there are two deep groove ball bearings stacked next to each other in on link, and a shoulder bolt goes through them and threads into the opposing link.

![|](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/joint.png)

### Feet
The robot feet are silicone pieces that we made using a 3D printed, 2-part mold.

![|](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/foot.jpeg)

## Frame

The frame of the robot is thankfully very simple. We have two waterjet, 4mm carbon fiber panels on each side, connected by two 1/32&rdquo; 5052 aluminum sheet metal parts. These sheet metal parts were cut using a waterjet, and then folded up by hand (long story, but because the two carbon fiber panels are canted inwards, the tabs on the aluminum part couldn&rsquo;t be folded on a brake).

![|](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/frame.jpeg)

# Electronics
Doggo has four v3.5, 48V ODrives, two for each leg, mounted on the carbon fiber side panels. Sitting on a 2mm carbon fiber plate in the middle, we have a Teensy 3.5, a Sparkfun BNO080 IMU, and a 5mW Xbee. The Teensy talks to the ODrives over four separate UART lines, each operating at 500,000 baud. Underneath this plate, we have the power distribution board (a janky quadcopter PDB we found on Amazon), and a fancy Gigavac P105 Mini-Tactor relay so we can kill the robot power using an offboard ESTOP switch. We also put our two, 1000mah 6s Tattu lipo batteries down there.

Last, but not least, each motor has a AS5047P encoder to track the motor angle. We actually are only using the incremental interface, because at the time we built the robot, there was no absolute encoder support on the ODrive and we couldn&rsquo;t make the index pin functionality work either.

#### Electronics schematic
![|](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/wiring.png)

#### Layout of ODrives
![|394x526](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/sides.jpeg)

#### Top side of the middle electronics plate
![|](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/electronics.jpeg)

#### The belly of the robot: Relay (translucent piece in the middle), PDB (golden board in front of the relay), and batteries (close and far).
![|](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/belly.jpeg)

# Software

## Overview

The Doggo software is relatively simple as far as things go. The gist of it is that we have a state machine that flips between different behaviors (like trot, jump etc), and for each behavior we send different position commands and gains to the four ODrives. We also have some helper threads running, like one to take IMU measurements, another to record telemetry from the ODrives, another to take commands over Xbee, etc.

## Leg trajectories

The robot walks, trots, bounds, and pronks by commanding different sinusoidal open-loop trajectories to the four ODrives. The leg trajectories are composed of two halves of sinusoidal curves for the flight and stance phases shown in orange and purple in the picture. The geometric parameters of the sinusoids, the virtual leg compliance, and the duration of time that the leg spends traversing each sinusoidal segment, were varied to create different gaits.

![|265x299](https://github.com/Nate711/StanfordDoggoProject/blob/master/images/trajectory.png)

At any given time, the Teensy computes the desired foot locations in cartesian coordinates, and then converts them to leg angles (θ) and leg separations (γ). These two numbers describe the virtual leg that originates at the hip joint of the leg and terminates at the foot.

These virtual leg parameters (theta and gamma) and their corresponding virtual stiffness and damping coefficients are sent from the Teensy to the four ODrives at the 100Hz refresh rate. The ODrives then run a custom PD controller to generate torques in theta-gamma space. The ODrives then use the [Jacobian](http://robots.iit.edu/uploads/2/5/7/1/25715664/mmae_540_-_lecture_2_-_manipulator_kinematics.pdf) of the leg to transform torques in theta-gamma space into torques in the motor0-motor1 space.

## ODrive Control
We implemented a custom binary UART protocol to send and receive data. The binary protocol is significantly faster than the ASCII protocol, which (I think) was the only protocol implemented for the Arduino when we built the robot. If you'd like more of the specifics, visit https://github.com/Nate711/Doggo/blob/master/lib/ODriveArduino/ODriveArduino.cpp

**I think that about wraps everything up! Let me know if you have questions, and I&rsquo;ll also try to update the post if people are interested in more details.**

# FAQ
## The sub-folders are empty!
Run this to populate the folders.
```shell
git submodule update --init --recursive --remote
```
## How do I configure the ODrive parameters for Doggo?
We use the script ```https://github.com/Nate711/ODrive/blob/master/tools/doggo_setup.py```
## How are the legs numbered?
Leg0 is the front left, leg1 is the back left, leg2 is the back right, and leg3 is the front right.
## How do I calibrate the legs?
This is a sore spot for the robot right now. When you power on the robot, all the driven linkages (ie top links) need to be as horizontal as possible. If everything is set up correctly, the motors will then begin their calibration routine which involves them rotating about 120 degrees to one side and then back. After this, the robot is ready.
## Can it turn?
Yes and no. It turns very slowly with the 'Y' command. The turning speed is set by 's [desired step difference]' where the step difference should be around -0.1 to 0.1 at the most.
## Which way should the IMU point?
There are little markings on the BNO080 board which indicate which way x is positive. Align that direction with the forward direction of the robot. The forward direction is towards the motors connected to ODrives 0 and 3. 
## How are the ODrives connected to the Teensy?
We use serial connections between the Teensy and ODrives so for each ODrive you'll need to connect Teensy RX to ODrive TX and Teensy TX to ODrive RX. Since there are four ODrives, you'll have to connect up four sets of these serial connections!

In code we have these definitions which may help with wiring:
```cpp
HardwareSerial& odrv0Serial = Serial1;
HardwareSerial& odrv1Serial = Serial2;
HardwareSerial& odrv2Serial = Serial3;
HardwareSerial& odrv3Serial = Serial4;
```

Here's also a little chart made by HelloPlanet!
```
Teensy3.5 --- Logical Function --- Component
P0 - RX1 - ODrive1 (odrv0)
P1 - TX1 - ODrive1 (odrv0)

P7 - RX3 - ODrive3 (odrv2)
P8 - TX3 - ODrive3 (odrv2)

P9 - RX2 - ODrive2 (odrv1)
P10 - TX2 - ODrive2 (odrv1)

P31 - RX4 - ODrive4 (odrv3)
P32 - TX4 - ODrive4 (odrv3)
```
## How is the Xbee wired?
We connect it via serial to Serial5. We also have a definition in ```config.h``` called ```USE_XBEE``` that determines whether the code should use the actual USB port on the Teensy or the Xbee for communications. 
## How is the IMU wired?
We connect it via SPI with the following defines.
```cpp
//Pins for BNO080 IMU
#define SPI_CS_PIN 15
#define SPI_WAK_PIN 14
#define SPI_INTPIN 17
#define SPI_RSTPIN 16
```
## How does the relay get wired up?
We now use a solid-state relay https://www.digikey.com/product-detail/en/sensata-crydom/D06D100/CC1520-ND/353618 with the output terminals in series with the main power and the input terminals connected to an external battery with a switch. We have the switch wired up in serial so that pressing the switch will turn on/off the relay and thus the robot's main power.
## The CAD doesn't download correctly
This is unfortunately not a problem on our end but on Fusion's. Fusion customer service has in the past been able to fix corrupted uploads on their server.
