# Self Balancing Robot with Custom PCB (ESP32)

## Overview

This project is a two wheeled self balancing robot built using an ESP32 and a custom designed PCB.

The goal was to design a compact and reliable embedded system by integrating control, sensing, power, and mechanical structure into a single platform.

---

## Key Features

* Custom PCB designed in KiCad
* ESP32 based control system
* MPU6050 IMU for angle sensing
* Dual motor driver system (TMC2209)
* NEMA17 stepper motors
* PID based balancing algorithm
* Custom mechanical body designed in CAD (Fusion 360)

---

## System Architecture

MPU6050 → ESP32 → PID Control → Motor Driver → Motors

---

## Hardware Components

* ESP32 microcontroller
* MPU6050 (IMU sensor)
* 2× TMC2209 motor drivers
* NEMA17 stepper motors
* 11.1V LiPo battery
* Custom designed PCB

---

## PCB Design

### PCB Layout

![PCB Layout](docs/images/pcb_layout.png)

### Schematic

![Schematic](docs/images/schematic.png)

### 3D View

![3D PCB](docs/images/pcb_3d.png)

### PCB Description

The custom PCB integrates:

* ESP32 control unit
* IMU interface (I2C communication)
* Motor driver connections
* Power distribution and regulation

This significantly reduces wiring complexity compared to breadboard setups and improves reliability.

---

## Mechanical Design (CAD)

### CAD Model

![CAD Model](docs/images/cad_render.png)

The robot body was designed in Fusion 360 with focus on:

* Structural stability
* Compact PCB integration
* Proper center of mass positioning for balance

---

## Control System

The robot uses a PID based control algorithm to maintain vertical balance.

**Parameters:**

* Kp: 38.0
* Kd: 2.2
* Kv: 0.010

The IMU provides tilt angle data, and the controller adjusts motor speed accordingly to stabilize the robot.

---

## Real Hardware

![Robot](docs/images/robot.jpg)

---

## Future Improvements

* Add encoder feedback for more precise control
* Improve PCB layout (noise reduction, grounding)
* Optimize PID tuning
* Add wireless control (Bluetooth/WiFi)
* Reduce system weight

---

## Goal

To develop a compact, efficient, and fully integrated self balancing robot system combining electronics, control algorithms, and mechanical design.
