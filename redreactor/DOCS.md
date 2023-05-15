# Home Assistant Add-on: Red Reactor Battery Monitor

## Installation

Follow these steps to get the add-on installed on your system:

1. Navigate in your Home Assistant front-end to **Supervisor** -> **Add-on Store**.
2. Find the "Red Reactor Battery Monitor" add-on and click it.
3. Click on the "INSTALL" button.

## How to use

The add-on has a couple of things that must be configured to get the add-on running as desired:

1. Configure the MQTT settings.
2. Update add-on settings to suit your needs.
3. Start the add-on.
4. Check the add-on log output to see the result.
5. If MQTT Auto Discovery is enabled, the Red Reactor should appear within your Device list

## Configuration

Add-on configuration:

```yaml
mqtt:
  broker: core-mosquitto # IP Address of your MQTT Broker
  port: 1883 # Port of your MQTT Broker
  user: redreactor # Username for your MQTT Broker
  password: redreactor # Password for your MQTT Broker
hostname:
  name: redreactor-pi # Hostname (used as a MQTT topic identifier)
  pretty: Raspberry Pi # Pretty Display Name
homeassistant:
  discovery_interval: 120 # Home Assistant Configuration discovery push interval
  expire_after: 120 # Home Assistant MQTT Data expiry time
system:
  shutdown: ha host shutdown # Shutdown (if using HASS OS, this doesn't need changing)
  restart: ha host restart # Restart (if using HASS OS, this doesn't need changing)
logging:
  console: INFO
  file: WARNING
```

Other configuration options are available from within the Home Assistant Device configuration page. Including the ability to change the `report_interval` to Home Assistant.

## OS Specific I2C configuration

_Depending on the operating system you are using, the configuration may differ as below._

### Home Assistant OS

When using the Home Assistant OS, you must enable I2C. This can be enabled by following the steps from within this [Home Assistant guide](https://www.home-assistant.io/common-tasks/os/#enable-i2c).

_The default configuration for this OS is for UART to be disabled - for the Red Reactor to power your Raspberry Pi, it must be enabled. This is due to the Red Reactor requiring UART assertion. It can be found at the same time as configuring the I2C settings, within the `hassos-boot` partition in `config.txt`. Enable it by adding `enable_uart=1` to the `config.txt`_

### Ubuntu

When using a standard operating system, I2C usually comes enabled. Meaning there is no additional configuration to get the Red Reactor working. If it is not enabled it can be done by ensuring the parameter `dtparam=i2c_arm=on` is contained within `/boot/config.txt` file.
