# airtouch4_lovelace_card
A custom Lovelace card for the AirTouch4 Integration

<img width="494" alt="airtouch _card" src="https://user-images.githubusercontent.com/59326901/138863952-e8635789-a3b3-4bb3-b973-6004e05235e1.png">

# Prerequsites
The AirTouch4 Integration
https://www.home-assistant.io/integrations/airtouch4/
https://github.com/home-assistant/core/tree/dev/homeassistant/components/airtouch4

Text Element (Installed via HACS)
https://github.com/custom-cards/text-element

# Setup
Install the AirTouch4 integration, then the Frontend "Text Element" Repository via HACS. The Text Element allows for text to be placed over a picture-elements card. This will allow for zone names to be changed / renamed without having to update the background images.

Add the airtouch folder from airtouch.zip into the www folder of the Home Assistant installation. 

[airtouch.zip](https://github.com/mycrouch/airtouch4_lovelace_card/files/7417211/airtouch.zip)

To enable the temperature up and down buttons on the card, scripts are required to call the climate.set_temperature service for each zone. Create two scripts for each zone (one up and one down) Example script code below and sample scripts.yaml available for download. Suggest a find and replace to update, for example replace lounge with zone name.

```
#Lounge
lounge_temp_up:
  alias: Lounge Temp Up
  sequence:
  - service: climate.set_temperature
    data_template:
      entity_id: climate.lounge
      temperature: '{{ state_attr(''climate.lounge'', ''temperature'') + 1 | float
        }}'
  mode: single
lounge_temp_down:
  alias: Lounge Temp Down
  sequence:
  - service: climate.set_temperature
    data_template:
      entity_id: climate.lounge
      temperature: '{{ state_attr(''climate.lounge'', ''temperature'') - 1 | float
        }}'
  mode: single
  ```
  
[scripts.yaml.zip](https://github.com/mycrouch/airtouch4_lovelace_card/files/7417349/scripts.yaml.zip)


Add a Manual Card to desired Lovelace View and paste the following code. 
- Update each entity code to reflect the integration entity, for example - entity: climate.lounge
- Update each coresponding text code for each - type: custom:text-element, for example - text: Lounge
- Update each service entry in the card to match the script names for each zone, for example - service: script.lounge_temp_down

# Lovelace Card

```
type: picture-elements
elements:
  - type: state-label
    entity: climate.ac_0
    style:
      top: 28%
      left: 69%
      title: null
      color: white
      font-size: 300%
    attribute: current_temperature
  - type: image
    entity: climate.ac_0
    style:
      top: 7%
      left: 41.5%
      title: null
      width: 5%
    state_image:
      cool: http://192.168.86.25:8123/local/airtouch/power_on.png
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      dry: http://192.168.86.25:8123/local/airtouch/power_on.png
      heat: http://192.168.86.25:8123/local/airtouch/power_on.png
      auto: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: image
    entity: climate.lounge
    style:
      top: 18.5%
      left: 3%
      title: null
      width: 4%
    state_image:
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: custom:text-element
    text: Lounge
    style:
      top: 18.5%
      left: 11%
      color: white
  - type: icon
    icon: mdi:minus-circle-outline
    tap_action:
      action: call-service
      service: script.lounge_temp_down
    style:
      top: 18.5%
      left: 20%
      color: white
  - type: state-label
    entity: climate.lounge
    style:
      top: 18.5%
      left: 25.5%
      title: null
      color: white
      font-size: 100%
    attribute: temperature
  - type: icon
    icon: mdi:plus-circle-outline
    tap_action:
      action: call-service
      service: script.lounge_temp_up
    style:
      top: 18.5%
      left: 30.5%
      color: white
  - type: state-label
    entity: climate.lounge
    style:
      top: 17%
      left: 35.5%
      title: null
      color: white
      font-size: 70%
    attribute: current_temperature
  - type: image
    entity: climate.kitchen
    style:
      top: 29%
      left: 3%
      title: null
      width: 4%
    state_image:
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: custom:text-element
    text: Kitchen
    style:
      top: 29%
      left: 11%
      color: white
  - type: icon
    icon: mdi:minus-circle-outline
    tap_action:
      action: call-service
      service: script.kitchen_temp_down
    style:
      top: 29%
      left: 20%
      color: white
  - type: state-label
    entity: cover.kitchen_vent
    style:
      top: 29%
      left: 25.2%
      title: null
      color: white
      font-size: 100%
    attribute: current_position
  - type: icon
    icon: mdi:plus-circle-outline
    tap_action:
      action: call-service
      service: script.kitchen_temp_up
    style:
      top: 29%
      left: 30.5%
      color: white
  - type: image
    entity: climate.powder
    style:
      top: 39.5%
      left: 3%
      title: null
      width: 4%
    state_image:
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: custom:text-element
    text: Powder
    style:
      top: 39.5%
      left: 11%
      color: white
  - type: icon
    icon: mdi:minus-circle-outline
    tap_action:
      action: call-service
      service: script.powder_temp_down
    style:
      top: 39.5%
      left: 20%
      color: white
  - type: state-label
    entity: cover.powder_vent
    style:
      top: 39.5%
      left: 25.2%
      title: null
      color: white
      font-size: 100%
    attribute: current_position
  - type: icon
    icon: mdi:plus-circle-outline
    tap_action:
      action: call-service
      service: script.powder_temp_up
    style:
      top: 39.5%
      left: 30.5%
      color: white
  - type: image
    entity: climate.office
    style:
      top: 50%
      left: 3%
      title: null
      width: 4%
    state_image:
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: custom:text-element
    text: Office
    style:
      top: 50%
      left: 10%
      color: white
  - type: icon
    icon: mdi:minus-circle-outline
    tap_action:
      action: call-service
      service: script.office_temp_down
    style:
      top: 50%
      left: 20%
      color: white
  - type: state-label
    entity: climate.office
    style:
      top: 50%
      left: 25.5%
      title: null
      color: white
      font-size: 100%
    attribute: temperature
  - type: icon
    icon: mdi:plus-circle-outline
    tap_action:
      action: call-service
      service: script.office_temp_up
    style:
      top: 50%
      left: 30.5%
      color: white
  - type: state-label
    entity: climate.office
    style:
      top: 48.5%
      left: 35.5%
      title: null
      color: white
      font-size: 70%
    attribute: current_temperature
  - type: image
    entity: climate.master
    style:
      top: 60.5%
      left: 3%
      title: null
      width: 4%
    state_image:
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: custom:text-element
    text: Master
    style:
      top: 60.5%
      left: 11%
      color: white
  - type: icon
    icon: mdi:minus-circle-outline
    tap_action:
      action: call-service
      service: script.master_temp_down
    style:
      top: 60.5%
      left: 20%
      color: white
  - type: state-label
    entity: climate.master
    style:
      top: 60.5%
      left: 25.5%
      title: null
      color: white
      font-size: 100%
    attribute: temperature
  - type: icon
    icon: mdi:plus-circle-outline
    tap_action:
      action: call-service
      service: script.master_temp_up
    style:
      top: 60.5%
      left: 30.5%
      color: white
  - type: state-label
    entity: climate.master
    style:
      top: 59%
      left: 35.5%
      title: null
      color: white
      font-size: 70%
    attribute: current_temperature
  - type: image
    entity: climate.ethan
    style:
      top: 71%
      left: 3%
      title: null
      width: 4%
    state_image:
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: custom:text-element
    text: Ethan
    style:
      top: 71%
      left: 10%
      color: white
  - type: icon
    icon: mdi:minus-circle-outline
    tap_action:
      action: call-service
      service: script.ethan_temp_down
    style:
      top: 71%
      left: 20%
      color: white
  - type: state-label
    entity: climate.ethan
    style:
      top: 71%
      left: 25.5%
      title: null
      color: white
      font-size: 100%
    attribute: temperature
  - type: icon
    icon: mdi:plus-circle-outline
    tap_action:
      action: call-service
      service: script.ethan_temp_up
    style:
      top: 71%
      left: 30.5%
      color: white
  - type: state-label
    entity: climate.ethan
    style:
      top: 69%
      left: 35.5%
      title: null
      color: white
      font-size: 70%
    attribute: current_temperature
  - type: image
    entity: climate.alexis
    style:
      top: 81.5%
      left: 3%
      title: null
      width: 4%
    state_image:
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: custom:text-element
    text: Alexis
    style:
      top: 81.5%
      left: 10%
      color: white
  - type: icon
    icon: mdi:minus-circle-outline
    tap_action:
      action: call-service
      service: script.alexis_temp_down
    style:
      top: 81.5%
      left: 20%
      color: white
  - type: state-label
    entity: climate.alexis
    style:
      top: 81.5%
      left: 25.5%
      title: null
      color: white
      font-size: 100%
    attribute: temperature
  - type: icon
    icon: mdi:plus-circle-outline
    tap_action:
      action: call-service
      service: script.alexis_temp_up
    style:
      top: 81.5%
      left: 30.5%
      color: white
  - type: state-label
    entity: climate.alexis
    style:
      top: 79.5%
      left: 35.5%
      title: null
      color: white
      font-size: 70%
    attribute: current_temperature
  - type: image
    entity: climate.garage
    style:
      top: 92%
      left: 3%
      title: null
      width: 4%
    state_image:
      fan_only: http://192.168.86.25:8123/local/airtouch/power_on.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: custom:text-element
    text: Garage
    style:
      top: 92%
      left: 11%
      color: white
  - type: icon
    icon: mdi:minus-circle-outline
    tap_action:
      action: call-service
      service: script.garage_temp_down
    style:
      top: 92%
      left: 20%
      color: white
  - type: state-label
    entity: cover.garage_vent
    style:
      top: 92%
      left: 25.2%
      title: null
      color: white
      font-size: 100%
    attribute: current_position
  - type: icon
    icon: mdi:plus-circle-outline
    tap_action:
      action: call-service
      service: script.garage_temp_up
    style:
      top: 92%
      left: 30.5%
      color: white
  - type: image
    entity: climate.ac_0
    style:
      top: 60%
      left: 53.7%
      title: null
      width: 10%
    state_image:
      cool: http://192.168.86.25:8123/local/airtouch/mode_cool.png
      fan_only: http://192.168.86.25:8123/airtouch/local/mode_fan_only.png
      dry: http://192.168.86.25:8123/local/airtouch/mode_dry.png
      heat: http://192.168.86.25:8123/local/airtouch/mode_heat.png
      auto: http://192.168.86.25:8123/local/airtouch/mode_auto.png
      'off': http://192.168.86.25:8123/local/airtouch/power_off.png
  - type: state-label
    entity: climate.ac_0
    style:
      top: 72%
      left: 53.7%
      title: null
      color: white
      font-size: 100%
    state: null
  - type: image
    entity: climate.ac_0
    attribute: fan_mode
    style:
      top: 60%
      left: 84.5%
      title: null
      width: 10%
    state_image:
      low: http://192.168.86.25:8123/local/fan_low.png
      medium: http://192.168.86.25:8123/local/fan_med.png
      high: http://192.168.86.25:8123/local/fan_high.png
      auto: http://192.168.86.25:8123/local/fan_auto.png
  - type: state-label
    entity: climate.ac_0
    style:
      top: 72%
      left: 84.5%
      title: null
      color: white
      font-size: 100%
    attribute: fan_mode
entity: climate.ac_0
state_image:
  'off': http://192.168.86.25:8123/local/airtouch/airtouch_cool.png
  cool: http://192.168.86.25:8123/local/airtouch/airtouch_cool.png
  fan_only: http://192.168.86.25:8123/local/airtouch/airtouch_fan_only.png
  dry: http://192.168.86.25:8123/local/airtouch/airtouch_dry.png
  heat: http://192.168.86.25:8123/local/airtouch/airtouch_heat.png
  auto: http://192.168.86.25:8123/local/airtouch/airtouch_cool.png
  ```
