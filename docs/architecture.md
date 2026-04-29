# Firmware Architecture

## Overview

The firmware is a single-module control loop that polls a keypad and updates GPIO outputs for LEDs.

- Language/style: Arduino-flavored C++
- Entry points: `setup()` and `loop()`
- Input abstraction: `Keypad` library instance
- Output abstraction: direct GPIO writes via `digitalWrite`

## Module Layout

- `src/main.cpp`
  - Static key matrix definition (`keys`)
  - GPIO assignment arrays (`ledPins`, `rowPins`, `colPins`)
  - `Keypad keypad` object construction
  - `setup()` for GPIO initialization
  - `loop()` for key read and action dispatch

## Runtime Flow

1. `setup()` iterates through 12 LED GPIOs:
   - Configures each pin as output
   - Initializes each output LOW
2. `loop()`:
   - Reads one key using `keypad.getKey()`
   - If a valid key is returned (`!= NO_KEY`), executes a `switch` branch
   - Sets one or more LED outputs HIGH/LOW based on command
   - Sleeps 10 ms (`delay(10)`) for basic pacing/debounce friendliness

## Design Notes

- Core logic was intentionally kept unchanged.
- The implementation is deterministic and event-polled.
- There is no Wi-Fi, interrupt, or multitasking path in this revision.

## Portability Notes

Although the target hardware is Pico W, the code uses Arduino APIs. Practical build options:

- Keep Arduino core for Pico W and compile as-is (preferred for this exact logic).
- Port to Pico SDK only if required by deployment constraints.
