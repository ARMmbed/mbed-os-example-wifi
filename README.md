# mbed-os-example-wifi #

WiFi example for mbed OS

## Getting started with the WiFi API ##

This is a quick example of a simple WiFi application using the WiFi and network-socket APIs that is provided as a part of [mbed-os](github.com/armmbed/mbed-os).

The program brings up the WiFi and the underlying network interface, and uses it to scans available networks, connects to a network, prints interface and connection details and performs simple HTTP operation.

### Supported hardware ###

* [UBLOX Odin board](https://developer.mbed.org/platforms/ublox-EVK-ODIN-W2/) built-in WiFi module
* [REALTEK_RTL8195AM](https://developer.mbed.org/platforms/REALTEK-RTL8195AM/) built-in WiFi module
* [NUCLEO_F401RE](https://developer.mbed.org/platforms/ST-Nucleo-F401RE/) with [X-NUCLEO-IDW01M1](https://developer.mbed.org/components/X-NUCLEO-IDW01M1/) WiFi expansion board using pins D8 D2
* [NUCLEO_F429ZI](https://developer.mbed.org/platforms/ST-Nucleo-F429ZI/) with ESP8266-01 module using pins D1 D0
* [NUCLEO_L476RG](https://developer.mbed.org/platforms/ST-Nucleo-L476RG/) with ESP8266-01 module using pins D8 D2
* Other mbed targets with ESP8266 module or [X-NUCLEO-IDW01M1](https://developer.mbed.org/components/X-NUCLEO-IDW01M1/) expansion board
  *(the mbed target board the WiFi shield gets connected to shouldn't have any other network interface e.g. Ethernet)*

ESP8266 is a fallback option and will be used if the build is for unsupported platform.

#### Connecting the ESP8266 ####
To connect the ESP8266 module to your development board, look at the [ESP8266 Cookbook page](https://developer.mbed.org/users/4180_1/notebook/using-the-esp8266-with-the-mbed-lpc1768/). In general, this means hooking up the ESP8266 TX pin to `D0` and the ESP8266 RX pin to `D1` on your development board.

**Note:** on NUCLEO development boards, pins `D0` and `D1` are used for serial communication with the computer. Use pins `D8` (to ESP8266 TX) and `D2` (to ESP8266 RX) instead.

#### Connecting the X-NUCLEO-IDW01M1 ####
To connect the [X-NUCLEO-IDW01M1](https://developer.mbed.org/components/X-NUCLEO-IDW01M1/) expansion board to your NUCLEO development board, just plug the expansion board on top of the NUCLEO board using the Morpho connector.

##  Getting started

1. Import the example

   ```
   mbed import mbed-os-example-wifi
   cd mbed-os-example-wifi
   ```
2. Configure the WiFi shield to use

   Edit ```mbed_app.json``` to include correct WiFi shield, SSID and Password:

   ```
       "config": { 
 	  "wifi-shield": {
               "help": "Options are WIFI_ESP8266, WIFI_IDW01M1",
               "value": "WIFI_IDW01M1"
        	  },
           "wifi-ssid": {
               "help": "WiFi SSID",
               "value": "\"SSID\""
           },
           "wifi-password": {
               "help": "WiFi Password",
               "value": "\"Password\""
           }
       },
   ```

3. Copy the respective _ignore_ file to `.mbedignore`
   * Copy `esp8266-mbedignore` when using ESP8266 module.
   * Copy `idw01m1-mbedignore` when using [X-NUCLEO-IDW01M1](https://developer.mbed.org/components/X-NUCLEO-IDW01M1/) expansion board.
  
4. Compile and generate binary

   For example, for `GCC`:

   ```
   mbed compile -t GCC_ARM -m UBLOX_EVK_ODIN_W2
   ```
   
 5. Open a serial console session with the target platform using the following parameters:
    * **Baud rate:** 9600
    * **Data bits:** 8
    * **Stop bits:** 1
    * **Parity:** None
 
 6. Copy or drag the application `mbed-os-example-wifi.bin` in the folder `mbed-os-example-wifi/BUILD/<TARGET NAME>/<PLATFORM NAME>` onto the target board.
 
 7. The serial console should display a similar output to below, indicating a successful WiFi connection:
 ```
 WiFi example

Scan:
Network: Dave Hot Spot secured: Unknown BSSID: 00:01:02:03:04:05 RSSI: -58 Ch: 1
1 network available.

Connecting...
Success

MAC: 00:01:02:03:04:05
IP: 192.168.0.5
Netmask: 255.255.255.0
Gateway: 192.168.0.1
RSSI: -27

Sending HTTP request to www.arm.com...
sent 38 [GET / HTTP/1.1]
recv 64 [HTTP/1.1 301 Moved Permanently]

Done
```

## Documentation ##

More information on the network-socket API can be found in the [mbed handbook](https://docs.mbed.com/docs/mbed-os-api-reference/en/5.2/APIs/communication/network_sockets/).
