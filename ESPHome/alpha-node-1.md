Product link : NA [Documentation](../Docs/AlfaNode_v1.pdf)

Description : Work in progress 

Pinout

|PIN|Function||
|--- |--- |--- |
|GPIO 00|NA|NOT Available; but can be tapped from the D1mini|
|GPIO 01|Button1|DO NOT CONNECT TO TOGGLE SW; boot fails|
|GPIO 02|User|Broken out: Free|
|GPIO 03|SW1||
|GPIO 04|I2C SDA|Broken out; Free|
|GPIO 05|I2C SCL|Broken out: Free|
|GPIO 12|SW2||
|GPIO 13|Relay 2||
|GPIO 14|Relay 1||
|GPIO 15|User|Broken out: Free|
|GPIO 16|NA|NOT Available; but can be tapped from the D1mini|
|GPIO 17|ADC|Broken out: Free|


```yaml
esphome:
  name: alpha-node-01
  platform: ESP8266
  board: d1_mini

# Enable logging
logger:

# Enable Home Assistant API
api:
  password: !secret api_password

ota:
  password: !secret ota_password

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_pass

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Alpha-Node-01 Fallback Hotspot"
    password: !secret failback_pass

captive_portal:

```
