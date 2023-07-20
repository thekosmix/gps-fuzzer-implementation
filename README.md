# gps-fuzzer-implementation
MQTT & Web-Socket (WS) implementation for demo of gps-fuzzer

## install dependancies and projects
1. [nodejs & npm](https://nodejs.org/en/download)
2. [mosquitto](https://mosquitto.org/blog/2011/03/mosquitto-in-mac-homebrew/)
3. checkout [gps-fuzzer](https://github.com/Thetaonelab/gps-fuzzer) - backend server for producing random lat-long for front-end to consume
4. checkout [Implementation-of-gps-fuzzer](https://github.com/sbhsb/Implementation-of-gps-fuzzer)

## Configurigure to run locally 

### Changing the MQTT & WS address
1. Go to Map.js file in Implementation-of-gps-fuzzer and replace existing `var client = ...` with your local mosquitto setup `var client = mqtt.connect("ws://127.0.0.1:8080", {clientId: "dfndmnfnbsfb_client"})`
2. Go to server.js file of gps-fuzzer and replace existing `var client = ...` with your local mosquitton setup `var client = mqtt.connect("mqtt://127.0.0.1", {clientId: "dfndmnfnbsfb_server"})`

### Enabling mosquitto to support WS
1. Follow the instructions mentioned [here](https://cedalo.com/blog/enabling-websockets-over-mqtt-with-mosquitto/#For_MacOS)
2. Restart Mosquitto server

## Running the applications
1. Run backend server: `cd gps-fuzzer && npm i && npm start`
2. start fuzzing by hitting the backend server
```
curl --location 'http://localhost:9999/fuzzgps' \
--header 'Content-Type: application/json' \
--data '{
        "payload":{ 
            "tripId":15, 
            "deviceId":123
        },
        "points":[{ "lati": 25.30, "longi": 88.30 }, { "lati": 24.30, "longi": 88.00 } , { "lati": 25.30, "longi": 89.00 }],
        "topic":"eyezon/livegps",
        "interval":400,
        "duration":4000,
        "loop":true
    }'
```
3. Subscribe on command line to check if it's actually publishing: `mosquitto_sub -h localhost -t eyezon/livegps --id dfndmnfnbsfb_cmd_client`
4. Run front-end: `cd Implementation-of-gps-fuzzer && npm i && npm start`
5. The last command will open web-browser at port [localhost:3000](http://localhost:3000/) and you'll see a small vehicle moving randomly
