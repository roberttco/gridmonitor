# Gridmonitor
## Overview
This is a schematic and PCB design for a four channel energy monitor.  Each channel is made up of two measurements - voltage 
and current.  The microcontroller is an ESP8266 on a Wemos D1 mini carrier.  The measurements are taken with four ADS1115 A/D
converters used in differential mode.  ESPHome code is also included.

## Folders
### EasyEDA
The schematic and PCB were designed using the EasyEDA standard edition software available [here](https://easyeda.com/page/download).

### ESPHome
This intent is to use this with Home Asssistant and the YAML code for the project is in the ESPHome folder.  The code cannot be 
used as is.  There are a few changes you need to make like addingyor SSID and SSID password as well as the HomeAssistant API encryption key.

### gerber
The PCB gerber files are in this folder and describe a 100mm x 100mm PCB - the maximum size PCB from JCL PCB that does not incurr additional fees.


