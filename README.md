# Pump Patrol

ESPHome package template for monitoring pump current and configurable inputs.

## Example device configuration

Create a device configuration such as `sewer-pump-device.yaml` alongside the package configuration, replacing the example API and OTA keys with your own:

```yaml
# sewer-pump-device.yaml
substitutions:
  device_name: "sewer-pump"
  friendly_name: "Sewer Pump"
  api_key: "{my API Key}"
  ota_key: "{my OTA Key}"

  # Amp Threshold Adjustments
  running_threshold: "1.0" # Should always be higher than stopping_threshold. When the pump draw is above this value, it will be considered to be running
  stopping_threshold: "0.8" # Should always be lower than running_threshold. When the pump draw is under this value, it will be considered to be off
  input_voltage: "120.0" # Used to calculate watts. Set to your approximate line voltage

  # Input 1
  input_1_internal: "false" # Shows up in Home Assistant if false; hidden if true
  input_1_name: "Tank High"
  input_1_triggers_alert: "true"

  # Input 2
  # input_2_internal: "true" # Shows up in Home Assistant if false; hidden if true
  # input_2_name: "Input 2"
  # input_2_triggers_alert: "false"

  # Input 3
  # input_3_internal: "true" # Shows up in Home Assistant if false; hidden if true
  # input_3_name: "Input 3"
  # input_3_triggers_alert: "false"

packages:
  pump_core:
    url: https://github.com/jeffremps/Pump-Patrol
    file: pump-patrol-template.yaml
    refresh: always
    ref: main
```

The package provides defaults for Inputs 2 and 3, so those substitutions can be uncommented and changed as needed. Set `running_threshold` higher than `stopping_threshold`; the pump state turns on at the running threshold and turns off at the stopping threshold, retaining its previous state between them.
