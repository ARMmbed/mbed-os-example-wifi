# mbed-os-example-wifi #

Wi-Fi example for Mbed OS

(Note: To see this example in a rendered form you can import into the Arm Mbed Online Compiler, please see [the documentation](https://os.mbed.com/docs/mbed-os/latest/apis/wi-fi.html#wi-fi-example).)

## Getting started with the Wi-Fi API ##

This is an example of a Wi-Fi application using the Wi-Fi APIs that [Mbed OS](https://github.com/ARMmbed/mbed-os) provides.

The program brings up the Wi-Fi and the underlying network interface and uses it to scan available networks, connects to a network and prints interface and connection details.

For more information about Wi-Fi APIs, please visit the [Mbed OS Wi-Fi](https://os.mbed.com/docs/latest/reference/wi-fi.html) documentation.

### Supported hardware ###

* All Mbed OS boards with build-in Wi-Fi module:
    * [u-blox ODIN-W2](https://os.mbed.com/platforms/ublox-EVK-ODIN-W2/)
    * [Realtek RTL8195AM](https://os.mbed.com/platforms/REALTEK-RTL8195AM/)
    * [ST DISCO IOT board](https://os.mbed.com/platforms/ST-Discovery-L475E-IOT01A/) with integrated [ISM43362 WiFi Inventek module](https://github.com/ARMmbed/wifi-ism43362).
    * [ST DISCO_F413ZH board](https://os.mbed.com/platforms/ST-Discovery-F413H/) with integrated [ISM43362 WiFi Inventek module](https://github.com/ARMmbed/wifi-ism43362).
    * [Advantech WISE-150](https://os.mbed.com/modules/advantech-wise-1530/)
    * USI WM-BN-BM-22
    * MxChip EMW3166
* Boards with external WiFi shields.
    * [NUCLEO-F429ZI](https://os.mbed.com/platforms/ST-Nucleo-F429ZI/) with ESP8266-01 module using pins D1 and D0.

##  Getting started ##

1. Import the example.

   ```
   mbed import mbed-os-example-wifi
   cd mbed-os-example-wifi
   ```

1. Configure the Wi-Fi shield and settings.
   Edit ```mbed_app.json``` to include the correct Wi-Fi shield, SSID and password:

```json
{
    "config": {
        "wifi-ssid": {
            "help": "WiFi SSID",
            "value": "\"SSID\""
        },
        "wifi-password": {
            "help": "WiFi Password",
            "value": "\"PASSWORD\""
        }
    },
    "target_overrides": {
        "*": {
            "platform.stdio-convert-newlines": true,
            "esp8266.provide-default" : false
        }
    }
}
```

   For build-in WiFi, you do not need to set any `provide-default` values. Those are required
   if you use external WiFi shield.

   Sample ```mbed_app.json``` files are provided for ESP8266 (```mbed_app_esp8266.json```), X-NUCLEO-IDW04A1 (```mbed_app_idw04a1.json```) and X-NUCLEO-IDW01M1 (```mbed_app_idw01m1```).


1. Compile and generate binary.
    For example, for `GCC`:
    ```
    mbed compile -t GCC_ARM -m UBLOX_EVK_ODIN_W2
    ```

1. Open a serial console session with the target platform using the following parameters:
    * **Baud rate:** 9600
    * **Data bits:** 8
    * **Stop bits:** 1
    * **Parity:** None

1. Copy or drag the application `mbed-os-example-wifi.bin` in the folder `mbed-os-example-wifi/BUILD/<TARGET NAME>/<PLATFORM NAME>` onto the target board.

1. The serial console should display a similar output to below, indicating a successful Wi-Fi connection:
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

    Done
    ```

## Troubleshooting

If you have problems, you can review the [documentation](https://os.mbed.com/docs/latest/tutorials/debugging.html) for suggestions on what could be wrong and how to fix it.

### License and contributions

The software is provided under Apache-2.0 license. Contributions to this project are accepted under the same license. Please see contributing.md for more info.

This project contains code from other projects. The original license text is included in those source files. They must comply with our license guide.
