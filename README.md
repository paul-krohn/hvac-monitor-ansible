# HVAC Monitor Role

Ansible role to deploy and configure the HVAC monitoring stack, including:
- Zigbee2MQTT for Zigbee device communication
- MQTT broker (Mosquitto) for message brokering
- mqtt2prometheus for converting MQTT metrics to Prometheus format

## Requirements

- Debian/Ubuntu-based system
- Zigbee adapter connected to the system (typically at `/dev/ttyUSB0`)
- MQTT broker configuration (default: localhost:1883)

## Role Variables

See `defaults/main.yaml` for all available configuration options.

Key variables:
- `hvac_monitor.service_user`: User to run services as (default: paul)
- `hvac_monitor.zigbee.serial_port`: Path to Zigbee adapter (default: /dev/ttyUSB0)
- `hvac_monitor.mqtt`: MQTT broker connection details
- `hvac_monitor.rooms`: List of rooms with Zigbee sensors

## Usage

```yaml
- hosts: hvac_monitors
  roles:
    - paul-krohn.hvac-monitor
```

Override defaults as needed in host_vars or group_vars.

## Post-Installation

After deployment:
1. Pair Zigbee sensors with the adapter
2. Map sensors in the Homebridge MQTT plugin configuration
3. Monitor metrics at `http://<host>:9641/metrics`
