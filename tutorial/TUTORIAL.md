# Tutorial
This is a general guide on how to discover your Tuya device config.
**Do this at your own risk**

If this saved you some time. Maybe think about [giving me a tip](https://ko-fi.com/chrisburrow1739)

<img src="/kofi_qrcode.png" href="https://ko-fi.com/chrisburrow1739" alt="Give me a tip" width="200"/>

## Project Used 
- tuya-cloudcutter: https://github.com/tuya-cloudcutter/tuya-cloudcutter
- OpenBeken - https://github.com/openshwprojects/OpenBK7231T_App
- Home Assistant -  https://www.home-assistant.io/
- ESPHome - https://esphome.io/
- Itchiptool - https://github.com/libretiny-eu/ltchiptool

## Hardware Used
- Hardware: Raspberry Pi 4 (https://github.com/tuya-cloudcutter/tuya-cloudcutter/blob/main/HOST_SPECIFIC_INSTRUCTIONS.md)
- OS: Raspberry OS
- Docker Installed
- Do not connect Pi to network via wifi. Use Ethernet to keep Wifi free for the process

---

## Process - Do this at your own risk
**Smartlife**

<img src="https://github.com/chris173972/my-tuya-devices-conversion/blob/main/tutorial/tutorial_smartlife_version.jpg?raw=true" alt="SmartLife Version" width="300"/>

- Add your device to SmartLife to get your firmware version. This will be used to find out which version of OpenBeken you will need to hack the device. 
- I use OpenBeken as it find it much easier to flash with this first and discover the config through it other than using other tools and guessing (email me if you have a easier way)
 
**Terminal**:
- Make sure you know this process is only one way, so once done, this will no longer communicate with Tuya
- git clone https://github.com/tuya-cloudcutter/tuya-cloudcutter
- cd tuya-cloudcutter
- sudo ./tuya-cloudcutter.sh
- Select: 2 - Flash 3rd Party Firmware
- Find a firmware closest to your firmware version you found. Don't worry, you can usually flash again if it didn't work. 
- Put device into AP mode: press hold button untill fast flash, press and hold again till slow flash
- Will show the device is connected on termainal
- Unplug the device and plug back in.
- Put device into AP mode again: press hold button untill fast flash, press and hold again till slow flash
- Please be patient. May take a while based upon machine used
- Will show device mac address if success.

**Download Tuya Config**

<img src="https://github.com/chris173972/my-tuya-devices-conversion/blob/main/tutorial/OpenBK_Flash.png?raw=true" alt="Get Tuya Config" width="300"/>

- Use a wifi device and search wifi
- Connect to the wifi hotspot provided by the device, usually starts OpenBK...
- Once connected, navigate to http://192.168.4.1
- Navigate to 'Config' -> 'Configure Wifi & Web'
- Add your wifi details, click submit and wait for it to connect.
- Go to your wifi router look for the new IP address of your device.
- Navigate to 'Launch Web Application'
- Navigate to 'Flash' and download 'Download Tuya GPIO Config'
- Generally a good idea to also download 'Download full 2mb dump' but it can take a long time. 

---

### To use OpenBeken Firmware

**Decompiling OpenBeken Config using Itchiptool**

<img src="https://github.com/chris173972/my-tuya-devices-conversion/blob/main/tutorial/Itchiptool_Startpage.png?raw=true" alt="Itchiptool" width="300"/>
<img src="https://github.com/chris173972/my-tuya-devices-conversion/blob/main/tutorial/Itchiptool_Sourcedata.png?raw=true" alt="Itchiptool" width="300"/>

- Navigate to 'UPK2ESPHome'
- Click 'Analyse firmware dump' and select the firmware you downloaded earlier.
- Navigate to 'Source Data' and copy the JSON.
- On the device url, navigate to 'Launch Web Application'
- Navigate to 'Import' and paste the config you copied within 'Enter Template here'
- 'Click on OBK and apply new script from above'

**Connect to MQTT**
- Navigate to 'Config' -> 'Configure MQTT'
- Add your MQTT Login details.
- The device should now be added via the MQTT Integration within Home Assistant.

---

### To use ESPHome Firmware

**ESPHome Config using Itchiptool**

<img src="https://github.com/chris173972/my-tuya-devices-conversion/blob/main/tutorial/Itchiptool_Startpage.png?raw=true" alt="Itchiptool" width="300"/>
<img src="https://github.com/chris173972/my-tuya-devices-conversion/blob/main/tutorial/Itchiptool_ESPHome_Config.png?raw=true" alt="Itchiptool" width="300"/>

- Navigate to 'UPK2ESPHome'
- Click 'Analyse firmware dump' and select the firmware you downloaded earlier.
- Navigate to 'ESPHome YAML' and copy the YAML.

**Compile ESPHome Firmware**
- Navigate to installed ESPHome: https://esphome.io/guides/getting_started_hassio
- Select: New device
- Select: Continue
- Name your device -> Next
- Select BK72xx
- Select CB2S Wi-Fi Module -> Next
- Select Skip (we will be updating these details on yaml)
- Edit device created
- Paste content copied from 'ESPHome YAML'
- Select: Install
- Select: Manual download
- Please be patient. May take a while based upon machine used
- Select: UF2 package (recommended)

**Upload Firmware**
- Navigate to Device IP
- Navigate to 'Launch Web Application'
- Navigate to 'OTA' and press 'Browse'.
- Select your bin file generated by ESPHome

**Update device with ESPHome Firmware**
- Connect computer to hotspot: 'kickstart-????' (specific to your device)
- Add your wifi details and click save

**Connect to Home Assistant**
- Open home assistant
- Device should be detected within integrations 'add new device'
- If not, select ESPHome, Add device


**Star the project at https://github.com/tuya-cloudcutter/tuya-cloudcutter**
