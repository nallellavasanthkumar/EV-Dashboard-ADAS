# ⚡ EV Dashboard & ADAS Warning System

### Real-Time Electric Vehicle Dashboard and Advanced Driver Assistance System using STM32 Blue Pill

A real-time embedded system project developed using the **STM32F103C8T6 Blue Pill** to simulate an Electric Vehicle (EV) control and monitoring system with **Advanced Driver Assistance System (ADAS)** features.

The project combines sensor-based vehicle monitoring, EV control logic, UART communication, fault detection, audible warnings, and a Python-based real-time dashboard.

---

## 🚗 Project Overview

The system is designed to monitor important EV parameters and provide real-time driver assistance warnings.

The STM32 Blue Pill acts as the main controller. It processes vehicle parameters, ultrasonic sensor measurements, drive-mode logic, ADAS conditions, and fault conditions.

The processed data is transmitted through **UART** to a Python dashboard, where the vehicle status is displayed graphically in real time.

### System Flow

```text
        ┌──────────────────────┐
        │   Vehicle Inputs     │
        │                      │
        │ Speed / SOC / Temp   │
        │ Accelerator / Brake  │
        │ Ultrasonic Sensors   │
        └──────────┬───────────┘
                   │
                   ▼
        ┌──────────────────────┐
        │    STM32F103C8T6     │
        │      Blue Pill       │
        │                      │
        │ EV Control Logic     │
        │ ADAS Processing      │
        │ Fault Detection      │
        │ Alarm Management     │
        └──────────┬───────────┘
                   │
                 UART
                   │
                   ▼
        ┌──────────────────────┐
        │  Python Dashboard    │
        │                      │
        │ Speed                │
        │ Battery SOC          │
        │ Torque               │
        │ Motor Temperature    │
        │ Range                │
        │ ADAS Status          │
        │ Alarms & Faults      │
        └──────────────────────┘
```

---

## 🎯 Project Objectives

* Develop an embedded EV monitoring and control system.
* Interface and process ultrasonic sensor data.
* Implement ADAS warning logic.
* Monitor EV parameters such as speed, battery SOC, torque, and motor temperature.
* Implement multiple EV driving modes.
* Detect and manage critical system faults.
* Generate different buzzer warning patterns.
* Implement UART-based command and telemetry communication.
* Develop a real-time Python visualization dashboard.
* Test the complete system using STM32/PICSimLab simulation.

---

## ✨ Key Features

### ⚡ EV Monitoring

The system monitors:

* Vehicle speed
* Battery State of Charge (SOC)
* Motor torque
* Motor temperature
* Estimated driving range
* Accelerator pedal
* Brake pedal
* Current drive mode

### 🛣️ ADAS Features

The system provides:

* Front obstacle detection
* Collision warning
* Critical collision warning
* Time-to-Collision (TTC) monitoring
* Left blind-spot detection
* Right blind-spot detection
* Alarm priority management

### 🚘 Drive Modes

Three driving modes are supported:

| Mode   | Description                          |
| ------ | ------------------------------------ |
| ECO    | Reduced torque for efficient driving |
| NORMAL | Standard vehicle operation           |
| SPORT  | Increased torque response            |

### 🔔 Warning System

Different warning patterns are generated according to the severity of the detected condition:

* **NONE** — No warning
* **ADVISORY** — Single beep
* **WARNING** — Double beep
* **CRITICAL** — Rapid beep

### 🛠️ Fault Management

The system supports detection and testing of faults including:

* Motor over-temperature
* Low battery SOC
* Critical collision condition

Fault conditions can also be injected through the UART command interface for testing.

---

## 📡 UART Communication

UART is used as the communication interface between the STM32 system and the Python dashboard.

The embedded system provides a UART shell that supports commands such as:

```text
mode eco
mode normal
mode sport

speed set <kmh>
soc set <pct>
temp set <degC>

obstacle <cm>
obstacle clear

fault inject motor
fault inject soc
fault inject col

fault clear

alarm test
status
reset
help
```

The UART shell also provides a complete system status containing:

```text
Speed
SOC
Torque
Motor Temperature
Range
Drive Mode
Accelerator
Brake
Front Distance
Left Distance
Right Distance
TTC
Collision Status
Alarm Priority
Fault Flags
```

---

## 🖥️ Python EV Dashboard

A Python-based graphical dashboard was developed to visualize the vehicle parameters received from the STM32 through UART.

The dashboard provides:

* Real-time speedometer
* Battery SOC indicator
* Estimated range
* Speed history graph
* EV metrics panel
* Motor temperature
* Torque
* Accelerator and brake status
* ADAS bird's-eye view
* Front obstacle visualization
* Blind-spot indication
* TTC display
* Alarm indication
* Fault indication
* UART connection status

