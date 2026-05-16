# Changelog

## 2026-05-14 (v0.9.4 – v0.9.7)

### v0.9.4
- **Weather Entity — Daily**: select any HA weather entity (DWD, OpenWeatherMap, Met.no, …) — fetches daily forecast via `weather.get_forecasts`; combines actual rainfall + expected precipitation for the skip decision
- **Temperature-based duration scaling**: when forecast temperature exceeds a configurable threshold, irrigation duration is multiplied by a configurable factor (e.g. 1.5× at >30 °C); effective duration written to `last_run_helper`
- All new weather features are fully optional — existing setups with only precipitation/probability sensors are unaffected

### v0.9.5
- **Weather Entity — Hourly**: optional second weather entity with hourly forecasts (e.g. DWD measurement station) — sums precipitation for today; replaces the daily forecast precipitation in the combined rain check

### v0.9.6
- **Forecast Window**: replaces today-only sum with a configurable look-ahead window of 6–72 h from now (default 24 h); directly answers *"will it rain enough before the next watering?"* — set to match your watering interval

### v0.9.7
- **Skip notifications**: default changed from on → off; notifications are now opt-in, Logbook logging always happens regardless
- **Override — Multiple Slots**: new optional `override_schedule` input accepts a second Schedule helper with any number of slots, each bypassing all skip conditions — sits alongside the existing single fixed-time override as an alternative

### Project & Infrastructure (v0.9.7)
- **CI / GitHub Actions**: `.github/workflows/validate.yaml` validates YAML syntax on every push and pull request; handles HA-specific `!input` tags correctly
- **Blueprint Validation badge**: CI status badge in README links directly to the workflow run
- **HA Version badge**: documents minimum supported HA version (2024.6+)
- **My Home Assistant import badge**: one-click blueprint import button at the top of the README
- **HACS removed**: HACS is intended for integrations, not blueprints; replaced with standard Blueprint Exchange workflow
- **README restructured**: features grouped into 5 sections (Weather Intelligence, Scheduling, Skip Conditions, Notifications, Additional Features); setup guide UI-first with YAML as alternative; weather integration reference table

### Inspiration & credit

Weather integration inspired by a brilliant community solution — thank you for sharing it openly. 🌱
https://community.simon42.com/t/wetterdaten-rasensprenger-benoetige-hilfe/28167

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
