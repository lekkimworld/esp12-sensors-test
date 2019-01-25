# esp12-sensors-test
Project to test running my required temperature sensors (ds18b20) and a light photo-resistor off an ESP-12 instead of a full Arduino

Remember to add vars.h to keep variables such as SSID of wi-fi plus passcode. The file also keeps the 
sensorId transmitted for the light sensor as well as the webservice to post to. Below is an example file.
```
const char ssid1[]   = "wifi-ssid1";
const char pass1[]   = "foo";
const char ssid2[]   = "wifi-ssid2";
const char pass2[]   = "bar";

// test or prod
const boolean isProd = false;

// servers
const char serverProd = "http://boiling-tree-34283.herokuapp.com";
const char serverTest = "http://trailing-sky-43213.herokuapp.com";

// enable DS18B20 on pin 12
#define SENSORTYPE_DS18B20
#define DS18B20_PIN 12

// enable DHT22 on pin 4 with specified deviceID's
#define SENSORTYPE_DHT22
#define DHT_PIN 4
#define DHT_TYPE DHT22
#define SENSORID_DHT22_TEMP "stue_dht_temp"
#define SENSORID_DHT22_HUM "stue_dht_hum"

// option to enable LDR on pin A0
//#define SENSORTYPE_LDR
//#define SENSORID_LDR "outside_light"
//#define LDR_PIN A0
```

Use esptool to write firmware after compiling in Arduino IDE
```bash
./esptool.py --port /dev/cu.usbserial-A50285BI write_flash 0x00000 /var/folders/7b/m6y7lf294fvfbjy8kjqqd9lhxfhvry/T/arduino_build_38010/esp12_blink.ino.bin
```

Use esptool.py to clear firmware using blank
```bash
./esptool.py --port /dev/cu.usbserial-A50285BI write_flash 0x00000 esp-01/boot_v1.7.bin 0x01000 esp-01/user1.1024.new.2.bin 0xfc000 esp-01/esp_init_data_default.bin 0x7e000 esp-01/blank.bin 0xfe000 esp-01/blank.bin
```

## esptool ##
https://github.com/espressif/esptool
