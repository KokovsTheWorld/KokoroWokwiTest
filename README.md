# Pico W Keypad-to-LED Controller

A Raspberry Pi Pico W project that reads a 4x4 matrix keypad and controls 12 discrete LEDs based on key presses.

> **Important:** The firmware logic was preserved exactly as provided. This repository update is documentation and structure focused.

## Features

- 4x4 keypad scanning through the `Keypad` library
- 12 independent LED outputs
- Group controls:
  - `9` turns ON LEDs mapped to keys `1..8`
  - `0` turns OFF LEDs mapped to keys `1..8`
  - `*` turns ON LEDs mapped to `A..D`
  - `#` turns OFF LEDs mapped to `A..D`
- Wiring and architecture docs for simulator and hardware bring-up

## Repository Layout

```text
.
├── CMakeLists.txt
├── diagram.json
├── docs/
│   ├── architecture.md
│   └── wiring.md
├── include/
├── src/
│   └── main.cpp
└── README.md
```

## Components (from `diagram.json`)

- 1x Raspberry Pi Pico / Pico W (target board for deployment is Pico W)
- 1x 4x4 membrane keypad
- 12x LEDs
  - 8 blue LEDs labeled `1..8`
  - 4 red LEDs labeled `A..D`
- 12x LED current-limiting resistors (`220Ω`)
- 4x keypad pull-up resistors (`1kΩ`) tied to 3V3
- jumper wires and USB cable

## Quick Start

### Wokwi

1. Create a new **Raspberry Pi Pico** project in Wokwi.
2. Paste `diagram.json` into the Wokwi diagram editor (or wire manually using `docs/wiring.md`).
3. Use the firmware from `src/main.cpp` in an Arduino-compatible environment.
4. Start simulation and press keypad buttons to verify LED behavior.

### Real Hardware (Pico W)

1. Wire the circuit as documented in `docs/wiring.md`.
2. Build and flash using your preferred Pico-compatible Arduino workflow.
3. Open serial monitor only if you later add debug prints (current firmware does not print).

## Build / Flash Notes

This source is **Arduino-style C++** (`Keypad.h`, `setup()`, `loop()`).

### Option A: Arduino IDE / Arduino CLI (recommended for current code)

- Board core: **Raspberry Pi Pico/RP2040** (Earle Philhower)
- Board: **Raspberry Pi Pico W**
- Install library: **Keypad**
- Compile and upload `src/main.cpp` content as sketch code.

### Option B: Pico SDK adaptation

If you need pure Pico SDK, retain behavior but port `Keypad` and Arduino GPIO calls to SDK APIs. This repository intentionally does **not** perform that logic rewrite.

## Wi-Fi Notes

- Current firmware does not use Wi-Fi.
- If Wi-Fi is added later, keep credentials out of source control by using:
  - a local `secrets.h` / `secrets.hpp` ignored by git
  - environment variables in CI

## Documentation Index

- Wiring details: [`docs/wiring.md`](docs/wiring.md)
- Firmware architecture: [`docs/architecture.md`](docs/architecture.md)
