# ha-garden-water

Home Assistant blueprints and helpers for smart garden irrigation.

## Structure

```
garden_irrigation.yaml    # Main blueprint
garden_helper.yaml        # Optional: vacation mode helper
```

## Install blueprint

In Home Assistant:
1. Settings → Automations → Blueprints → Import blueprint
2. Enter URL:

```
https://raw.githubusercontent.com/nic2045/ha-garden-water/main/garden_irrigation.yaml
```

## Set up helpers

**Required — Schedule helper:**
1. Settings → Helpers → Create helper → Schedule
2. Configure irrigation days and times (any combination, any number of slots)
3. Select it in the blueprint as "Bewässerungsplan"

**Optional — Vacation mode:**
Add the contents of `garden_helper.yaml` to your `configuration.yaml` and restart HA:

```yaml
input_boolean:
  garten_urlaub:
    name: Garden Vacation Mode
    icon: mdi:palm-tree
```

## Features

- Flexible scheduling via HA Schedule helper (any days, any number of times per day)
- Weather-based skip logic (rainfall amount + probability) — optional
- **Weather entity support**: point your HA weather entity (DWD, OpenWeatherMap, Met.no, …) at the blueprint — it fetches the daily forecast and combines actual + expected rain for a smarter skip decision
- **Temperature-based duration scaling**: irrigate longer on hot days — configurable threshold and multiplier
- Vacation mode (input_boolean) — optional
- Motion sensor with debounce — optional
- All parameters configurable via UI
- Multiple zones via multiple automations from the same blueprint

## Requirements

- Home Assistant 2024.6.0 or newer
- A Schedule helper (Settings → Helpers → Schedule)
- Any weather integration with precipitation and probability sensors (optional)
  - e.g. [DWD Weather (FL550)](https://github.com/FL550/dwd_weather), OpenWeatherMap, Met.no
- SONOFF SWV Zigbee water valve via ZHA
