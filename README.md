# ha-garden-water

![HA Version](https://img.shields.io/badge/Home%20Assistant-2024.6%2B-blue?logo=homeassistant)
[![Blueprint Validation](https://github.com/nic2045/ha-garden-water/actions/workflows/validate.yaml/badge.svg)](https://github.com/nic2045/ha-garden-water/actions/workflows/validate.yaml)

Home Assistant blueprint for smart, weather-aware garden irrigation.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fnic2045%2Fha-garden-water%2Fmain%2Fgarden_irrigation.yaml)

## Features

### 🌦️ Weather Intelligence
- **Daily weather entity** — fetches forecast via `weather.get_forecasts`; combines expected + actual precipitation for the skip decision
- **Hourly weather entity** — sums precipitation over a configurable window (6–72 h) from now; answers *"will it rain enough before the next watering is due?"*
- **Temperature-based duration scaling** — irrigate longer on hot days; configurable threshold and multiplier
- **Precipitation & probability sensors** — alternative to weather entities; any HA sensor works

### 📅 Scheduling
- **Schedule helper** — any days, any number of time slots per day; configured entirely in the HA UI
- **Sun-based triggers** — trigger relative to sunset or sunrise with configurable offset
- **Override time** — fixed daily time that always runs, bypassing all skip conditions

### 💧 Skip Conditions
- **Weather skip** — skip when rainfall + forecast exceeds your threshold
- **Skip if already watered** — suppresses re-irrigation within a configurable time window
- **Vacation mode** — one toggle suppresses all irrigation while away

### 🔔 Monitoring
- **Skip notifications** — every skipped run is logged to the HA Logbook with the reason; optional push notification to HA app, mobile (iOS/Android), or Alexa
- **Motion sensor pause** — pauses the valve mid-run when motion is detected; resumes automatically after the area clears

### 🏡 Multi-zone
- One blueprint, one automation per valve — independent settings per zone

---

## Requirements

### Valve
Any switch or water valve entity — no specific hardware required.

### Schedule helper (required)
**Via UI:** Settings → Helpers → Add helper → Schedule

Configure irrigation days and times directly in the UI — no YAML needed.

### Weather entity (optional)
Any HA weather integration works. Recommended:

| Integration | Type | Install |
|---|---|---|
| **Met.no** | Daily forecast | Built-in — Settings → Devices & Services → Add → Met.no |
| **DWD Weather** | Hourly (measurement station) | HACS → [DWD Weather (FL550)](https://github.com/FL550/dwd_weather) |
| OpenWeatherMap | Daily forecast | Built-in |

### Vacation mode helper (optional)
**Via UI:** Settings → Helpers → Add helper → Toggle — name it e.g. *Garden Vacation Mode*

**Via config** (`configuration.yaml`):
```yaml
input_boolean:
  garten_urlaub:
    name: Garden Vacation Mode
    icon: mdi:palm-tree
```

### Last run duration helper (optional, for "skip if already watered")
**Via UI:** Settings → Helpers → Add helper → Number — set unit to `min`, range 0–120

---

## Install

**Manually:** Settings → Automations → Blueprints → Import blueprint → paste URL:
```
https://raw.githubusercontent.com/nic2045/ha-garden-water/main/garden_irrigation.yaml
```

---

## Weather integration details

| Input | What it does |
|---|---|
| Precipitation sensor | Any sensor reporting today's accumulated rainfall in mm |
| Rain probability sensor | Any sensor reporting precipitation probability in % |
| **Weather Entity — Daily** | Fetches daily forecast; combines actual + expected rain for skip decision; also drives temperature scaling |
| **↳ Weather Entity — Hourly** | Fetches hourly forecast; sums precipitation over the forecast window |
| **↳ Forecast Window** | Hours to look ahead (default 24 h — set to match your watering interval) |

**Inspiration:** [simon42.com community](https://community.simon42.com/t/wetterdaten-rasensprenger-benoetige-hilfe/28167)
