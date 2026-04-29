cmake_minimum_required(VERSION 3.13)

project(pico_keypad_led_controller C CXX ASM)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# This firmware uses Arduino-style APIs (Keypad, pinMode, digitalWrite).
# Build with a Pico-compatible Arduino core/toolchain (e.g., Earle Philhower core).
add_executable(${PROJECT_NAME}
  src/main.cpp
)
