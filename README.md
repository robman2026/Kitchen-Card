# Kitchen Card

A power-first Home Assistant Lovelace custom card for kitchen dashboards.

![Kitchen Card](https://img.shields.io/badge/version-1.0.0-blue) ![HACS](https://img.shields.io/badge/HACS-Custom-orange) ![HA](https://img.shields.io/badge/Home%20Assistant-2024.1%2B-brightgreen)

## Features

- ⚡ **Power-first layout** — total circuit as a featured large arc gauge, sub-circuits below
- 🍳 **Appliances** — oven, dishwasher, fridge etc. with optional live temperature arc gauge
- 💡 **Lights** — toggle tiles with tap-to-toggle support
- 🌡️ **Climate gauges** — dual-ring temp + humidity gauges with auto-severity colors
- 📡 **Sensors** — motion (animated), door, occupancy, illuminance and more
- 🎛️ **Full visual editor** — no YAML needed, all sections configurable via HA UI
- 📱 **Fully responsive** — works on desktop, tablet and mobile

## Screenshot

> *(Add a screenshot of your kitchen card here)*

## Installation via HACS

1. Go to **HACS → Frontend → ⋮ → Custom repositories**
2. Add `https://github.com/robman2026/kitchen-card` as category **Lovelace**
3. Click **Download**
4. Restart Home Assistant

## Add Resource

After installing, add the resource in **Settings → Dashboards → ⋮ → Manage resources**:

```
/hacsfiles/kitchen-card/kitchen-card.js
```

Type: `JavaScript module`

## Add the Card

In any dashboard, click **Add card → Custom: Kitchen Card**.

Or in YAML:

```yaml
type: custom:kitchen-card
card_title: Kitchen
card_icon: mdi:chef-hat
show_datetime: true
power_circuits:
  - entity: sensor.kitchen_power
    label: Kitchen Total
    energy_entity: sensor.kitchen_energy
    max_w: 5000
  - entity: sensor.oven_power
    label: Oven
    max_w: 3500
appliances:
  - entity: switch.oven
    label: Oven
    icon: mdi:stove
    temp_entity: sensor.oven_temperature
    temp_max: 300
  - entity: binary_sensor.dishwasher_door
    label: Dishwasher
    icon: mdi:dishwasher
    mode_entity: sensor.dishwasher_program
lights:
  - entity: light.kitchen_main
    label: Main Light
  - entity: light.kitchen_led
    label: LEDs
sensors:
  - entity: binary_sensor.kitchen_motion
    label: Occupancy
    category: motion
  - entity: sensor.kitchen_illuminance
    label: Illuminance
```

## Configuration

All options are available in the visual editor. The sections below describe what each section supports.

### Header

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `card_title` | string | `Kitchen` | Title shown in the header |
| `card_icon` | string | `mdi:chef-hat` | MDI icon for the header |
| `title_position` | `left` / `center` | `left` | Title alignment |
| `show_datetime` | boolean | `true` | Show live date and time |
| `show_status_dot` | boolean | `false` | Show online/offline status dot |
| `status_entity` | entity | — | Entity to determine status dot color |

### Power Circuits

The **first** circuit you add becomes the featured large gauge (total). All additional circuits appear as smaller sub-tiles.

| Option | Type | Description |
|--------|------|-------------|
| `entity` | sensor | Power entity in Watts |
| `energy_entity` | sensor | Energy entity in kWh (optional) |
| `current_entity` | sensor | Current entity in Amps (optional) |
| `label` | string | Display name |
| `max_w` | number | Max watts for gauge scale |

### Appliances

| Option | Type | Description |
|--------|------|-------------|
| `entity` | any | State entity (switch, binary_sensor, sensor) |
| `temp_entity` | sensor | Temperature sensor — shows arc gauge when set |
| `temp_max` | number | Max temp for gauge scale (default 300°C) |
| `mode_entity` | sensor / input_select | Program or mode entity for sub-text |
| `label` | string | Display name |
| `icon` | string | MDI icon (used when no temp_entity) |
| `state_on_label` | string | Badge text when on (default `On`) |
| `state_off_label` | string | Badge text when off (default `Off`) |

### Lights

| Option | Type | Description |
|--------|------|-------------|
| `entity` | light / switch | Toggle entity |
| `label` | string | Display name |
| `icon` | string | MDI icon |

### Climate Gauges

| Option | Type | Description |
|--------|------|-------------|
| `temp_entity` | sensor | Temperature sensor |
| `humidity_entity` | sensor | Humidity sensor (optional, inner ring) |
| `label` | string | Display name |

### Sensors

| Option | Type | Description |
|--------|------|-------------|
| `entity` | binary_sensor / sensor | Sensor entity |
| `label` | string | Display name |
| `category` | `sensor` / `motion` / `door` / `light` / `person` | Determines display format |
| `icon` | string | MDI icon |

## Color Logic

Gauge colors are fully automatic — no configuration needed:

| Sensor | Color scale |
|--------|------------|
| Temperature | Blue (cold) → Green (comfort) → Yellow (warm) → Red (hot) |
| Humidity | Yellow (dry) → Green (ideal) → Yellow (humid) → Red (very humid) |
| Appliance temp | Blue → Yellow → Orange → Red |
| Power | Gray (off) → Green (low) → Yellow (medium) → Red (high) |

## Related Cards

All cards by robman2026:

| Card | Repo |
|------|------|
| Multi-Panel Dashboard Card | [robman2026/multi-panel-dashboard-card](https://github.com/robman2026/multi-panel-dashboard-card) |
| Room Card | [robman2026/room-card](https://github.com/robman2026/room-card) |
| Kids Room Card | [robman2026/Kids-Room-Dashboard-Card](https://github.com/robman2026/Kids-Room-Dashboard-Card) |
| Garage Dashboard Card | [robman2026/garage-dashboard-card](https://github.com/robman2026/garage-dashboard-card) |
| Samsung Laundry Card | [robman2026/Laundry-Room-Card](https://github.com/robman2026/Laundry-Room-Card) |
| Power Monitor Card | [robman2026/power-monitor-card](https://github.com/robman2026/power-monitor-card) |

## License

MIT © robman2026
