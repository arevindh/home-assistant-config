Product link : NA

Description : Work in progress 

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