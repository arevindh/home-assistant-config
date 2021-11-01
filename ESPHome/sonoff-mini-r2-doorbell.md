Product link : [Amazon](https://www.amazon.in/AC100-240V-Compatible-Assistant-Supports-Firmware/dp/B07WJFHBMT)

Description : Connect switch between S1 and S2 and Regular doorbell at output. The device will auto power off in 200ms after switch on.

```yaml
substitutions:
  device_name: doorbell

esphome:
  name: ${device_name}
  platform: ESP8266
  board: esp8285

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_pass
  ap:
    ssid: "Doorbell ESPHOME"
    password: !secret failback_pass

logger:
  
api:
  reboot_timeout: 15min
  password: !secret device_pass

ota:
  password: !secret ota_password

sensor:
  - platform: wifi_signal
    name: ${device_name} Wifi Signal Strength
    update_interval: 60s
  - platform: uptime
    name: ${device_name} Uptime

#######################################
# Device specific Config Begins Below #
#######################################

binary_sensor:
  - platform: gpio
    pin: GPIO00
    id: reset
    internal: true
    filters:
      - invert:
      - delayed_off: 10ms
    on_press:
      - switch.toggle:
          id: relay_1

  - platform: gpio
    name: ${device_name}_status
    pin: GPIO04
    id: switch_1
    on_press:
      then:
        - switch.turn_on:
            id: relay_1
    on_release:
      then:
        - switch.turn_off:
            id: relay_1

switch:
  - platform: gpio
    name: ${device_name}_switch
    icon: "mdi: bell-ring"
    pin: GPIO12
    id: relay_1
    restore_mode: restore_default_off
    on_turn_on:
    - delay: 200ms
    - switch.turn_off: relay_1

status_led:
  pin:
    number: GPIO13
    inverted: true

output:
  - platform: esp8266_pwm
    id: blue_led
    pin: GPIO13
    inverted: True

light:
  # the 4 lines below define the Blue LED light on Sonoff Mini, to expose in HomeAssistant remove line "internal: true"
  - platform: monochromatic
    name: ${device_name}_blueled
    output: blue_led
    internal: true # hides the Blue LED from HomeAssistant

```
