Product link : [Amazon](https://www.amazon.in/gp/product/B0932VPMSL/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1)

Description : 4 relays , 4 switches 1 Buzzer 

Working perfectly

Mine had an issue with pcb Switch 4 was not properly connected GPIO2, so I used a wire to connect it

Pinout

![1-pinout](https://user-images.githubusercontent.com/693151/183081837-cb54f5fb-9846-450d-8cb2-b169b4100e19.jpg)


```yaml
binary_sensor:
  - platform: gpio
    internal: true
    pin:
      number: GPIO10
      inverted: True
    name: "Smartmesh Switch 2"
    on_press:
      - switch.turn_on: relay_2
    on_release:
      - switch.turn_off: relay_2
    
  - platform: gpio
    pin:
      number: GPIO12
      inverted: True
    name: "Smartmesh Switch 3"
    internal: true
    on_press:
      - switch.turn_on: relay_3
    on_release:
      - switch.turn_off: relay_3
      
  - platform: gpio
    pin:
      number: GPIO2
      inverted: True
    name: "Smartmesh Switch 4"
    internal: true
    on_press:
      - switch.turn_on: relay_4
    on_release:
      - switch.turn_off: relay_4
    
  - platform: gpio
    pin:
      number: GPIO9
      inverted: True
    name: "Smartmesh Switch 1"
    internal: true
    on_press:
      - switch.turn_on: relay_1
    on_release:
      - switch.turn_off: relay_1

switch:
  - platform: gpio
    pin: 5
    name: "Smartmesh 1"
    id: relay_1
  - platform: gpio
    pin: 4
    name: "Smartmesh 2"
    id: relay_2
  - platform: gpio
    pin: 15
    name: "Smartmesh 3"
    id: relay_3
  - platform: gpio
    pin: 14
    name: "Smartmesh 4"
    id: relay_4
  - platform: gpio
    pin: 16
    name: "Smartmesh LED"
  - platform: gpio
    pin: 13
    name: "Smartmesh Buzzer"
```



![1-opened](https://user-images.githubusercontent.com/693151/183081988-026aa787-9c4d-4787-85b6-5666373c6449.jpg)
![1-backside](https://user-images.githubusercontent.com/693151/183081996-a5b171c0-4561-48bd-affd-c768acb601a8.jpg)
![1-front](https://user-images.githubusercontent.com/693151/183081999-40e1fd4c-5195-47cf-b38f-de3943de39e9.jpg)
