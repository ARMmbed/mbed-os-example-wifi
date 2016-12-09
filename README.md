# mbed-os-example-wifi #

WiFi example for mbed OS

## Getting started with the WiFi API ##

This is a quick example of a simple WiFi application using the WiFi and network-socket APIs that is provided as a part of [mbed-os](github.com/armmbed/mbed-os).

The program brings up the WiFi and the underlying network interface, and uses it to scans available networks, connects to a network, prints interface and connection details and performs simple HTTP operation.

### Supported hardware ###

* [UBLOX Odin board](https://developer.mbed.org/platforms/ublox-EVK-ODIN-W2/) (`UBLOX_EVK_ODIN_W2` target when using mbed CLI)
* Other mbed target with ESP2866 module (Board it's connected to shouldn't have other network interface eg. Ethernet)

ESP2866 is a fallback option and will be used if the build is for unsupported platform.

#### Connecting the ESP2866 ####

ESP module needs to be connected to RX and TX UART pins (+ power and ground) on your target board. That can be achieved using Grove shield or connected directly using jumper wires, please note that not all Arduino form factor boards have UART compatible with the Grove shiled.

For Grove shield TX has to be connected to D1 and RX to D0.

Make sure that UART module you're connecting ESP to is different than the debug UART connected to your USB port.

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
