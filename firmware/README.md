# Firmware

This directory contains the microcontroller source code that drives the FootCensor.

## Architecture
- **Low-Latency Updates**: The firmware runs an internal loop at ~1kHz to constantly update the IMU and NIR array values.
- **USB HID Profile**: Presents the device directly as a standard USB HID Gamepad (no serial-to-virtual-joystick middleware required).
- **Parallel Processing**: 
  - IMU determines the current physical state (Resting vs Moving vs Input-Ready)
  - Optical array determines the desired direction
  - The final HID report combines both via a gating mechanism.

## Dependencies
*(List platform dependencies, e.g., PlatformIO, Arduino core, USB HID libraries here)*
