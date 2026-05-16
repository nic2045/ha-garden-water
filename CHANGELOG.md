# Changelog

## [0.10.0](https://github.com/nic2045/ha-garden-water/compare/v0.9.7...v0.10.0) (2026-05-16)


### Features

* add HACS support, HA version badge, and HACS validation CI ([07144f7](https://github.com/nic2045/ha-garden-water/commit/07144f752c106395d5278c4ab492ea575ec7a5a6))
* add hourly weather entity for today's precipitation sum ([baa2f9b](https://github.com/nic2045/ha-garden-water/commit/baa2f9baa5d6219a4e3681f1059866636908540c))
* add Skip if Already Watered feature ([c59ae95](https://github.com/nic2045/ha-garden-water/commit/c59ae95daa3009b24ea343eb97724b7774ec4bda))
* add skip logging and optional notifications ([a4c4b80](https://github.com/nic2045/ha-garden-water/commit/a4c4b80eeda447543444baab8d18a1cbf14a39c8))
* add sun-based schedule section with sunset/sunrise offset controls ([148c432](https://github.com/nic2045/ha-garden-water/commit/148c432204f8746b75c5c7905dc3dcb7f758a6ee))
* add weather entity support with combined rain forecast and temperature-based duration scaling ([0fde9a7](https://github.com/nic2045/ha-garden-water/commit/0fde9a7cd89976ee34ac28e8400e66f2d4e02735)), closes [#2](https://github.com/nic2045/ha-garden-water/issues/2)
* filter DWD sensor selectors by integration ([a47446d](https://github.com/nic2045/ha-garden-water/commit/a47446df38c7ee66384834d6d67bfed0562622f2))
* group all inputs into logical UI sections ([0afd23c](https://github.com/nic2045/ha-garden-water/commit/0afd23c46eba16297901677cdf4ae953b5bd78b3))
* group motion sensor and debounce into collapsible UI section ([a15d24f](https://github.com/nic2045/ha-garden-water/commit/a15d24f92fd890f0309f39384bceb1fe89145a6c))
* make vacation_boolean optional ([1d8cb18](https://github.com/nic2045/ha-garden-water/commit/1d8cb18e7d90e95f1342f6e70ab5e9eee6852f20))
* make weather sensors optional ([0968965](https://github.com/nic2045/ha-garden-water/commit/096896594ff2befcb57a0b3953dc863d4aba2c22))
* notify why irrigation was skipped ([8cec56d](https://github.com/nic2045/ha-garden-water/commit/8cec56d354162e495d0e41677988ecbb90042d22))
* rename all variables/inputs to English, add homeassistant.min_version 2024.5.0 ([196ca4a](https://github.com/nic2045/ha-garden-water/commit/196ca4a6e4c8d68be0f19e29cd99f9a143ecbac1))
* replace custom time logic with HA Schedule helper ([254d455](https://github.com/nic2045/ha-garden-water/commit/254d4550f70f1003815f3f560b04330a2b8116a5))
* replace override_time with override_schedule (any number of slots) ([a5ea405](https://github.com/nic2045/ha-garden-water/commit/a5ea40590dfd51bb3755714a4420ad7510ff234e))
* replace today-only hourly sum with configurable forecast window ([aba7190](https://github.com/nic2045/ha-garden-water/commit/aba719007a26d94015c81c9fe7a15c2700ca6614)), closes [#3](https://github.com/nic2045/ha-garden-water/issues/3)
* support any weather integration via device_class filter ([21ce875](https://github.com/nic2045/ha-garden-water/commit/21ce87556789c8b9c950a262f9f6a07e4cb996c0))
* support both override schedule and override fixed time ([41708d6](https://github.com/nic2045/ha-garden-water/commit/41708d6a59fb20baf7a856e7d7cfedb5ba05ba56))
* weather entity support, forecast window, temperature scaling, override schedule ([9140be0](https://github.com/nic2045/ha-garden-water/commit/9140be0ebd0b7c9e59a4666031e330f670b55f49))
* weather forecast integration (daily + hourly + temperature scaling) ([e7e8368](https://github.com/nic2045/ha-garden-water/commit/e7e836865da7dc79ab5a5b630b1fe5eb47e2b77c))


### Bug Fixes

* accept both switch and valve domains for irrigation valve input ([c0b9522](https://github.com/nic2045/ha-garden-water/commit/c0b9522f8966cc67996b66f497c0d6954763a725))
* default skip notifications to off ([b8b19bc](https://github.com/nic2045/ha-garden-water/commit/b8b19bc1657ce6c86c75e459f42c3f1615af63f2))
* move logbook.log entity_id from target to data ([994a6c1](https://github.com/nic2045/ha-garden-water/commit/994a6c176a03b7522413ad4059279857b508539f))
* quote description containing colon to prevent YAML parse error ([e825d75](https://github.com/nic2045/ha-garden-water/commit/e825d7556c1db3cc3f392497d836b4f1e08186dd))
* remove colon from precipitation sensor description ([5655d59](https://github.com/nic2045/ha-garden-water/commit/5655d596d3df75cc68a28bdead34fcbb6f3ed912))
* remove device_class filter from precipitation sensor — DWD does not set it ([c37c7d6](https://github.com/nic2045/ha-garden-water/commit/c37c7d6e8d2340d7f8f695a2deba358f16c3691c))
* remove min_ha_version field not supported by current HA version ([7225bb4](https://github.com/nic2045/ha-garden-water/commit/7225bb4b3852438f4ebaef447c3cfc5b0a0d8319))
* rename workflow to validate.yaml, fix !input tag handling, move badge up ([5634d54](https://github.com/nic2045/ha-garden-water/commit/5634d5423fec47cbff73cdac7b95c93362cf26a1))
* replace hacs/action with YAML validation (blueprint category unsupported) ([420cb4a](https://github.com/nic2045/ha-garden-water/commit/420cb4a33b1d98d2074cb24efc9fe765cb878a53))
* simplify hacs.json to standard blueprint fields ([add11b2](https://github.com/nic2045/ha-garden-water/commit/add11b295b44e608bcd19054e9756a3eb5ebcd48))
* use template for last_run_helper entity_id to avoid validation error when empty ([fe44890](https://github.com/nic2045/ha-garden-water/commit/fe44890a31ee0a5d99e6a8de0795c04b1e0fd9e9))
* use template for logbook.log entity_id to avoid list type error ([cdc795f](https://github.com/nic2045/ha-garden-water/commit/cdc795fea3bb249da5b8d9dd13b73652f8a9a793))

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
