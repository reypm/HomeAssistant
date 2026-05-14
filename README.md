# Home Assistant Configuration

![Config Check](https://github.com/reypm/HomeAssistant/actions/workflows/config-check.yaml/badge.svg)

Personal Home Assistant configuration repository. This is the root of my HA installation, covering a multi-room household with smart devices, energy monitoring, camera streaming, pool heater control, and a Mushroom-based dashboard.

---

## Hardware & Infrastructure

- **Home Assistant OS** running on dedicated hardware
- **MariaDB** for recorder persistence (10-day retention)
- **Node-RED** for complex automations
- **go2rtc** (v1.9.9) for WebRTC camera streaming
- **RTL433** for software-defined radio RF sensors
- **Scrypted** as the video streaming backend

---

## Repository Structure

```
.
├── configuration.yaml        # Main HA configuration entry point
├── secrets.fake.yaml         # Placeholder secrets for reference
├── go2rtc.yaml               # WebRTC streaming config
├── custom_components/        # Manually managed custom integrations
├── dashboards/               # Lovelace dashboard definitions (Mushroom)
│   └── mushroom/views/       # Per-room dashboard views
├── includes/                 # Split configuration files
│   ├── automation/           # Automations
│   ├── inputs/               # Input booleans and numbers
│   ├── scene/                # Scenes
│   ├── script/               # Scripts
│   ├── sensor/               # Sensors
│   └── templates/            # Template sensors
├── pymyq/                    # MyQ garage door library
├── rtl_433/                  # RTL433 SDR config
└── www/                      # Frontend web resources (community cards)
```

---

## Custom Integrations

Integrations managed manually under `custom_components/`:

| Integration | Version | Purpose |
|---|---|---|
| [Orbit B-hyve](https://github.com/sebr/bhyve-home-assistant) | 4.1.1 | Smart irrigation control |
| [Dreo](https://github.com/JeffSteinbok/hass-dreo) | 1.8.4 | Dreo smart fans and appliances |
| [Energy Meter](https://github.com/zeronounours/HA-custom-component-energy-meter) | — | Energy consumption tracking |
| [HACS](https://hacs.xyz) | — | Community store manager |
| [Hubspace](https://github.com/jdeath/Hubspace-Homeassistant) | 6.0.0 | Hubspace smart devices |
| [Node-RED Companion](https://github.com/zachowj/hass-node-red) | — | Node-RED ↔ HA bridge |
| [Scrypted](https://github.com/koush/scrypted) | — | Video platform integration |
| [SmartThinQ LGE Sensors](https://github.com/ollo69/ha-smartthinq-sensors) | — | LG washer/dryer sensors |
| [Sonoff LAN](https://github.com/AlexxIT/SonoffLAN) | 3.11.1 | Local Sonoff device control |
| [Tapo: Cameras Control](https://github.com/JurajNyiri/HomeAssistant-Tapo-Control) | — | TP-Link Tapo cameras |
| [WebRTC Camera](https://github.com/AlexxIT/WebRTC) | — | WebRTC camera streaming |

---

## HACS Frontend Resources

Lovelace cards and plugins under `www/community/`:

| Card | Purpose |
|---|---|
| [lovelace-auto-entities](https://github.com/thomasloven/lovelace-auto-entities) | Dynamic entity lists |
| [lovelace-card-mod](https://github.com/thomasloven/lovelace-card-mod) | CSS customization for cards |
| [lovelace-layout-card](https://github.com/thomasloven/lovelace-layout-card) | Custom dashboard layouts |
| [lovelace-mushroom](https://github.com/piitaya/lovelace-mushroom) | Mushroom card collection |
| [mini-graph-card](https://github.com/kalkih/mini-graph-card) | Compact history graphs |
| [mini-media-player](https://github.com/kalkih/mini-media-player) | Compact media player card |
| [stack-in-card](https://github.com/custom-cards/stack-in-card) | Stack cards inside a single card |
| [timer-bar-card](https://github.com/rianadon/timer-bar-card) | Visual timer progress bars |
| [vertical-stack-in-card](https://github.com/ofekashery/vertical-stack-in-card) | Vertical card stacking |
| [weather-card](https://github.com/bramkragten/weather-card) | Weather display card |
| [weather-chart-card](https://github.com/mlamberts78/weather-chart-card) | Weather forecast chart |

---

## Dashboard

Uses a **Mushroom** themed dashboard organized by area:

| View | Area |
|---|---|
| 1.1 | Home — overview |
| 1.2 | Office |
| 1.3 | Master bedroom |
| 1.4 | Kid's room |
| 1.5 | Living room |
| 1.6 | Kitchen |
| 1.8 | Laundry |
| 1.9 | Cameras |
| 1.10 | Patio |

---

## Key Features

### Energy & Water Monitoring

Utility meters track consumption in hourly, daily, and monthly cycles for both electricity and water. Source sensors: `water_meter_reading` and `electricity_meter`.

### Pool Heater Control (Raypak)

Full monitoring and control of a Raypak pool heater via the Raymote REST API (30-second polling):

- Inlet/outlet/coil/air temperatures
- Heater status, setpoint, BTU rating
- Estimated heat-up time and lifetime heat hours
- Estimated flow (GPH) and RSSI signal
- On/off control and setpoint adjustment via REST commands
- Generic thermostat entity (50–104°F range, 80°F default)

### Camera Streaming

Tapo and Ring cameras streamed via WebRTC using go2rtc as the relay server.

### Garage Door

MyQ garage door integration via the bundled `pymyq` library.

### RF Sensors

RTL433 SDR configured to receive 433 MHz RF sensor data.

---

## CI

GitHub Actions runs a configuration validation check on every push and pull request using [`frenck/action-home-assistant`](https://github.com/frenck/action-home-assistant) against the stable HA release.

---

## Secrets

Sensitive values are kept out of version control. Use `secrets.fake.yaml` as a reference for the required keys:

- Home coordinates
- Internal and external URLs
- Device MAC addresses (LG TV, FireTV, AppleTV)
- Camera stream URLs (Tapo, Ring)
- Telegram bot token and chat ID
- MariaDB connection string
- Raypak API endpoints
