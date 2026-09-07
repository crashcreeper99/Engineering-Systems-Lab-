# Hoverboard Motor Diagnostic Bench

**Status:** Planned / In Progress  
**Week:** September 7, 2026

## Project Goal

Build a safe low-voltage ESP32 diagnostic setup for studying the Hall-effect sensor outputs from a hoverboard BLDC wheel motor while the wheel is rotated manually.

This is the first project in this repository that directly connects my embedded-systems work to the kind of repair, modification, and custom-build work I want to explore through JoyraTech.

## Safety Scope

This first version is intentionally limited to low-voltage diagnostics.

**I will not connect the ESP32 to:**

- The hoverboard battery
- Motor phase wires
- High-current motor power wiring
- Any unknown high-voltage connector

The hoverboard drive battery will remain disconnected while the diagnostic circuit is being built and checked.

The ESP32 will only monitor the motor's low-voltage Hall-sensor signals.

## How the Motor Works

A typical hoverboard wheel uses a brushless DC (BLDC) motor. Instead of brushes mechanically switching current, the motor controller electronically commutates the motor phases.

Hall-effect sensors inside the wheel help the controller determine rotor position.

```text
Rotor turns
   |
   v
Magnetic field changes
   |
   v
Hall sensors switch
   |
   v
H1 / H2 / H3 pattern
   |
   v
Controller determines rotor position
```

A healthy three-Hall sequence may cycle through six states such as:

```text
001
101
100
110
010
011
```

The exact direction/order can differ with motor wiring and rotation direction. States such as `000` or `111` may indicate a wiring, power, sensor, or interpretation problem and will be investigated rather than assumed to be valid.

## Planned Hardware

- ESP32 DEVKIT V1
- Hoverboard BLDC wheel motor
- Breadboard
- Jumper wires
- Multimeter
- Appropriate low-voltage Hall-sensor supply after wire identification
- Pull-up resistors if required by the Hall sensor outputs

## Planned Workflow Before Wiring

I will not guess the motor wire functions by color alone.

1. Identify the motor connector groups.
2. Keep the high-current phase wires isolated.
3. Identify the low-voltage Hall-sensor connector.
4. Use documentation and/or a multimeter to confirm ground, Hall supply, and signal wires.
5. Verify the Hall signal voltage is safe for the ESP32 before connecting any GPIO.
6. Only then connect the three Hall signals to GPIO inputs.

## Planned ESP32 Signal Connections

The exact motor wire colors will be documented only after they are verified.

Planned GPIO assignments:

| Signal | ESP32 |
|---|---|
| Hall A | GPIO 25 |
| Hall B | GPIO 26 |
| Hall C | GPIO 27 |
| Hall Ground | ESP32 GND / common low-voltage ground |

The Hall supply connection will depend on the verified requirements of the specific motor sensor assembly. I will not assume it is 3.3 V or 5 V without checking first.

## Planned Firmware Behavior

The ESP32 will:

1. Read Hall A, Hall B, and Hall C as digital inputs.
2. Combine them into a three-bit rotor-state value.
3. Print state transitions to Serial.
4. Detect whether the wheel is producing a repeating six-state sequence.
5. Flag suspicious states such as `000` and `111`.
6. Count transitions as the wheel is rotated manually.
7. Later estimate rotational speed from transition timing if the basic diagnostic works reliably.

Example output:

```text
Hall state: 001
Hall state: 101
Hall state: 100
Hall state: 110
Hall state: 010
Hall state: 011
Sequence repeated
```

## Concepts I Want to Learn

- BLDC motor architecture
- Hall-effect position sensing
- Digital signal diagnostics
- Binary state representation
- State transitions
- Safe separation of logic-level electronics from power electronics
- Using a multimeter before connecting unknown hardware
- How embedded diagnostics can support repair and modification work

## Why This Project Matters

Before attempting to control or modify a mobility motor, I need to understand the hardware and learn how to diagnose it safely.

This project is therefore not a motor-controller project yet. It is a diagnostic and learning platform that can lead toward future work such as:

- Wheel-speed measurement
- Direction detection
- BLDC controller diagnostics
- Motor-controller interfaces
- Scooter or bike instrumentation
- Mobility-system restoration
- JoyraTech custom builds

## Planned Testing

- Confirm the battery and phase wiring remain isolated from the ESP32 circuit.
- Verify Hall-sensor supply and signal levels with a multimeter.
- Rotate the wheel slowly by hand.
- Record the Hall sequence in one direction.
- Rotate it in the opposite direction and compare the reversed sequence.
- Check whether each Hall channel switches between logical states.
- Look for stuck or missing Hall states.
- Repeat the test to verify consistent behavior.

## Completion Criteria

I will mark this project complete only after I can explain:

- The difference between motor phase wires and Hall-sensor wires
- Why the ESP32 must stay isolated from the hoverboard battery and high-current motor wiring in this project
- What the three Hall sensors tell the controller
- How the binary Hall sequence changes as the rotor moves
- How a failed Hall sensor could be identified from the data
- What additional electronics would be required before attempting actual BLDC motor control

## Reflection

Not written yet. I will add the reflection only after I inspect the real motor, verify the wiring, collect Hall-state data, troubleshoot the system, and document what actually happened.
