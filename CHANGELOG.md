# Changelog

## [Unreleased] - 2026-05-09

### Added
- `min_ha_version: "2026.1.0"` requirement in blueprint metadata
- `.vscode/settings.json` with `yaml.customTags` to suppress false `!input` errors in VS Code

### Changed
- `abend_offset` input: switched from `number` (minutes) to `text` selector with `HH:MM:SS` format to correctly pass a timedelta string to the sun trigger `offset` field
- `bewegungssensor` default: changed from `{}` to `""` — empty dict is not a valid default for an entity selector
- All blueprint and input descriptions translated to English; UI labels (input `name` fields) remain in German
- Blueprint `name` and `description` translated to English

### Fixed
- Sun trigger `offset: !input abend_offset` now receives a valid timedelta string instead of an integer
- Motion sensor check in template updated from `!= {}` to `!= ''` to match new default
- `wait_template` replaced with `wait_for_trigger` (deprecated since HA 2022.9)
