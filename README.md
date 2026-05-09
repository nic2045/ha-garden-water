# ha-garden-water

Home Assistant blueprints and helpers for smart garden irrigation.

## Structure

```
gartenbewasserung.yaml    # Main blueprint
garten_helper.yaml        # Input helpers for configuration.yaml
```

## Install blueprint

In Home Assistant:
1. Settings → Automations → Blueprints → Import blueprint
2. Enter URL:

```
https://raw.githubusercontent.com/nic2045/ha-garden-water/main/gartenbewasserung.yaml
```

## Set up helpers

Add the contents of `garten_helper.yaml` to your `configuration.yaml`:

```yaml
input_boolean:
  garten_urlaub:
    name: Garten Urlaubsmodus
    icon: mdi:palm-tree
```

Then restart HA.

## Features

- Morning and evening irrigation (sunset + configurable offset)
- DWD weather integration (rainfall amount + probability)
- Vacation mode (input_boolean)
- Optional motion sensor with debounce
- All parameters configurable via UI
- Multiple zones via multiple automations from the same blueprint

## Requirements

- [DWD Weather Integration (FL550)](https://github.com/FL550/dwd_weather) via HACS
- SONOFF SWV Zigbee water valve via ZHA
- Home Assistant 2026.1.0 or newer
