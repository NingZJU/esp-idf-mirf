# esp-idf-mirf
A port of the Mirf library for ESP-IDF.   
The library provides basic control of the Nordic NRF24L01/NRF24L01+ RF modules.

I ported from [here](https://github.com/nopnop2002/Arduino-STM32-nRF24L01).   

# Software requirements
esp-idf v4.4 or later.   
This is because this version supports ESP32-C3.   

# Installation for ESP32

```Shell
git clone https://github.com/nopnop2002/esp-idf-mirf
cd esp-idf-mirf/Peer-to-peer
idf.py set-target esp32
idf.py menuconfig
idf.py flash
```

# Installation for ESP32-S2

```Shell
git clone https://github.com/nopnop2002/esp-idf-mirf
cd esp-idf-mirf/Peer-to-peer
idf.py set-target esp32s2
idf.py menuconfig
idf.py flash
```

# Installation for ESP32-C3

```Shell
git clone https://github.com/nopnop2002/esp-idf-mirf
cd esp-idf-mirf/Peer-to-peer
idf.py set-target esp32c3
idf.py menuconfig
idf.py flash
```

__Note__   
For some reason, there are development boards that cannot use GPIO06, GPIO08, GPIO09, GPIO19 for SPI clock pins.   
According to the ESP32C3 specifications, these pins can also be used as SPI clocks.   
I used a raw ESP-C3-13 to verify that these pins could be used as SPI clocks.   

# Configuration for Transceiver
![config-mirf-1](https://user-images.githubusercontent.com/6020549/154790117-90def013-f960-42b4-a02c-44dcba2c3be5.jpg)
![config-mirf-2](https://user-images.githubusercontent.com/6020549/154790120-73f7d79d-f4e2-413a-a61d-f6b77e103ebc.jpg)

# Wirering

|nRF24L01||ESP32|ESP32-S2|ESP32-C3|
|:-:|:-:|:-:|:-:|:-:|
|MISO|--|GPIO19|GPIO33|GPIO18|
|MOSI|--|GPIO23|GPIO35|GPIO19|
|SCK|--|GPIO18|GPIO36|GPIO10|
|CE|--|GPIO16|GPIO37|GPIO9|
|CSN|--|GPIO17|GPIO38|GPIO8|
|GND|--|GND|GND|GND|
|VCC|--|3.3V|3.3V|3.3V|

__You can change it to any pin using menuconfig.__   


# Communicat with AtMega/STM32/ESP8266/ESP8285 using Arduino environment  
I used [this](https://github.com/nopnop2002/Arduino-STM32-nRF24L01) library on Arduino environment.   
__You need to match the payload size and channel with Arduino and esp-idf.__   

- Arduino environment   
```C++
Mirf.payload = sizeof(mydata.value);
Mirf.channel = 90;
Mirf.config();
```
- esp-idf   
```C
uint8_t payload = sizeof(value);
uint8_t channel = 90;
Nrf24_config(&dev, channel, payload);
```

# Communicat with Raspberry Pi
I used [this](https://github.com/nopnop2002/Raspberry-Mirf) library on Raspberry Pi.   

# Important
When changing the settings of the nRF24L01, it is necessary to power cycle the nRF24L01 before executing.   
Because nRF24L01 remembers the previous setting.   
nRF24L01 does not have Software Reset function.   

# Reference

https://github.com/nopnop2002/esp-idf-mirf2mqtt

