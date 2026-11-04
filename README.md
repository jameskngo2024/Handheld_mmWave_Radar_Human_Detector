# Handheld mmWave Radar Human Detector

A handheld radar device that detects nearby people and shows them on a military-style display, inspired by the heartbeat sensor from *Call of Duty*.

> **Status:** Early development

## What It Does

The device uses millimeter-wave radar to sense people around it, even through thin walls like drywall or wood. Each detected person appears as a blip on a radar-style screen with a rotating sweep, and a small vibration motor pulses as people get closer.

**Planned capabilities**
- Detect and track up to 3 people at once
- Range of about 6 meters, with a wide field of view
- A *Call of Duty*-style radar display
- Vibration feedback based on distance
- Rechargeable battery in a handheld, 3D-printed case

## Components

| Component | Part | Role |
|---|---|---|
| Radar sensor | **HLK-LD2450** (24 GHz mmWave) | Detects people and reports their position and movement |
| Microcontroller | **ESP32-S3** | The "brain": reads radar data, processes it, and drives the display |
| Display | **2.4" TFT screen** | Shows the radar interface |
| Haptics | **Vibration motor** | Gives tactile alerts |
| Power | **18650 battery + charging and 5 V boost modules** | Portable, rechargeable power |

## How It Connects

```
 ┌──────────────┐        ┌──────────────┐        ┌──────────────┐
 │ Radar Sensor │──UART─►│   ESP32-S3   │──SPI──►│   Display    │
 │  (LD2450)    │        │              │        │              │
 └──────────────┘        └──────┬───────┘        └──────────────┘
                                │
                         ┌──────▼───────┐
                         │ Vibration    │
                         │ Motor        │
                         └──────────────┘

     Battery ──► Charger ──► 5 V Boost ──► Powers all components
```

- The **radar** sends target data to the ESP32 over a serial connection (UART).
- The **ESP32** sends graphics to the screen over SPI.
- The **vibration motor** is driven by an output pin on the ESP32.
- The **battery system** supplies power to everything.

## Workflow

1. **Sense:** the radar scans its surroundings and finds people.
2. **Process:** the ESP32 reads each person's position and cleans up noisy readings.
3. **Display:** people appear as blips on the radar screen.
4. **Alert:** the vibration motor pulses faster as someone gets closer.

## Roadmap

- [ ] Get the radar talking to the ESP32
- [ ] Build the radar display
- [ ] Improve accuracy and filter out false detections
- [ ] Add battery power
- [ ] Design a custom circuit board
- [ ] Build a handheld enclosure
- [ ] Future: longer range and a heartbeat/breathing detection mode

## Author

**James Ngo**, Computer Engineering @ University of Houston
