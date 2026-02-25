# Optimization Notes

## 1. Motor Oscillation Issue
Initial PD tuning caused aggressive oscillation.
Solution:
- Reduced Kp
- Increased Kd for damping
- Added control deadband

---

## 2. Motor Noise Problem
Motors produced mechanical vibration noise.

Root Causes:
- Low microstepping configuration
- High Vref setting

Solutions:
- Switched to 1/16 microstepping (MS1/MS2 hardware config)
- Tuned Vref to ~0.97–0.98V
- Reduced RATE_SCALE after microstepping change

---

## 3. Faulty Driver Detection
One TMC2209 module showed unstable Vref behavior (0.04V jump).
Replaced driver and recalibrated.

---

## 4. Final Stable Configuration
- Kp = 7.5
- Kd = 3.5
- Microstepping = 1/16
- Vref ≈ 0.97–0.98V
- Stable around 0° with reduced acoustic noise
