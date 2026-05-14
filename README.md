# ha-garden-water

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://github.com/hacs/integration)
![HA Version](https://img.shields.io/badge/Home%20Assistant-2024.6%2B-blue?logo=homeassistant)
[![HACS Validation](https://github.com/nic2045/ha-garden-water/actions/workflows/hacs.yaml/badge.svg)](https://github.com/nic2045/ha-garden-water/actions/workflows/hacs.yaml)

Home Assistant blueprints and helpers for smart garden irrigation.

## Structure

```
garden_irrigation.yaml    # Main blueprint
garden_helper.yaml        # Optional: vacation mode helper
```

## Install blueprint

**Via HACS (recommended):**
1. HACS → Blueprints → ⋮ → Custom repositories
2. Add `https://github.com/nic2045/ha-garden-water` — category: **Blueprint**
3. Download the blueprint from HACS — updates are notified automatically

**One-click import:**

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fnic2045%2Fha-garden-water%2Fmain%2Fgarden_irrigation.yaml)

**Manually:** Settings → Automations → Blueprints → Import blueprint → paste URL:

```
https://raw.githubusercontent.com/nic2045/ha-garden-water/main/garden_irrigation.yaml
```

## Set up helpers

**Required — Schedule helper:**
1. Settings → Helpers → Create helper → Schedule
2. Configure irrigation days and times (any combination, any number of slots)
3. Select it in the blueprint as the irrigation schedule

**Optional — Vacation mode:**
Add the contents of `garden_helper.yaml` to your `configuration.yaml` and restart HA:

```yaml
input_boolean:
  garten_urlaub:
    name: Garden Vacation Mode
    icon: mdi:palm-tree
```

## Features

- **Flexible scheduling** via HA Schedule helper — any days, any number of time slots per day
- **Weather-based skip logic** — optional rainfall amount and probability sensors
- **Daily weather entity** (DWD, OpenWeatherMap, Met.no, …) — combines actual + forecast precipitation for a smarter skip decision
- **Hourly weather entity** (e.g. DWD measurement station) — sums precipitation over a configurable forecast window to answer: *"Will it rain enough before the next watering is due?"*
- **Temperature-based duration scaling** — irrigate longer on hot days (configurable threshold and multiplier)
- **Sun-based triggers** — trigger relative to sunset or sunrise with configurable offset
- **Override time** — fixed daily time that bypasses all skip conditions
- **Skip if already watered** — suppresses re-irrigation within a configurable time window
- **Vacation mode** — one toggle suppresses all irrigation while away
- **Motion sensor pause** — pauses the valve mid-run, resumes automatically after the area clears
- **Skip notifications** — every skipped run is logged to the HA Logbook; optional push notification to HA, mobile app, or Alexa
- **Multiple zones** — one blueprint, one automation per valve

## Weather integration

The blueprint supports three levels of weather intelligence, which can be combined:

| Input | What it does |
|---|---|
| Precipitation sensor | Any sensor reporting today's accumulated rainfall in mm |
| Rain probability sensor | Any sensor reporting precipitation probability in % |
| **Weather Entity — Daily** | Fetches daily forecast via `weather.get_forecasts`; combines actual + forecast rain for the skip decision; also used for temperature-based duration scaling |
| **↳ Weather Entity — Hourly** | Fetches hourly forecast; sums precipitation over a configurable window (6–72 h) from now — set to your watering interval |
| **↳ Forecast Window** | How many hours ahead to sum (default 24 h for daily schedules, 48 h for every-other-day) |

**Recommended setup with DWD:**
- Daily: `weather.wettervorhersage_home` (Met.no — built-in, no extra install)
- Hourly: `weather.wetterstation_*` (DWD measurement station via HACS DWD Weather)

## Requirements

- Home Assistant 2024.6.0 or newer
- A Schedule helper (Settings → Helpers → Schedule)
- Any weather integration with precipitation/probability sensors (optional)
  - e.g. [DWD Weather (FL550)](https://github.com/FL550/dwd_weather), OpenWeatherMap, Met.no
- Switch or valve entity for the irrigation valve (any manufacturer)
