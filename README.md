# Sonoff TX Ultimate — Smart Light Version

ESPHome 韌體配置：Sonoff TX Ultimate 觸控面板 + 智慧燈效

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

[English](#english) | [繁體中文](#繁體中文)

---

<a id="english"></a>
## English

### What is this

ESPHome firmware for Sonoff TX Ultimate touch panel with configurable smart lighting effects. Supports 2/3 relay touch zones, runtime LED direction flip, nightlight mode, and per-button LED color control.

**Architecture:**
```
Sonoff TX Ultimate (ESP32)
  ├─ Touch Panel (UART) → relay control via touch zones
  ├─ NeoPixel LED Ring (32 LEDs)
  │   ├─ Button LEDs (left / middle / right)
  │   └─ Top LEDs (ambient / touch feedback / nightlight)
  ├─ Vibration Motor
  └─ I2S Audio Output
          ↓
    Home Assistant ← API / OTA
```

### Forked from

This project is forked from [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome).

The original project provides base ESPHome firmware for TX Ultimate with touch panel and LED control. This fork adds:

- 🔌 Multi-relay (2/3) touch zone mapping
- 🔄 Runtime **Reverse** switch — flip LED layout 180° for different installation orientations
- 🌙 Nightlight mode with HA integration
- 🎨 Configurable touch/swipe/long-press LED color effects
- 💡 Independent button LED mode control (left / middle / right)

### Flashing Instructions

> Please refer to the original project's flashing guide:
>
> 👉 [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome)

### Quick Start

#### 1. Prerequisites

- [ESPHome](https://esphome.io/guides/installing_esphome.html) installed
- Sonoff TX Ultimate hardware

#### 2. Clone and Configure

```bash
git clone https://github.com/Nyquist1992/tx-ultimate-smartlight-version.git
cd tx-ultimate-smartlight-version

# Create secrets.yaml with your WiFi credentials
cat > secrets.yaml << 'EOF'
wifi_ssid: "YourSSID"
wifi_password: "YourPassword"
EOF
```

#### 3. Edit YAML

Open `tx-ultimate-smartlight-version.yaml` and edit substitutions:

```yaml
substitutions:
  name: your-device-name
  friendly_name: "Your Device Name"
  relay_count: "2"  # 1, 2, or 3
```

Update `api` encryption key and `ota` password to unique values.

#### 4. Flash

```bash
# Via CLI
esphome run tx-ultimate-smartlight-version.yaml

# Or use ESPHome dashboard (recommended)
# Add the YAML file to ESPHome dashboard and click Upload
```

### Substitutions

| Parameter | Description | Default |
|-----------|-------------|---------|
| `name` | Device name (ESPhome ID) | `tx-ultimate` |
| `friendly_name` | HA display name | `TX Ultimate` |
| `relay_count` | Number of relays: `1`, `2`, or `3` | `2` |
| `button_color` | Button LED RGB `{R,G,B}` | `{100,77,56}` |
| `button_brightness` | Button LED brightness (0-1) | `0.4` |
| `nightlight_brightness` | Nightlight brightness (0-1) | `0.2` |
| `nightlight_color` | Nightlight RGB | `{100,100,100}` |
| `touch_color` | Touch feedback RGB | `{100,60,0}` |
| `swipe_left_color` | Swipe left RGB | `{80,80,50}` |
| `swipe_right_color` | Swipe right RGB | `{80,70,10}` |
| `multi_touch_color` | Full touch RGB | `{0,80,40}` |
| `long_press_color` | Long press RGB | `{100,100,100}` |

### HA Switches

| Switch | Function |
|--------|----------|
| `{name} L1 / L2 / L3` | Relay on/off |
| `{name} Reverse` | Flip LED layout 180° |
| `{name} Nightlight` | Toggle nightlight (ON = lights off, OFF = white 20%) |
| `{name} Button Left Mode` | Button left LED mode |
| `{name} Button Middle Mode` | Button middle LED mode |
| `{name} Button Right Mode` | Button right LED mode |
| `{name} Restart` | Reboot device |

### Touch Zone Mapping

Touch position is mapped to relays based on `relay_count`:

| relay_count | Touchzone → Relay |
|-------------|-------------------|
| `1` | All positions → L1 |
| `2` | pos ≤ 5 → L1, else → L2 |
| `3` | pos ≤ 3 → L1, pos ≤ 7 → L2, else → L3 |

### LED Layout (Normal vs Reverse)

The TX Ultimate has 32 WS2811 LEDs in a ring. The **Reverse** switch rotates the mapping by 16 LEDs (180°).

**Normal:**
```
Button Left  [0-1, 31]    Button Middle [2-5]    Button Right [6-8]
              LEDs Top [9-30]
```

**Reverse:**
```
Button Left  [22-24]    Button Middle [18-21]    Button Right [15-17]
              LEDs Top [0-14, 25-31]
```

### Notes

- The YAML file uses ESPHome substitutions — values are text-replaced at compile time.
- `relay_count` is compile-time only. Changing it requires re-flashing.
- `Reverse` is runtime — toggled via HA switch, no re-flash needed.
- For 2-relay users: `Button Right` partition exists but is unused (no touchfield triggers it).
- API encryption key and OTA password should be changed to unique values before flashing.

### Related Projects

- [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome) — Original TX Ultimate ESPHome project
- [ESPHome](https://esphome.io/) — Firmware framework
- [Sonoff TX Ultimate](https://www.itead.cc/smart-home/sonoff-tx-ultimate.html) — Hardware

### License

MIT License — Based on [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome)

---

<a id="繁體中文"></a>
## 繁體中文

### 這是什麼

適用於 Sonoff TX Ultimate 觸控面板的 ESPHome 韌體配置，支援可配置的智慧燈效。包含 2/3 路繼電器觸控區域映射、runtime LED 方向翻轉、夜燈模式、按鍵 LED 顏色獨立控制。

**架構：**
```
Sonoff TX Ultimate (ESP32)
  ├─ 觸控面板 (UART) → 透過觸控區域控制繼電器
  ├─ NeoPixel LED 環 (32 顆)
  │   ├─ 按鍵燈 (左 / 中 / 右)
  │   └─ 頂部燈 (氛圍 / 觸控反饋 / 夜燈)
  ├─ 震動馬達
  └─ I2S 音訊輸出
          ↓
    Home Assistant ← API / OTA
```

### Fork 自

本專案 fork 自 [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome)。

原始專案提供 TX Ultimate 基礎 ESPHome 韌體，包含觸控面板與 LED 控制。本 Fork 新增：

- 🔌 多繼電器（2/3 路）觸控區域映射
- 🔄 Runtime **Reverse** 開關 — 翻轉 LED 燈效方向 180°，適配不同安裝方向
- 🌙 整合 HA 的夜燈模式
- 🎨 可配置的觸控 / 滑動 / 長按 LED 顏色效果
- 💡 按鍵 LED 模式獨立控制（左 / 中 / 右）

### 燒錄說明

> 請參閱原專案的燒錄指南：
>
> 👉 [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome)

### 快速開始

#### 1. 前置需求

- 已安裝 [ESPHome](https://esphome.io/guides/installing_esphome.html)
- Sonoff TX Ultimate 硬體

#### 2. Clone 並設定

```bash
git clone https://github.com/Nyquist1992/tx-ultimate-smartlight-version.git
cd tx-ultimate-smartlight-version

# 建立 secrets.yaml 填入 WiFi 密碼
cat > secrets.yaml << 'EOF'
wifi_ssid: "YourSSID"
wifi_password: "YourPassword"
EOF
```

#### 3. 編輯 YAML

開啟 `tx-ultimate-smartlight-version.yaml`，編輯 substitutions：

```yaml
substitutions:
  name: your-device-name
  friendly_name: "你的設備名稱"
  relay_count: "2"  # 1、2 或 3
```

更新 `api` 加密金鑰和 `ota` 密碼為唯一位元組。

#### 4. 燒錄

```bash
# 透過 CLI
esphome run tx-ultimate-smartlight-version.yaml

# 或使用 ESPHome 面板（推薦）
# 將 YAML 加入 ESPHome 面板，點選 Upload
```

### Substitutions 設定

| 參數 | 說明 | 預設值 |
|------|------|--------|
| `name` | 設備名稱（ESPhome ID） | `tx-ultimate` |
| `friendly_name` | HA 顯示名稱 | `TX Ultimate` |
| `relay_count` | 繼電器數量：`1`、`2` 或 `3` | `2` |
| `button_color` | 按鍵燈 RGB `{R,G,B}` | `{100,77,56}` |
| `button_brightness` | 按鍵燈亮度（0-1） | `0.4` |
| `nightlight_brightness` | 夜燈亮度（0-1） | `0.2` |
| `nightlight_color` | 夜燈 RGB | `{100,100,100}` |
| `touch_color` | 觸控反饋 RGB | `{100,60,0}` |
| `swipe_left_color` | 左滑 RGB | `{80,80,50}` |
| `swipe_right_color` | 右滑 RGB | `{80,70,10}` |
| `multi_touch_color` | 全觸 RGB | `{0,80,40}` |
| `long_press_color` | 長按 RGB | `{100,100,100}` |

### HA 開關

| 開關 | 功能 |
|------|------|
| `{name} L1 / L2 / L3` | 繼電器開關 |
| `{name} Reverse` | 翻轉 LED 燈效方向 180° |
| `{name} Nightlight` | 切換夜燈模式（ON = 熄燈，OFF = 白色 20%） |
| `{name} Button Left Mode` | 左按鍵 LED 模式 |
| `{name} Button Middle Mode` | 中按鍵 LED 模式 |
| `{name} Button Right Mode` | 右按鍵 LED 模式 |
| `{name} Restart` | 重啟設備 |

### 觸控區域映射

根據 `relay_count` 將觸控位置映射到繼電器：

| relay_count | 觸控區域 → 繼電器 |
|-------------|-------------------|
| `1` | 所有位置 → L1 |
| `2` | pos ≤ 5 → L1，其餘 → L2 |
| `3` | pos ≤ 3 → L1，≤ 7 → L2，其餘 → L3 |

### LED 分區（Normal vs Reverse）

TX Ultimate 有 32 顆 WS2811 LED 環形排列。**Reverse** 開關將 LED 映射旋轉 16 顆（180°）。

**Normal：**
```
Button Left  [0-1, 31]    Button Middle [2-5]    Button Right [6-8]
              LEDs Top [9-30]
```

**Reverse：**
```
Button Left  [22-24]    Button Middle [18-21]    Button Right [15-17]
              LEDs Top [0-14, 25-31]
```

### 備註

- YAML 使用 ESPHome substitutions — 數值在編譯時文字替換。
- `relay_count` 僅限編譯前設定，更改需重新燒錄。
- `Reverse` 為 runtime — 透過 HA 開關切換，無需重新燒錄。
- 2-relay 用戶：`Button Right` 分區存在但不會被觸發（沒有 touchfield 會啟動它）。
- API 加密金鑰和 OTA 密碼應在燒錄前改為唯一位元組。

### 相關專案

- [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome) — 原始 TX Ultimate ESPHome 專案
- [ESPHome](https://esphome.io/) — 韌體框架
- [Sonoff TX Ultimate](https://www.itead.cc/smart-home/sonoff-tx-ultimate.html) — 硬體

### License

MIT License — 基於 [SmartHome-yourself/sonoff-tx-ultimate-for-esphome](https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome)
