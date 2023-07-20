# gps-fuzzer-implementation
MQTT & Web-socket implementation for demo of gps-fuzzer

## install dependancies and projects
1. [nodejs & npm](https://nodejs.org/en/download)
2. [mosquitto](https://mosquitto.org/blog/2011/03/mosquitto-in-mac-homebrew/)
3. checkout [gps-fuzzer](https://github.com/Thetaonelab/gps-fuzzer) - backend server for producing random lat-long for front-end to consume
4. checkout [Implementation-of-gps-fuzzer](https://github.com/sbhsb/Implementation-of-gps-fuzzer)

## Configurigure to run locally 
### Changing the MQTT & WS address
1. Go to Map.js file in Implementation-of-gps-fuzzer and replace existing `var client = ...` with your local mosquitto setup `var client = mqtt.connect("ws://127.0.0.1:8080", {clientId: "dfndmnfnbsfb_client"})`
2. Go to server.js file of 
