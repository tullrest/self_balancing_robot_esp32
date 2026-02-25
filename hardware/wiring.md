# Hardware Wiring – Self Balancing Robot

## 1. Microcontroller

**Board:** ESP32 Dev Module

Power:
- VIN → 7.4V (2S LiPo via motor driver supply)
- 3.3V → Logic supply for MPU6050 and MS pins
- GND → Common ground across all components

---

## 2. MPU6050 (I2C)

| MPU6050 Pin | ESP32 Pin |
|-------------|-----------|
| VCC         | 3.3V      |
| GND         | GND       |
| SDA         | GPIO21    |
| SCL         | GPIO22    |

I2C is used for angle estimation.

---

## 3. TMC2209 Stepper Drivers

Two drivers are used (Left and Right motor).

### STEP/DIR Connections

| Driver Pin | ESP32 Pin |
|------------|-----------|
| STEP1      | GPIO18    |
| DIR1       | GPIO19    |
| STEP2      | GPIO14    |
| DIR2       | GPIO23    |

---

### Microstepping Configuration

MS1 → 3.3V  
MS2 → 3.3V  

Configured for 1/16 microstepping to reduce mechanical noise and improve smoothness.

---

### Vref Calibration

Final calibrated values:
- Driver 1: ~0.97V
- Driver 2: ~0.98V

Measured between trim potentiometer and GND.

Lowering Vref reduced acoustic noise while maintaining sufficient torque.

---

## 4. Motors

Type: NEMA17 Stepper Motor  
Driven in full bipolar mode via TMC2209.

---

## 5. Power System

Battery:
- 2S LiPo (7.4V nominal)
- Connected to VM input of both drivers

All grounds are shared between:
- ESP32
- Drivers
- MPU6050

---

## 6. Notes

- Ensure common ground between ESP32 and drivers.
- Incorrect Vref calibration may cause oscillation or insufficient torque.
- Faulty TMC2209 module was replaced during debugging process.
