# Engineering Systems Lab

My next-stage engineering lab focused on robotics, FreeRTOS, PCB design, power systems, deeper embedded C/C++, and original custom hardware builds.

This repository marks the transition from small embedded learning exercises into larger engineering systems that require planning, integration, testing, debugging, and design decisions across hardware and software.

## Main Goals

- Build complete robotic and embedded systems instead of isolated exercises
- Strengthen embedded C/C++ beyond basic Arduino-style sketches
- Learn FreeRTOS and real-time firmware architecture
- Design and test custom PCBs
- Understand safe low-voltage power systems and power distribution
- Improve debugging, testing, and technical documentation
- Use Python as a supporting engineering tool for automation, data analysis, testing, and computer-side robotics tasks
- Create original projects strong enough for an engineering portfolio and JoyraTech content

## Development Path

### Phase 1 — Robotics
Build a custom ESP32-based robotic vehicle with motor control, sensors, manual control, autonomous behavior, and a proper power system.

Focus areas:
- DC motor control
- Motor drivers
- PWM
- Ultrasonic and other sensors
- State machines
- Mechanical integration
- Battery-powered operation
- Debugging complete systems

### Phase 2 — FreeRTOS
Rebuild or expand the robot firmware using FreeRTOS.

Focus areas:
- Tasks
- Task priorities
- Queues
- Semaphores and mutexes
- Software timers
- Inter-task communication
- Watchdogs
- Real-time scheduling
- Multi-core ESP32 development

### Phase 3 — PCB Design
Move from breadboard-only prototypes toward custom circuit boards.

Focus areas:
- KiCad
- Schematic capture
- Component selection
- Footprints
- PCB layout
- Ground and power routing
- Decoupling capacitors
- Connectors
- Design-rule checking
- PCB fabrication
- Board bring-up and testing

### Phase 4 — Power Systems
Learn how to design reliable low-voltage power architectures for embedded and robotic systems.

Focus areas:
- Voltage regulators
- Buck and boost converters
- Battery monitoring
- Current sensing
- Fuses and protection
- Power distribution
- Grounding
- Low-battery detection
- Power budgeting

For safety, initial work will stay focused on low-voltage DC systems rather than mains electricity.

### Phase 5 — Deeper Firmware
Move beyond single-file Arduino sketches into more structured embedded software.

Focus areas:
- C/C++ project organization
- Header and source files
- Classes and structs
- Pointers and references
- Memory management
- Bitwise operations
- Hardware abstraction
- Interrupts
- Timers
- UART, I2C, and SPI
- Device drivers
- Error handling
- Logging
- Unit and hardware testing

### Phase 6 — Original Custom Builds
Combine electronics, firmware, mechanical systems, and power design into larger original projects.

Possible directions include:
- Mobile robots
- Smart workshop equipment
- Automated tools
- Sensor platforms
- Vehicle and mobility modifications
- Custom electronics for JoyraTech builds

## Programming Focus

### Primary — C/C++
C/C++ will remain the main language for embedded firmware, ESP32 development, FreeRTOS, hardware drivers, timing-critical code, and low-level system control.

### Secondary — Python
Python will support the engineering workflow through:
- Serial communication tools
- Automated testing
- Data logging and analysis
- Plotting sensor data
- Computer vision
- Raspberry Pi projects
- Robotics scripting
- Development utilities

The goal is not to replace C/C++ with Python, but to become comfortable using both where each language is strongest.

## First Major Build

### Custom ESP32 Robotic Vehicle

The first project in this stage will be a custom robotic vehicle designed as a platform for learning robotics, firmware architecture, FreeRTOS, sensors, power systems, and eventually PCB design.

Initial target features:
- ESP32 controller
- Two-motor drive system
- Motor driver
- Distance sensing
- Manual control mode
- Autonomous obstacle-avoidance mode
- Battery operation
- Modular wiring
- Structured C/C++ firmware
- Serial debugging

Later versions can add:
- FreeRTOS task architecture
- Wheel encoders
- IMU
- OLED status display
- Wi-Fi or Bluetooth control
- Battery monitoring
- Custom PCB
- Data logging

## Repository Structure

As projects are built, this repository will contain planning notes, experiments, architecture documentation, and engineering progress. Larger completed builds may receive their own dedicated repositories once they become substantial enough to stand alone.

Suggested structure:

```text
Engineering-Systems-Lab/
├── robotics/
├── freertos/
├── pcb-design/
├── power-systems/
├── firmware/
├── python-tools/
├── notes/
└── README.md
```

## Project Standard

Major projects should document:

1. Problem or goal
2. Requirements
3. System architecture
4. Parts and component selection
5. Wiring or schematic
6. Firmware structure
7. Build process
8. Testing
9. Problems and debugging
10. Results
11. Photos or video
12. Reflection and next improvements

## Current Status

**Stage 2 started — September 2026**

The embedded-learning phase is complete. The focus now is fewer, larger, more original engineering systems with stronger technical depth and better documentation.

The goal is to move from following examples to designing systems I can explain, modify, troubleshoot, and take ownership of from idea to working prototype.
