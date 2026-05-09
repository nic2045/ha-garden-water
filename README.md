# ha-garden-water

Home Assistant Blueprints und Helpers für die smarte Gartenbewässerung.

## Struktur

```
blueprints/
  gartenbewasserung.yaml    # Haupt-Blueprint
helpers/
  garten_helper.yaml        # Input Helpers für configuration.yaml
```

## Blueprint installieren

In Home Assistant:
1. Einstellungen → Automationen → Blueprints → Blueprint importieren
2. URL eingeben:

```
https://raw.githubusercontent.com/nic2045/ha-garden-water/main/blueprints/gartenbewasserung.yaml
```

## Helper einrichten

Inhalt von `helpers/garten_helper.yaml` in deine `configuration.yaml` einfügen:

```yaml
input_boolean:
  garten_urlaub:
    name: Garten Urlaubsmodus
    icon: mdi:palm-tree
```

Danach HA neu starten.

## Features

- Morgen- und Abendbewässerung (Sonnenuntergang + Offset)
- DWD Wetterintegration (Regenmenge + Wahrscheinlichkeit)
- Urlaubsmodus (input_boolean)
- Optionaler Bewegungssensor mit Debounce
- Alle Parameter per UI einstellbar
- Mehrere Zonen via mehrere Automationen aus demselben Blueprint

## Voraussetzungen

- [DWD Weather Integration (FL550)](https://github.com/FL550/dwd_weather) via HACS
- SONOFF SWV Zigbee Wasserventil via ZHA
