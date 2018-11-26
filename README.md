# The Stanford Doggo Project
## Overview Of Stanford Doggo
Stanford Doggo is a highly agile robot designed to provide an accessible platform for legged robot research. Currently, the robot holds the record (among all robots) for greatest vertical jumping agility<sup>1</sup>. Stanford Doggo can also jump twice as high as any existing quadruped robot. Weighing in at a little less than 5kg, Stanford Doggo is easy and safe to develop on, but at the same time, Stanford Doggo should not be expected to carry heavy loads or climb extremely aggressive terrain. The project is supported by Stanford Student Robotics http://roboticsclub.stanford.edu/.

<sup>1</sup>[Vertical jumping agility] = [maximum vertical jump height] / [time from onset of actuation to apogee of jump]

## Building Doggo
We want you to be able to build your own Stanford Doggo without a hassle. To this end, we've uploaded the entire CAD model under the Hardware folder. The design was completed in Fusion 360 and includes all the mechanical parts you'll need to source. Many of the custom pieces are either 3d printed or waterjet, which means you will only have to do post-processing work. For example, the primary links on each leg assembly (which are waterjet) require you to drill a hole for a set screw and then tap it. For now, if you need help, please reference the CAD or submit an issue to this github repo. You can find a WIP BOM here: https://docs.google.com/spreadsheets/d/1MQRoZCfsMdJhHQ-ht6YvhzNvye6xDXO8vhWQql2HtlI/edit#gid=726381752. We understand that at this moment, it may be quite frustrating to build Doggo yourself. Part of the reason is that we're working on a bigger and better version of Doggo that may make this version obsolete. However, we will continue to support this version Stanford Doggo and will continue to upload resources to make this project more accessible. Please do not hesitate to ask for individual help!

## Doggo Software
The brains of Stanford Doggo are split between the ODrive motor controllers and the central Teensy microcontroller. To run Doggo, you'll need to flash the ODrive firmware onto the four motor controllers in the robot and then configure them. You'll then want to upload the Doggo code to the central microcontroller. When you power on the robot, the four legs will first do a calibration routine, and then the robot will enter an idle mode. Once in idle, you can send serial commands over the wireless xbee network to command Doggo to trot, jump, etc. Please reference the Doggo software repo for more information.

## Help
We encourage you to submit issues to this github, or email the owner, nathan kau [at] stanford [dot edu]. 
