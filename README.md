# 足コン (Ashicon): Dual-Ankle Low-Latency USB Stick Replacement Interface

![Status](https://img.shields.io/badge/Status-Prototyping-orange)
![License](https://img.shields.io/badge/License-MIT-blue)
![Architecture](https://img.shields.io/badge/Hardware-NIR%20%2B%20IMU-brightgreen)

**足コン (Ashicon)** (formerly FootCensor) is a research and development project aiming to replace the left and right analog sticks of a standard gamepad with **wearable devices attached to both ankles**. It enables low-latency PC game inputs by capturing the subtle deformations of the skin, tendons, and muscles around the ankle using an array of near-infrared (NIR) sensors, assisted by an IMU for state estimation.

<p align="center">
  <em>Free your hands. Control your movement and camera with your feet.</em>
</p>

## 🌟 Key Features

*   **Left Ankle = Movement (Left Stick)**: Controls character movement (forward, backward, left, right).
*   **Right Ankle = Camera (Right Stick)**: Controls camera or viewpoint (up, down, left, right).
*   **Low-Latency USB HID**: The device connects via a wired USB connection and presents itself directly to the PC as a standard USB HID Gamepad, bypassing the need for intermediate translation software. Targets an internal update rate of ~1kHz.
*   **Parallel 2-Stage Estimation**:
    *   **IMU (Traffic Controller)**: Detects the macroscopic state (Resting, Ready for Input, Posture Transition, Walking) to allow, suppress, or block inputs.
    *   **Optical NIR Array (Direction Engine)**: Reads micro-deformations in the ankle to estimate the intended input direction.
*   **Rapid Calibration**: Designed for quick 30-60 second initial calibration and 5-10 second re-calibration upon re-equipping.

## 🚀 Evolution from AnkleSens

This project significantly builds upon and overcomes the limitations of prior research, specifically *AnkleSens* (`papers/7330752.pdf`), which demonstrated the feasibility of using 16 photo-reflective sensors on the ankle to classify foot posture. However, AnkleSens was limited as an HCI prototype by its inability to separate motion states, processing delays (offline learning), and wired constraints.

**Ashicon introduces three major breakthroughs for practical gaming use:**

1. **IMU Gating (Traffic Controller)**: Unlike AnkleSens, which relied entirely on optical sensors, Ashicon introduces an IMU to determine macroscopic states (e.g., walking, posture transitions). This successfully separates "mere leg crossing" from "intentional input actions," drastically reducing false positives.
2. **Direct HID Mapping (Low-Latency)**: Moving away from offline classification via 8-bit microcontrollers, Ashicon maps the optical directional output directly to a 1ms low-latency USB HID Gamepad interface, achieving OS-level integration essential for gaming.
3. **Wireless Future**: While the initial prototype is wired for latency guarantees, the architecture is designed with the ultimate goal of Bluetooth/2.4GHz wireless operation, completely freeing the user from cable tangling issues inherent to ankle-worn devices.

## 📁 Repository Structure

```
FootCensor/
├── docs/            # Detailed system architecture, requirements, and development phases
├── hardware/        # Mechanical CAD files (3D printable bands/mounts) and PCB schematics
├── firmware/        # Microcontroller code (C/C++, USB HID implementation, sensor reading)
├── software/        # PC-side data collection, visualization, and ML training scripts
└── papers/          # Reference literature and related academic papers
```

## 📖 Documentation

For detailed technical specifications and development plans, please refer to the `docs/` folder:

1.  **[System Architecture](docs/system_architecture.md)**: Details the sensor choices, USB HID strategy, processing pipeline, and machine learning models.
2.  **[Requirements and Specifications](docs/requirements_and_fixations.md)**: Outlines the design goals, constraints, priority (Latency > Stability > Accuracy), and output forms.
3.  **[Development Phases](docs/development_phases.md)**: Describes the step-by-step approach starting from a single left-foot unit up to full dual-ankle integration.
4.  **[Future Works](docs/future_works.md)**: Notes on expanding the system into full VR tracking and complex simultaneous interactions.

## 🔬 Scientific Background

This project builds upon the foundations of several research domains:
*   **Foot Posture Prediction**: Utilizing photo-reflective sensors on the ankle (e.g., *AnkleSens*).
*   **Gait Phase Detection via Muscle Deformation**: Reading millimeter-scale deformations from the skin surface.
*   **Wrist-Worn Optical and Inertial Networks**: Combining NIR and IMU for gesture detection without direct hand occlusion.

See the `papers/` directory for the source materials inspiring this architecture.

## 🚀 Getting Started

*(Development is currently in Phase 1: Left-foot standalone prototype).*

1.  **Hardware**: Check the `hardware/` directory for the latest prototype designs (BOM, 3D models).
2.  **Firmware**: Flash the microcontroller using the project in `firmware/`. The device should show up as a `USB Gamepad` on Windows.
3.  **Software**: Use the Python scripts in `software/` to collect raw sensor data and train the initial directional classifiers.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