### Demo Mode

The dashboard also supports a demo mode that can run without STM32 hardware.

```bash
python dashboard.py --demo
```

### Hardware Mode

To connect the dashboard to a UART serial port:

```bash
python dashboard.py --port COM3
```

Example:

```bash
python dashboard.py --port COM3 --baud 115200
```

---

## 🔧 Hardware / Simulation

### Main Controller

* STM32F103C8T6 Blue Pill

### Sensors / Inputs

* HC-SR04 Ultrasonic Sensors
* Potentiometer-based simulated EV inputs
* Accelerator input
* Brake input
* Motor temperature input

### Output

* Buzzer / warning system
* UART telemetry

### Simulation / Development Tools

* STM32CubeIDE
* PICSimLab
* Python
* UART Serial Interface

---

## ⏱️ Timer Configuration

The project uses STM32 timers for different system functions.

### TIM1

Configured for PWM generation.

```text
Prescaler : 71
Period    : 9999
Mode      : PWM
Channel   : TIM1 Channel 1
```

### TIM2

Used as a high-resolution timing counter for measurement operations.

```text
Prescaler : 71
Period    : 65535
```

### TIM3

Configured for periodic timing operations.

```text
Prescaler : 7199
Period    : 999
```

---

## 📊 ADAS Logic

### Front Collision Detection

The front ultrasonic sensor measures the distance to an obstacle.

The system uses distance and TTC conditions to determine the severity of the warning.

```text
Safe
  ↓
Advisory
  ↓
Warning
  ↓
Critical
```

### Time-to-Collision

TTC is used as an additional parameter for estimating the risk of collision.

A lower TTC indicates a higher collision risk.

### Blind Spot Detection

Left and right ultrasonic measurements are used to identify nearby objects in the vehicle's blind-spot regions.

---

## 🧪 Testing & Fault Injection

The UART shell provides commands for testing system behavior without requiring an actual fault.

### Motor Overheat Test

```text
fault inject motor
```

Simulates:

```text
Motor Temperature = 95 °C
```

### Low Battery Test

```text
fault inject soc
```

Simulates:

```text
SOC = 1%
```

### Collision Test

```text
fault inject col
```

Simulates a critical collision condition.

### Alarm Test

```text
alarm test
```

Tests:

```text
ADVISORY
WARNING
CRITICAL
```

with different buzzer patterns.

---

## 📁 Project Structure

```text
EV-Dashboard-ADAS/
│
├── README.md
│
├── STM32/
│   ├── Core/
│   ├── Drivers/
│   └── ...
│
├── Python-Dashboard/
│   └── dashboard.py
│
├── Documentation/
│   ├── architecture.md
│   ├── uart-protocol.md
│   └── testing.md
│
├── Images/
│   ├── dashboard.png
│   ├── stm32.png
│   └── adas.png
│
└── Demo/
    └── demo-video-link.md
```

---

## ▶️ How to Run

### 1. STM32 Project

Open the STM32 project using **STM32CubeIDE**.

Build and flash/run the firmware on the STM32 Blue Pill or use the configured simulation environment.

### 2. UART Connection

Connect the STM32 UART interface to the computer and identify the corresponding COM port.

Example:

```text
COM3
```

### 3. Install Python Dependencies

```bash
pip install pyserial matplotlib numpy
```

### 4. Run the Dashboard

For hardware:

```bash
python dashboard.py --port COM3 --baud 115200
```

For demonstration without hardware:

```bash
python dashboard.py --demo
```

---

## 📈 Future Improvements

Possible future enhancements include:

* CAN bus communication
* Real EV motor controller integration
* Real battery management system integration
* GPS-based range estimation
* Vehicle-to-vehicle communication
* Camera-based ADAS
* Lane departure warning
* Automatic emergency braking
* Cloud-based telemetry
* Mobile application integration
* Machine-learning-based driver assistance

---

## 📚 Technologies Used

```text
C / Embedded C
STM32F103C8T6
STM32CubeIDE
HAL Drivers
UART
PWM
Timers
ADC
HC-SR04
PICSimLab
Python
PySerial
NumPy
Matplotlib
```

---

## 👨‍💻 Project

**EV Dashboard & ADAS Warning System**

Developed as an embedded systems project focusing on:

**Embedded C • STM32 • EV Control • ADAS • Sensors • UART • Python Visualization**

---

## ⭐ Acknowledgement

This project was developed as part of an Embedded Systems internship and demonstrates the integration of embedded firmware, sensor processing, vehicle-control concepts, communication interfaces, fault management, and PC-based visualization.
