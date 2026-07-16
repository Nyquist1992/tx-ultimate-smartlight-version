# Sonoff TX Ultimate — Smart Light Version

ESPHome configuration for Sonoff TX Ultimate touch panel with smart lighting effects.

---

# Sonoff TX Ultimate — 智慧燈效版

適用於 Sonoff TX Ultimate 觸控面板的 ESPHome 韌體配置，支援多鍵觸控 + LED 燈效。

---

## Features / 功能特色

- **2/3 Relay Support** — configurable via `relay_count` substitution
- **2/3 路繼電器** — 透過 `relay_count` substitution 設定
- **Touch Feedback LED** — color effects for touch, swipe left/right, long press, multi-touch
- **觸控 LED 反饋** — 觸控、左右滑動、長按、全觸各有獨立色效
- **Nightlight Mode** — toggle via HA switch, white 20% ambient light
- **夜燈模式** — 透過 HA 開關切換，白色 20% 氛圍燈
- **Button LED Mode** — independent control for left/middle/right button LEDs
- **按鍵 LED 模式** — 左/中/右按鍵燈獨立控制
- **Reverse Switch** — runtime toggle to flip LED layout 180° for different installation orientations
- **Reverse 開關** — runtime 切換 LED 燈效方向，適配不同安裝方向

---

## Forked From / Fork 來源

This project is forked from [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome).

本專案 fork 自 [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome)。

**Original project provides / 原始專案提供：**
Base ESPHome firmware for Sonoff TX Ultimate with touch panel, UART communication, and LED control.
基礎 ESPHome 韌體，包含 TX Ultimate 觸控面板、UART 通訊、LED 控制。

**This fork adds / 本 Fork 新增：**
- Multi-relay (2/3) touch zone mapping / 多繼電器觸控區域映射
- Direction-aware LED partitions (normal/reversed) / 支援方向感知的 LED 分區（正/反）
- Runtime reverse switch for installation flexibility / Runtime reverse 開關，靈活適配安裝方向
- Configurable touch feedback colors and effects / 可配置的觸控反饋顏色與效果
- Nightlight mode with HA integration / 整合 HA 的夜燈模式

---

## Flashing Instructions / 燒錄說明

> **Important / 重要：** Please refer to the original project's flashing guide for initial setup:
>
> 👉 [SmartHome-yourself/sonoff-tx-ultimate-for-esphome — Flashing Guide](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome)
>
> 首次燒錄請參閱原專案的燒錄指南。

### Quick Start / 快速開始

1. Install [ESPHome](https://esphome.io/guides/installing_esphome.html) / 安裝 ESPHome
2. Copy `tx-ultimate-smartlight-version.yaml` to your ESPHome config directory / 複製 YAML 到 ESPHome 設定目錄
3. Create `secrets.yaml` with your WiFi credentials / 建立 `secrets.yaml` 填入 WiFi 密碼：
   ```yaml
   wifi_ssid: "YourSSID"
   wifi_password: "YourPassword"
   ```
4. Edit substitutions in the YAML / 編輯 YAML 中的 substitutions：
   - Set `name` and `friendly_name` / 設定設備名稱
   - Set `relay_count` to match your hardware (1, 2, or 3) / 設定 relay 數量（1/2/3）
   - Update `api` encryption key and `ota` password / 更新 API 加密金鑰與 OTA 密碼
5. Compile and upload via ESPHome dashboard or CLI / 透過 ESPHome 面板或 CLI 編譯上傳

---

## Configuration / 設定參數

### Substitutions

| Parameter / 參數 | Description / 說明 | Default / 預設 |
|-----------|-------------|---------|
| `name` | Device name / 設備名稱 | `tx-ultimate` |
| `friendly_name` | HA display name / HA 顯示名稱 | `TX Ultimate` |
| `relay_count` | Number of relays (1/2/3) / 繼電器數量 | `2` |
| `button_color` | Button LED RGB `{R,G,B}` / 按鍵燈顏色 | `{100,77,56}` |
| `nightlight_brightness` | Nightlight brightness (0-1) / 夜燈亮度 | `0.2` |
| `touch_color` | Touch feedback RGB / 觸控反饋顏色 | `{100,60,0}` |
| `swipe_left_color` | Swipe left RGB / 左滑顏色 | `{80,80,50}` |
| `swipe_right_color` | Swipe right RGB / 右滑顏色 | `{80,70,10}` |
| `multi_touch_color` | Full touch RGB / 全觸顏色 | `{0,80,40}` |
| `long_press_color` | Long press RGB / 長按顏色 | `{100,100,100}` |

### HA Switches / HA 開關

After flashing, the following switches appear in Home Assistant:

燒錄後，以下開關會出現在 Home Assistant 中：

| Switch / 開關 | Function / 功能 |
|--------|----------|
| `{name} L1/L2/L3` | Relay control / 繼電器控制 |
| `{name} Reverse` | Flip LED layout 180° / 翻轉 LED 燈效方向 |
| `{name} Nightlight` | Toggle nightlight mode / 切換夜燈模式 |
| `{name} Button Left/Middle/Right Mode` | Button LED mode / 按鍵 LED 模式 |

---

## License / 授權條款

MIT License — see [LICENSE](LICENSE)

---

## Acknowledgments / 致謝

- [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome) — Original ESPHome TX Ultimate project / 原始 ESPHome TX Ultimate 專案
- [ESPHome](https://esphome.io/) — Firmware framework / 韌體框架
