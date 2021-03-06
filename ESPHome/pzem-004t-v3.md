Product link :  [Robu](https://robu.in/product/pzem-004t-multi-function-ac-power-monitor-module/), [Techtonics](https://www.techtonics.in/peacefair-pzem-004t-ac-multi-function-electric-energy-metering-power-monitor) | [ESPHome](https://esphome.io/components/sensor/pzemac.html)

Description: This Peacefair PZEM-004T Multi-function AC Power Monitor is very popular in electrical consumption measurement projects. It is capable of measuring four interrelated electrical variables as voltage, current, power, and energy. 

```yaml
esphome:
  name: kseb
  platform: ESP8266
  board: d1_mini

# Enable logging
logger:

ota:
  password: !secret ota_password

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_pass

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Kseb Fallback Hotspot"
    password: !secret failback_pass
  power_save_mode: none
captive_portal:

api:
  password: !secret device_pass

uart:
  rx_pin: D1
  tx_pin: D2
  baud_rate: 9600

modbus:

sensor:
  - platform: pzemac
    current:
      name: "KSEB Grid Current"
      filters:
        - calibrate_linear:
            - 0.0 -> 0.0
            - 0.593 -> 0.58
            - 1.412 -> 1.37
            - 1.799 -> 1.77
            - 1.817 -> 1.78
    voltage:
      name: "KSEB Grid Voltage"
    energy:
      name: "KSEB Grid Energy"
    power:
      name: "KSEB Grid Power"
    frequency:
      name: "KSEB Grid Frequency"
    power_factor:
      name: "KSEB Grid Power Factor"
    update_interval: 5s
    
```
