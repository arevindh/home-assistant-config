[Buy](https://www.tatacliq.com/polycab-hohm-avenir-llp0103084-20w-smart-wi-fi-led-batten-white/p-mp000000011272731)

Fashing methord : Serial
Chip : ESP8266EX

```

light:
  - platform: color_temperature
    name: "Corridor Tubelight"
    color_temperature: output_component2
    brightness: output_component1
    cold_white_color_temperature: 6536 K
    warm_white_color_temperature: 2000 K
    restore_mode: RESTORE_DEFAULT_OFF
    default_transition_length: 1s
    
output:
  - platform: esp8266_pwm
    id: output_component2
    inverted: true
    pin: GPIO13
    max_power: 80%
  - platform: esp8266_pwm
    id: output_component1
    pin: GPIO05
    max_power: 80%
```
