
```
esphome:
  name: mfm384
  friendly_name: mfm384

esp8266:
  board: d1_mini

# ---------------- UART (RS485 via XY-485 board) ----------------
uart:
  id: mod_bus
  tx_pin: GPIO12   # D6 -> TXD
  rx_pin: GPIO13   # D7 -> RXD
  baud_rate: 9600
  stop_bits: 1

# ---------------- Modbus ----------------
modbus:
  id: modbus1
  flow_control_pin: GPIO14 

modbus_controller:
  - id: mfm
    address: 1
    modbus_id: modbus1
    update_interval: 5s

sensor:
  # -------------------------------------------------------------------------
  # VOLTAGE (L1, L2, L3)
  # -------------------------------------------------------------------------
  - platform: modbus_controller
    modbus_controller_id: mfm
    id: voltage_l1
    address: 0
    name: "Voltage L1"
    unit_of_measurement: "V"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 1

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: voltage_l2
    address: 2
    name: "Voltage L2"
    unit_of_measurement: "V"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 1

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: voltage_l3
    address: 4
    name: "Voltage L3"
    unit_of_measurement: "V"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 1

  # -------------------------------------------------------------------------
  # CURRENT (L1, L2, L3) - Raw from Meter (likely rounded)
  # -------------------------------------------------------------------------
  - platform: modbus_controller
    modbus_controller_id: mfm
    id: current_l1
    address: 16
    name: "Current L1"
    unit_of_measurement: "A"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: current_l2
    address: 18
    name: "Current L2"
    unit_of_measurement: "A"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: current_l3
    address: 20
    name: "Current L3"
    unit_of_measurement: "A"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  # -------------------------------------------------------------------------
  # ACTIVE POWER (L1, L2, L3)
  # -------------------------------------------------------------------------
  - platform: modbus_controller
    modbus_controller_id: mfm
    id: power_l1
    address: 24
    name: "Power L1"
    unit_of_measurement: "W"
    register_type: read
    value_type: FP32_R
    filters:
      - multiply: 1000  # Convert kW to W

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: power_l2
    address: 26
    name: "Power L2"
    unit_of_measurement: "W"
    register_type: read
    value_type: FP32_R
    filters:
      - multiply: 1000

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: power_l3
    address: 28
    name: "Power L3"
    unit_of_measurement: "W"
    register_type: read
    value_type: FP32_R
    filters:
      - multiply: 1000

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: total_power
    address: 42
    name: "Total Power"
    unit_of_measurement: "W"
    state_class: measurement
    register_type: read
    value_type: FP32_R
    filters:
      - multiply: 1000

  # -------------------------------------------------------------------------
  # ENERGY & FREQUENCY
  # -------------------------------------------------------------------------
  - platform: modbus_controller
    modbus_controller_id: mfm
    id: total_import
    device_class: energy
    state_class: total_increasing
    address: 96
    name: "Total Import Energy"
    unit_of_measurement: "kWh"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: total_export
    device_class: energy
    state_class: total_increasing
    address: 98
    name: "Total Export Energy"
    unit_of_measurement: "kWh"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: frequency
    address: 56
    name: "Frequency"
    unit_of_measurement: "Hz"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  # -------------------------------------------------------------------------
  # MAX DEMAND CURRENT (L1, L2, L3)
  # -------------------------------------------------------------------------
  - platform: modbus_controller
    modbus_controller_id: mfm
    id: max_i1_demand
    address: 692
    name: "Max Demand Current L1"
    unit_of_measurement: "A"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: max_i2_demand
    address: 694
    name: "Max Demand Current L2"
    unit_of_measurement: "A"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  - platform: modbus_controller
    modbus_controller_id: mfm
    id: max_i3_demand
    address: 696
    name: "Max Demand Current L3"
    unit_of_measurement: "A"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2


  # ---------------- TOTAL NET ENERGY ----------------
  - platform: modbus_controller
    modbus_controller_id: mfm
    id: total_net_kwh
    device_class: energy
    state_class: total_increasing
    address: 60
    name: "Total Net Energy"
    unit_of_measurement: "kWh"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  # ---------------- AVERAGE ----------------
  - platform: modbus_controller
    modbus_controller_id: mfm
    name: "Average Current"
    id: avg_current
    address: 22
    unit_of_measurement: "A"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 2

  - platform: modbus_controller
    modbus_controller_id: mfm
    name: "Average Voltage"
    id: avg_voltage_ln
    address: 6
    unit_of_measurement: "V"
    register_type: read
    value_type: FP32_R
    accuracy_decimals: 1


```
