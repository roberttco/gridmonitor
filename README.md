# Gridmonitor
## Overview
This is a schematic and PCB design for a four channel energy monitor.  Each channel is made up of two measurements - voltage 
and current.  The microcontroller is an ESP8266 on a Wemos D1 mini carrier.  The measurements are taken with four ADS1115 A/D
converters used in differential mode.  ESPHome code is also included.

## What could have been done better
Let's get this out of the way first.  There is no fuse protection on any of the inputs.  That would have been a goode idea.  Also the voltage measurement
is taken directly from the mains connected to the voltage inputs.  In other words, no isolation.  Also could have been done better.  Finally, powering the
ESP8266 from the input supply would have been nice instead of requiring a separate USB supply.  All this being said, a second generation of this board has
been created sans the fused inputs.  That will be in a different repository when I get to it... [as of 21-sept-2022].

# Requisite warning
## Line voltages are exposed on the back and front of this PCB - an enclosure is highly recommended!!  You have been warned.

If you shock yourself or worse, don't blame me.  You decided to build this thing and I an not responsible for how you do or don't protect yourself.

## Voltage inputs
The resistor values used in the schamatic on the voltage inputs are for measuring up to **120VAC**.  

**You must change the resistor values to suit your current transformers and voltage inputs**

### Input protection
The schematic specifies varisters be placed across the voltage input connections.  The 20D201K MOV is rated for 130V clamping so 
if you want to measure a higher (or lower) voltage, change the MOV as appropriate. You want to select a MOV with a voltage rating
slightly higher than the measured voltage.  

## Current inputs
The current inputs include a burden resistor for the current transformers.  The value specified in the schematic is for a 3000:1 100A current transformer.  
Depending on what transformer you you, you will need to add the correct burden resistor. **NEVER** connect a current transformer without a burden resistor. 
You will destroy the A/D converter. The only exception is if you use a current transformer that has a burden resitor built in.

## What you need to change
The governing factor is the maximum input voltage for the A/D converter.  The ADS1115 has a maximum input voltage of 6.144v (since they are connected to be operated in differential mode)
You will need to make these changes if you want to change the range of input currents and/or voltages.

**The voltage divider resistors** Keep the values fairly high so you do not have too much current goign through the divider and thus too much power disapation for the resistors.  The 
schematic describes a voltage divider that has an "output" voltage of 3.725v at 120v "input"
	
`120V / 1063K = 113uA * 33K = 3.72V`
	
Note: The value of the resistor across the differential inputs should be significantly smaller than the 22M ohm input inpedance.

**The current transformer burden resistors** The burden resistor should likewise be chosen to keep the input to the A/D converter below 6.144v.  Choose a current transformer that is rated
for the load you are going to measure.  For example [only] if you have a 240v split phase 200A service at your home (i.e. the main breaker is rated for 200A) then you should use a current
transformer that could handle the full 100A per phase plus some headroom.  A 150A current transformer would suffice.  Then, using the current ratio of the transformer, you sould choose a resistor 
that would provide you a maximum value of 6.144v minus some headroom (such as 5v maximum).

Assuming a 1000:1 current transformer and 100A flowing through the conductor:

`100A / 1000 = 0.1A * R = 5v.  R = 50 ohms`

**Input protection**
The inputs are protected with metal oxide varisters - or voltage controlled resistors.  As the voltage increases, the resistance goes down.  If too much voltage is applied, the MOVs behive like a
short circuit.  You should choose MOVs that suit your input voltages.  Incidentally these are the saem devices used in "surge supressors" that you may find.  More information for selectiong one
can be found in the resource links below.

# [GitHub](https://github.com/roberttco/gridmonitor) Folders
### EasyEDA
The schematic and PCB were designed using the EasyEDA standard edition software. (see link below).

### ESPHome
This intent is to use this with Home Asssistant and the YAML code for the project is in the ESPHome folder.  The code cannot be 
used as is.  There are a few changes you need to make like addingyor SSID and SSID password as well as the HomeAssistant API encryption key.

### gerber
The PCB gerber files are in this folder and describe a 100mm x 100mm PCB - the maximum size PCB from JCL PCB that does not incurr additional fees.


# References
Here are some useful references to help you.

* [Voltage divider calculator](https://ohmslawcalculator.com/voltage-divider-calculator)
* [ADS1115 Datasheet](https://www.ti.com/product/ADS1115)
* [EasyEDA](https://easyeda.com/page/download)
* [MOVs](https://components101.com/articles/metal-oxide-varistor-mov-overview#:~:text=1%20The%20first%20step%20of%20choosing%20a%20MOV,in%20case%20of%20a%20surge.%20...%20More%20items)
* [JLC PCB](https://jlcpcb.com/)

