# Home Assistant App: Red Reactor Battery Monitor

Automatically control your Red Reactor Battery Monitor from within Home Assistant via MQTT.

[![Release][release-shield]][release]
![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]

## About

This app uses I2C to read the state of your Red Reactor Battery Monitor and displays the read details within Home
Assistant. The data is published to your Home Assistant instance via MQTT.

The [Red Reactor][redreactor] can be purchased to help protect your Raspberry Pi from power outages.

[release-shield]: https://img.shields.io/badge/version-v0.1.6-blue.svg
[release]: https://github.com/mreditor97/app-redreactor/tree/0.1.6
[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-no-red.svg
[redreactor]: https://www.theredreactor.com/