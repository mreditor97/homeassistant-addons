# Home Assistant Add-on: Red Reactor Battery Monitor

Automatically control your Red Reactor Battery Monitor from within Home Assistant via MQTT.

[![Release][release-shield]][release]
![Supports aarch64 Architecture][aarch64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports i386 Architecture][i386-shield]

## About

This add-on uses I2C to read the state of your Red Reactor Battery Monitor and displays the read details within Home
Assistant. The data is published to your Home Assistant instance via MQTT.

The [Red Reactor][redreactor] can be purchased to help protect your Raspberry Pi from power outages.


[release-shield]: https://img.shields.io/badge/version-v0.1.4-blue.svg
[release]: https://github.com/mreditor97/addon-redreactor/tree/0.1.4
[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-no-red.svg
[i386-shield]: https://img.shields.io/badge/i386-no-red.svg
[redreactor]: https://www.theredreactor.com/