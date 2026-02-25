# Control Strategy – Self Balancing Robot

## 1. System Model

The robot is modeled as an inverted pendulum mounted on two wheels.
The objective is to maintain the pitch angle at 0° (upright position).

State variable:
- θ : Pitch angle (degrees)
- ω : Angular velocity (deg/s)

Control objective:
Maintain θ ≈ 0 while rejecting disturbances.


---

## 2. Angle Estimation

The MPU6050 provides:
- Accelerometer-based tilt estimation (stable but noisy)
- Gyroscope angular velocity (fast but drifting)

The library internally applies a complementary filter:

θ_est = α(θ_prev + gyro * dt) + (1 − α)(acc_angle)

This balances short-term gyro accuracy and long-term accelerometer stability.


---

## 3. PD Controller Design

A Proportional-Derivative (PD) controller is used:

u = Kp * θ + Kd * ω

Where:
- Kp corrects positional error
- Kd damps oscillation via angular velocity feedback

Why PD (not full PID)?
- Integral term was unnecessary for this platform
- System reacts quickly and does not require steady-state bias correction


---

## 4. Motor Control Implementation

Instead of using delay-based stepping,
a hardware timer interrupt is used for deterministic pulse generation.

Timer frequency determines step rate:

halfPeriod = 1 / (2 * step_rate)

This ensures:
- Stable motor timing
- Reduced jitter
- Better balance stability


---

## 5. Noise and Oscillation Reduction

Several optimizations were implemented:

- Deadband around small angle values
- Deadband on control output (u)
- Microstepping increased to 1/16 (hardware configuration)
- Vref tuned to ~0.97V for torque/noise balance

These reduced acoustic noise and micro oscillation.


---

## 6. Final Tuning Values

- Kp = 7.5
- Kd = 3.5
- Microstepping = 1/16
- Vref ≈ 0.97–0.98V
- Stable around θ = 0° ± small oscillation


---

## 7. Lessons Learned

- Real-time control requires deterministic timing.
- Driver configuration significantly affects mechanical noise.
- Hardware issues (faulty driver, Vref instability) can mimic control instability.
- Iterative tuning is essential for physical systems.
