# `esp_wifi_80211_tx` sample code
<img src="rickroll.png" alt="Rickrolling with WiFi Networks" width="400px"/>

## Introduction
Sending arbitrary IEEE 802.11 frames can be useful in various ways, e.g. for mesh networking, [unidirectional long-distance communication](https://www.youtube.com/watch?v=tBfa4yk5TdU) or low-overhead data transmission. It can, however, be abused for spamming large numbers of invalid SSIDs, jamming WiFi networks or sending deauthentication frames in order to sniff SSIDs of hidden wireless networks. Please be advised that such usage is morally doubtful at best and illegal at worst. Use this at your own risk.

Espressif have now created the `esp_wifi_80211_tx` API, making [esp32free80211](https://github.com/Jeija/esp32free80211) obsolete. The new function is thoroughly documented **[in the API guide](https://github.com/espressif/esp-idf/blob/master/docs/en/api-guides/wifi.rst#wi-fi-80211-packet-send)**. Since at the time of writing not a lot of sample code using `esp_wifi_80211_tx` exists and many developers wanting to send arbitrary data with their ESP32s end up using [esp32free80211](https://github.com/Jeija/esp32free80211) with an outdated [esp-idf](https://github.com/espressif/esp-idf) version, I want to hereby provide some more up-to-date sample code for `esp_wifi_80211_tx`.

## Project Description
In order to demonstrate the freedom output functionality, this software broadcasts the infamous lines from Rick Astley's `Never gonna give you up`. This is achieved by manually assembling IEEE 802.11 beacon frames in `main.c` and broadcasting them via the currently unofficial `esp_wifi_80211_tx` API in Espressif's [esp32-wifi-lib](https://github.com/espressif/esp32-wifi-lib).

If you want to use raw packet sending functionality in your own project, just declare the `esp_wifi_80211_tx` function like this:
```C
// buffer: Raw IEEE 802.11 packet to send
// len: Length of IEEE 802.11 packet
// en_sys_seq: see https://github.com/espressif/esp-idf/blob/master/docs/api-guides/wifi.rst#wi-fi-80211-packet-send for details
esp_err_t esp_wifi_80211_tx(wifi_interface_t ifx, const void *buffer, int len, bool en_sys_seq);
```

### Compile / Flash
This project uses the [Espressif IoT Development Framework](https://github.com/espressif/esp-idf). With the ESP-IDF installed, execute
```
make menuconfig
```
and configure the SDK to use your preferred settings (baudrate, python2 executable, serial flasher port, …) and proceed to compile and flash this project using
```
make flash
```

## Project License: MIT
```
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
