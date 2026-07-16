# Sonoff TX Ultimate — Smart Light Version

ESPHome configuration for Sonoff TX Ultimate touch panel with smart lighting effects.

## Features

- **2/3 Relay Support** — configurable via `relay_count` substitution
- **Touch Feedback LED** — color effects for touch, swipe left/right, long press, multi-touch
- **Nightlight Mode** — toggle via HA switch, white 20% ambient light
- **Button LED Mode** — independent control for left/middle/right button LEDs
- **Reverse Switch** — runtime toggle to flip LED layout 180° for different installation orientations

## Forked From

This project is forked from [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome).

**Original project provides:** Base ESPHome firmware for Sonoff TX Ultimate with touch panel, UART communication, and LED control.

**This fork adds:**
- Multi-relay (2/3) touch zone mapping
- Direction-aware LED partitions (normal/reversed)
- Runtime reverse switch for installation flexibility
- Configurable touch feedback colors and effects
- Nightlight mode with HA integration

## Flashing Instructions

> **Important:** Please refer to the original project's flashing guide for initial setup:
>
> 👉 [SmartHome-yourself/sonoff-tx-ultimate-for-esphome — Flashing Guide](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome)

### Quick Start

1. Install [ESPHome](https://esphome.io/guides/installing_esphome.html)
2. Copy `tx-ultimate-smartlight-version.yaml` to your ESPHome config directory
3. Create `secrets.yaml` with your WiFi credentials:
   ```yaml
   wifi_ssid: "YourSSID"
   wifi_password: "YourPassword"
   ```
4. Edit substitutions in the YAML:
   - Set `name` and `friendly_name`
   - Set `relay_count` to match your hardware (1, 2, or 3)
   - Update `api` encryption key and `ota` password
5. Compile and upload via ESPHome dashboard or CLI

## Configuration

### Substitutions

| Parameter | Description | Default |
|-----------|-------------|---------|
| `name` | Device name | `tx-ultimate` |
| `friendly_name` | HA display name | `TX Ultimate` |
| `relay_count` | Number of relays (1/2/3) | `2` |
| `button_color` | Button LED RGB `{R,G,B}` | `{100,77,56}` |
| `nightlight_brightness` | Nightlight brightness (0-1) | `0.2` |
| `touch_color` | Touch feedback RGB | `{100,60,0}` |
| `swipe_left_color` | Swipe left RGB | `{80,80,50}` |
| `swipe_right_color` | Swipe right RGB | `{80,70,10}` |
| `multi_touch_color` | Full touch RGB | `{0,80,40}` |
| `long_press_color` | Long press RGB | `{100,100,100}` |

### HA Switches

After flashing, the following switches appear in Home Assistant:

| Switch | Function |
|--------|----------|
| `{name} L1/L2/L3` | Relay control |
| `{name} Reverse` | Flip LED layout 180° |
| `{name} Nightlight` | Toggle nightlight mode |
| `{name} Button Left/Middle/Right Mode` | Button LED mode |

## License

MIT License — see [LICENSE](LICENSE)

## Acknowledgments

- [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome) — Original ESPHome TX Ultimate project
- [ESPHome](https://esphome.io/) — Firmware framework
