# mbed-os-example-wifi #

WiFi example for mbed OS

## Getting started with the WiFi API ##

This is a quick example of a simple WiFi application using the WiFi and network-socket APIs that is provided as a part of [mbed-os](github.com/armmbed/mbed-os).

The program brings up the WiFi and the underlying network interface, and uses it to scans available networks, connects to a network, prints interface and connection details and performs simple HTTP operation.

### Supported hardware ###

* [UBLOX Odin board](https://developer.mbed.org/platforms/ublox-EVK-ODIN-W2/) built-in WiFi module
* [REALTEK_RTL8195AM](https://developer.mbed.org/platforms/REALTEK-RTL8195AM/) built-in WiFi module
* [NUCLEO_F429ZI](https://developer.mbed.org/platforms/ST-Nucleo-F429ZI/) with ESP8266-01 module using pins D1 D0
* [NUCLEO_L476RG](https://developer.mbed.org/platforms/ST-Nucleo-L476RG/) with ESP8266-01 module using pins D8 D2
* Other mbed target with ESP2866 module (Board it's connected to shouldn't have other network interface eg. Ethernet)

ESP2866 is a fallback option and will be used if the build is for unsupported platform.

#### Connecting the ESP2866 ####

To connect the ESP8266 module to your development board, look at the [ESP8266 Cookbook page](https://developer.mbed.org/users/4180_1/notebook/using-the-esp8266-with-the-mbed-lpc1768/). In general, this means hooking up the ESP8266 TX pin to `D0` and the ESP8266 RX pin to `D1` on your development board.

**Note on NUCLEO boards:** On the NUCLEO boards, pins `D0` and `D1` are used for serial communication with the computer. Use pins `D8` (to ESP8266 TX) and `D2` (to ESP8266 RX) instead.

##  Getting started

1. Import the example

  ```
  mbed import mbed-os-example-wifi
  cd mbed-os-example-wifi
  ```
2. Configure the WiFi credentials

  Edit ```mbed_app.json``` to include correct SSID and Password:

  ```
      "config": {
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

3. Compile and generate binary

  For example, for `GCC`:

  ```
  mbed compile -t GCC_ARM -m UBLOX_EVK_ODIN_W2
  ```

## Documentation ##

More information on the network-socket API can be found in the [mbed handbook](https://docs.mbed.com/docs/mbed-os-api-reference/en/5.2/APIs/communication/network_sockets/).
