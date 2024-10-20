# Garage Door Lights

## Requirements
- Addressable LED stip with a WLED controller integrated with Home Assistant.
- A way to detect your door's open, closed and moving (opening/closing) states.  This can be done using two door sensors.  I use an [ESP Home Garage Door Controller](https://github.com/wernerhp/esphome/tree/main/garage-door) with two door sensors. 

## WLED
Configure the desired [presets](wled-presets.json) on your device.

## Automation
The garage door controller detects the closed, moving and opening states.  This can be done using two door switches and a template sensor.  e.g.
```yaml
{% set door_open = is_state("binary_sensor.wc_door_sensor_door", "on") %}
{% set door_closed = is_state("binary_sensor.bedroom_motion_sensor_motion", "on") %}
{% if door_open and not door_closed %}
  open
{% elif not door_open and not door_closed %}
  moving
{% elif not door_open and door_closed %}
  closed
{% else %}
  unknown
{% endif %}
```

The [automation](automation.yaml) uses the state form the door sensors to select one of the WLED presets.

## Demo

![Alt text](IMG_20221128_211637.jpg)

![Alt text](PXL_20231220_193948350.jpg)

<video src="VID_20220324_191508.mp4" controls title="Garage Door Light Automation"></video>
