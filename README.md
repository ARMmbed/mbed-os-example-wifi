# mbed-os-example-wifi #

Wi-fi example for mbed OS 5.0

## Getting started with the WiFi API ##

This is a quick example of a simple WiFi application using the WiFi and
network-socket APIs that is provided as a part of [mbed-os](github.com/armmbed/mbed-os).

The program brings up the WiFi and the underlying network interface, and uses it to
scans available networks, connects to a network, prints interface and connection details
and performs simple HTTP operation.

### Supported hardware ###

* UBLOX Odin board (UBLOX_EVK_ODIN_W2)
* ESP2866 module (Board it's connected to shouldn't have other network interface eg. Ethernet)

ESP2866 is a fallback option and will be used if the build is for unsupported platform.

## Configuration ##

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

## Documentation ##

More information on the network-socket API can be found in the [mbed handbook](https://docs.mbed.com/docs/mbed-os-api-reference/en/5.2/APIs/communication/network_sockets/).
