Product link : [Amazon.in](https://www.amazon.in/gp/product/B07KGFQTV5/)

Details : Only White is usable in current situation 

```yaml
esphome:
  name: light-master-bedroom
  platform: ESP8266
  board: esp01_1m

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_pass
  
  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Light-Master-Bed-Room Fallback"
    password: !secret failback_pass

captive_portal:

# Enable logging
logger:

# Enable Home Assistant API
api:
  password: !secret device_pass


ota:
  password: !secret device_pass
  
light:
  - platform: cwww
    id: master_bedroom_light
    name: "Master bedroom light"
    constant_brightness: false
    # red: color_red
    # green: color_green
    # blue: color_blue
    # color_interlock: true
    cold_white: cold_white
    warm_white: warm_white
    cold_white_color_temperature: 6536 K
    warm_white_color_temperature: 5000 K
    restore_mode: RESTORE_DEFAULT_OFF
    
# Example output entry
output:
  - platform: esp8266_pwm
    id: warm_white
    pin: GPIO12
    max_power: 20%
  # - platform: esp8266_pwm
  #   id: color_green
  #   pin: GPIO4
  #   max_power: 100%
  # - platform: esp8266_pwm
  #   id: color_red
  #   pin: GPIO5
  #   max_power: 100%
  # - platform: esp8266_pwm
  #   id: color_blue
  #   pin: GPIO13
  #   max_power: 100%
  - platform: esp8266_pwm
    id: cold_white
    pin: GPIO14
    max_power: 100%
```
