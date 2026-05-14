# Changelog

## 2026-05-14 (v0.9.4 – v0.9.6)

### Features
- **Weather Entity — Daily**: select any HA weather entity (DWD, OpenWeatherMap, Met.no, …) — fetches daily forecast via `weather.get_forecasts`; combines actual rainfall + expected precipitation for the skip decision
- **Weather Entity — Hourly + Forecast Window**: optional second weather entity with hourly forecasts (e.g. DWD measurement station) — sums precipitation over a configurable window of 6–72 h from now (default 24 h); replaces the daily forecast component when set; answers "will it rain enough before the next watering is due?"
- **Temperature-based duration scaling**: when forecast temperature exceeds a configurable threshold, irrigation duration is multiplied by a configurable factor (e.g. 1.5× at >30 °C); effective duration written to `last_run_helper`
- All new weather features are fully optional — existing setups with only precipitation/probability sensors are unaffected

### Inspiration & credit

This entire weather integration was inspired by a brilliant community solution shared in the
[simon42.com forum](https://community.simon42.com/t/wetterdaten-rasensprenger-benoetige-hilfe/28167/6).
The author had already built a sophisticated multi-condition automation that combined actual
rainfall, temperature tiers, days since last watering, and `weather.get_forecasts` — long before
this blueprint supported any of it. A big thank you for sharing that work openly: it directly
shaped what v0.9.4–v0.9.6 became. Great thinking, great execution. 🌱

---

## 2026-05-10

### Features
- **Skip notifications**: skipped runs are always logged to HA Logbook with reason; optional push notification to HA, mobile app, or Alexa (toggle + free-text service target)
- **Skip if Already Watered**: skips if valve ran within configurable time window; optional `input_number` helper tracks blueprint-controlled run duration
- **Sun-based triggers**: trigger irrigation relative to sunset or sunrise with configurable offset (select)
- **Override time**: fixed daily time that bypasses all skip conditions
- **UI reorganization**: sections reduced from 9 → 6, reordered essential → nice-to-have; dependent inputs marked with `↳` prefix

### Fixed
- Motion pause: replaced `wait_for_trigger` with `wait_template` — entity ID templates are not resolved at config load time
- `last_run_helper` entity_id: use template instead of `!input` to avoid validation error when empty
- Valve selector: added `device_class: water` filter to the `valve` domain

### Changed
- Build number format: `YYMMDD.HHMM` (e.g. `260509.2331`) — date + time, unique per build
- Skip logic moved from `condition:` block into action `if/else` to enable per-reason notifications

---

## 2026-05-09

### Added
- Blueprint version string in description: `v0.9.0 (build 260509)`
- `.vscode/settings.json`: suppresses false `!input` YAML errors in VS Code
- `.gitignore`
- `CHANGELOG.md`

### Features
- **Schedule helper**: replaced custom time logic with HA Schedule entity — supports any number of slots per day, any weekday combination, configurable in HA UI
- **Optional weather sensors**: precipitation and rain probability sensors are now optional (leave empty to always irrigate)
- **Optional vacation mode**: `input_boolean` is optional
- **UI sections**: all inputs grouped into logical collapsible sections (Schedule, Weather, Vacation, Motion)
- **Multi-domain valve selector**: accepts both `switch` and `valve` entities from any manufacturer
- **Generic weather support**: removed DWD-specific filters — any integration with precipitation/probability sensors works

### Fixed
- Removed `min_ha_version` (invalid field) — correct field is `homeassistant.min_version`
- Removed `device_class` filter from precipitation sensor — DWD does not set it
- Removed colon from sensor descriptions to prevent YAML parse error on import
- Motion sensor default changed from `{}` to `""` — empty dict is not valid for entity selector

### Changed
- All files renamed to English (`gartenbewasserung.yaml` → `garden_irrigation.yaml`)
- All variable and input names translated to English
- All UI labels translated to English
- Blueprint description reformatted with emojis, collapsible feature list, README link
- Blueprint name: `Automated Garden Irrigation`
- `homeassistant.min_version: "2024.6.0"` (2 years support policy)
