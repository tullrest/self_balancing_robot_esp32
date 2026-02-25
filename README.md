# Self-Balancing Robot (ESP32)

A two-wheeled self-balancing robot built using an ESP32, MPU6050 IMU, and TMC2209 stepper drivers.

This project implements real-time PD control with hardware timer–based step generation to stabilize an inverted pendulum system.

---

## Project Overview

The objective of this project was to design and implement a real-time self-balancing robot that maintains an upright position (0° pitch) using feedback control.

Unlike delay-based stepping, this system uses a hardware timer interrupt on the ESP32 to generate deterministic step pulses, improving control stability and reducing jitter.

The robot integrates:

- Real-time sensor fusion
- Closed-loop PD control
- Motor driver current tuning
- Microstepping optimization
- Custom CAD chassis design

---

## Control Strategy

The robot is modeled as an inverted pendulum.

State variables:
- θ (pitch angle)
- ω (angular velocity)

A PD controller is used:

u = Kp·θ + Kd·ω

Where:
- Kp corrects positional error
- Kd provides damping to reduce oscillation

Angle estimation is handled using the MPU6050 library’s complementary filtering of accelerometer and gyroscope data.

Detailed explanation:
See `docs/control_strategy.md`

---

## System Architecture

**Microcontroller**
- ESP32 Dev Module

**IMU**
- MPU6050 (I2C)

**Motor Drivers**
- 2× TMC2209 (configured for 1/16 microstepping)

**Motors**
- NEMA 17 Stepper Motors

**Power**
- 2S LiPo Battery (7.4V)

Wiring details:
See `hardware/wiring.md`

---

## Engineering Challenges & Solutions

### 1. Oscillation Instability
Initial aggressive proportional gain caused high-frequency oscillation.

Solution:
- Reduced Kp
- Increased Kd
- Added control deadband

---

### 2. Excessive Motor Noise
Motors produced mechanical vibration during micro-corrections.

Root causes:
- Default 1/8 microstepping
- High driver current (Vref)

Solutions:
- Upgraded to 1/16 microstepping via MS1/MS2 hardware configuration
- Tuned Vref to ~0.97–0.98V
- Adjusted RATE_SCALE for smoother response

---

### 3. Faulty Driver Debugging
One TMC2209 module showed unstable Vref behavior (~0.04V fluctuation).

Resolution:
- Replaced defective driver
- Recalibrated both drivers for matched current

---

## Mechanical Design

The chassis was custom-designed in CAD with the following considerations:

- Low center of gravity
- Symmetric motor alignment
- Stable battery placement
- Rigid frame to reduce vibration

CAD files and renders:
➡️ See `/cad` directory

---

## Final Stable Configuration

- Kp = 7.5
- Kd = 3.5
- Microstepping = 1/16
- Vref ≈ 0.97–0.98V
- Stable near 0° with reduced acoustic noise

---

## Key Technical Highlights

- Hardware timer–based deterministic step generation
- Real-time closed-loop PD control
- Driver current calibration (Vref tuning)
- Microstepping-based vibration reduction
- Structured debugging and iterative optimization

---

## Demo



---

## Lessons Learned

- Deterministic timing is critical in real-time control systems.
- Hardware misconfiguration can mimic control instability.
- Iterative tuning is essential for physical dynamic systems.
- Mechanical design significantly affects control performance.

---

## License

This project is for educational and portfolio purposes.
