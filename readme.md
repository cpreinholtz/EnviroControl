# Overview - Enviro Control
This repo contains PCB designs and Arduino firmware for controlling lights and fans via PWM.

Driecotry structure:

cad
doc
firmware
hardware
production
simulation


**PCBs (see detailed descriptions below)**
* SmartPwm_v1, **obsolete**, was an attempt to put multiple pwm outputs onto a esp32 based board.
* HANA, **H**abitation **A**mbiance **N**ano based **A**utomation

## HANA Hardware

### Hardare Overview
The goal of the HANA board is to be a modular PWM controller for either leds or DC fans.  With the latest Arduino nano 33 BLE IOT/SENSE boards it should be possible to cheaply and easily create a wirless notwork of these modules, controllable via an app or master control box.  Additionally the BLE SENSE has fun things like temperature and light sensors which allow for fun closed loop control systems.  The goals are to be relativley cheap, low SWAP, modular, and easily deployable into a 12-14.4v van electrical system.


### Hardare Features
tbd

### Hardware Installation
* Battery GND
* Load -
* Load +
* Battery +

### Hardware Future Considerations
* **User Interface**
* PEC11R / 12R rotary encoder with switch for local control.
* Leds for local display / user interface.
* On off switch for complete power shutoff?, maybe just handle this with a sleep mode at button press?
* Overide switch (2 throw, 1 pole) to connect load return direct to gnd and disconnect from fet, eliminating voltage loss from Vds.



* **Electrical Design Considerations**
* backwards compatability. would it be possible to use old nano, new nano BLE, BLE SENSE, BLE IOT? probably not without a 5v regulator.
* 5v reg, probably only needed if backward compatability is needed because i think the new nanos handle 12v
* Over current shutoff? how to detect a fault on the load lines?
* Input voltage sense. volt div or otherwise for a low voltage cutoff to be enabled for battery protection.
* Do I need a heatsink if I am using a fet driver? perhaps I should add the abilty to install one just in case.
* vertical, or horizintal, or barrel Fets.  Barrel is not enough for the fan, but perhaps LEDS it would work... Horizontal might make sense if only one fet is needed per board. vertical makes sense if mutiple and we can manage heat.

* **Mechanical Design Considerations**
* Easy spaced mounting holes and encoder location for use with CNCed, 3d printed, or lazer cut cases
* long shaft encoder for use with a case.
* User freindly Silk screen for easy install.



* **External Connections**
* really only need 4 wired external connections, battery+-, Load+-, although if using n channel fets the load and battery share the + side, (load return is not the same as gnd with N channel fets!).  consider if you want to use ring terminals, screw down clamps, or some other method (solder, spring based, etc).
* daisy chain? I.E. an extra 12v and gnd connector.
* LORA. Add ability to connect or transmit to a LORA module to enable a temperature alarm.
* perhaps add ability to connect to lcd display, fastleds (they now make a truly 12v version), etc.


## HANA Firmware

### Firware Overview
The firware uses Arduino Version 1.8.13.  Firmware is currently a work in progress, I.E. not yet started.

### Firmware Future Considerations
* pwm frequency modifiers for bringing the fan control out of audible ranges.
* Sleep timers for auto shut off at bed time.
* closed loop bang bang contol system for fans. make sure to add hysteresis to avoid oddities.
* logging of temperatures and pwm settings every N minutes.
* dumping of pwm settings and or temp etc every n minutes, or upon request.
* low voltage shutoff.
* temperature allarm, either dump to BLE and or or use LORA module to get a warning to the user

