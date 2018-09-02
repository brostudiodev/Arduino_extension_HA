# Arduino extension (more than one Arduino board - Custom components

This extension is the exact copy of hassio's arduino.py component. Without extension you can connect only one Arduino board. 
Using this component you are able to connect up to 4 Arduinos (by USB cable) in Raspberry Pi (Rpi has 4 USB ports)

follow Home Assistant's guide for Arduino: https://www.home-assistant.io/components/arduino/ 

<b>Installation:</b>

Instal the Samba share addon in Hassio (to see the config directory in your comuter (where your configuration.yaml file lives) on your PI. 
Go to config directory. Open custom_components folder (this folder isn’t there by default, so for the first time you have to create it -? right click > new folder on a PC and name it custom_components).

Copy all files in custom_components. The directory structure will be CONFIG>CUSTOM_COMPONENTS>

<b>Connection check</b>

To check USB connection please refer to Home Assistant's guide for Arduino. The best way is to connect by SSH eg. by Putty and type
dmesg. Then copy all into Notepad++ or any other notepad and find /dev/ttyACM or /dev/ttyUSB. Then check what number has each Arduino (eg /dev/ttyACM0 , /dev/ttyACM1)

<b>configuration.yaml:</b>

# Example configuration.yaml entry START

arduino2:
  port: /dev/ttyACM0
arduino3:
  port: /dev/ttyACM1
  
switch:
 - platform: arduino2
    pins:
      11:
        name: Arduino2 PIN11
      12:
        name: Arduino2 PIN12
        initial: true
        negate: true
      13:
        name: Arduino2 PIN13 - Led
  - platform: arduino3
    pins:
      11:
        name: Arduino3 PIN11
      12:
        name: Arduino3 PIN12
        initial: true
        negate: true
      13:
        name: Arduino3 PIN13 - Led

sensor:
  platform: arduino2
  pins:
    1:
      name: Door switch
    0:
      name: Brightness
      
  platform: arduino3
  pins:
    1:
      name: Door switch
    0:
      name: Brightness
 
# - END 

Hope this helps.
