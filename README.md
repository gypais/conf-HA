# conf-HA
je place ici toute la conf pour HA, Frigate, esp etc.


pour installer le code (generé par esphome) si le wifi marche pas
https://web.esphome.io/?dashboard_install
puis aller sous esphome dans HA


code de l'esp
substitutions:
  name: capteur-odeur
  friendly_name: Capteur odeurs

esphome:
  name: ${name}
  friendly_name: ${friendly_name}
  min_version: 2024.6.0
  name_add_mac_suffix: false
  project:
    name: esphome.web
    version: dev

esp32:
  board: esp32dev
  framework:
    type: arduino

# Enable logging
logger:

# Enable Home Assistant API
api:

# Allow Over-The-Air updates
ota:
- platform: esphome

# Allow provisioning Wi-Fi via serial
improv_serial:

wifi:
  # Set up a wifi access point
  ap:
    ssid: "Capteur-odeur"
    password: "231123112311"
  ssid: "gypaisSL en bas"
  password: "231123112311"

# In combination with the `ap` this allows the user
# to provision wifi credentials to the device via WiFi AP.
captive_portal:

dashboard_import:
  package_import_url: github://esphome/example-configs/esphome-web/esp32.yaml@main
  import_full_config: true

# Sets up Bluetooth LE (Only on ESP32) to allow the user
# to provision wifi credentials to the device.
esp32_improv:
  authorizer: none

# To have a "next url" for improv serial
web_server:
  port: 80

sensor:
  - platform: adc
    pin: GPIO36
    name: "Odeur 1"
    update_interval: 2s
    accuracy_decimals: 3
    attenuation: 11db
  - platform: adc
    pin: GPIO39
    name: "Odeur 2"
    update_interval: 2s
    accuracy_decimals: 3
    attenuation: 11db  
  - platform: adc
    pin: GPIO34
    name: "Odeur 3"
    update_interval: 2s
    accuracy_decimals: 3
    attenuation: 11db 
  - platform: adc
    pin: GPIO35
    name: "Odeur 4"
    update_interval: 2s
    accuracy_decimals: 3
    attenuation: 11db 

  - platform: dht
    pin: GPIO2
    temperature:
      name: "Température odeur"
    humidity:
      name: "Humidité odeur"
    model: DHT22
    update_interval: 10s


#output:
#  - platform: gpio
#    pin: GPIO25
#    id: GPIO25
    
#switch:
#  - platform: output
#    name: "Switch 0 à 3.3v"
#    output: GPIO25    

text_sensor:
  - platform: wifi_info
    ip_address:
      name: "IP Address"

button:
  - platform: restart
    name: "Redémarrer ESP"      
