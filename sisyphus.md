---
layout: page
title: "sisyphus"
permalink: /sisyphus/
---
# Documenting the creation of a new project going by the name sisyphus 
Sisyphus is a basic robot that is to be used a platform to test the capabilities of the BBB protocol.
Sisyphus includes a raspberry pi zero which acts as the central processing unit and a raspberry pico which controls all the hardware.
Communication is done between the Rasspberry pi and the raspberry pico using the SPI protocol.

All of the hardware on sisyphus however, is not controlled by the raspberry pico. Sisyphus has a pi camera which is directly connected to the raspberry pi.
The camera however is mounted on top of a servo system , giving it motion on two axes.

The author intends to use multi view geometry algorithms to extract spatial information from images.

### Current state of the project
 - The robot has the hardware required for the camera ready and a little LCD screen that acts as a debug GUI.
 - SPI communication (albeit with a few hitches along the way) has been succesfully established between the pico and the pi.
 - The next goal of the project is to get myself bold enough to get PWM working properly.
 
