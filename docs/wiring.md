# Wiring Guide (Raspberry Pi Pico W)

This document maps the provided keypad/LED wiring to Pico W GPIOs.

## Assumptions

- Logical mapping follows firmware arrays in `src/main.cpp`.
- Physical wiring follows the provided Wokwi diagram and `diagram.json`.
- All LED cathodes are connected to common GND.
- Keypad row lines have external pull-ups (`1kΩ`) to 3V3 in the supplied diagram.

## Keypad GPIO Mapping

| Keypad Signal | Pico GPIO |
|---|---|
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |

## LED GPIO Mapping

Each LED anode is driven from a GPIO through a `220Ω` resistor. LED cathodes go to GND.

| Logical LED Index | LED Label | Pico GPIO |
|---:|---|---|
| 0 | 1 | GP11 |
| 1 | 2 | GP10 |
| 2 | 3 | GP9 |
| 3 | 4 | GP8 |
| 4 | 5 | GP7 |
| 5 | 6 | GP6 |
| 6 | 7 | GP5 |
| 7 | 8 | GP4 |
| 8 | A | GP3 |
| 9 | B | GP2 |
| 10 | C | GP28 |
| 11 | D | GP27 |

## Power / Ground

- Use Pico `3V3` to feed the keypad pull-up resistor chain.
- Use Pico `GND` as common return for all LEDs.

## Behavior Cross-Check

- Press `1..8`: turns on corresponding blue LED.
- Press `9`: turns on all blue LEDs (`1..8`).
- Press `0`: turns off all blue LEDs (`1..8`).
- Press `A..D`: turns on corresponding red LED.
- Press `*`: turns on red LEDs (`A..D`).
- Press `#`: turns off red LEDs (`A..D`).
