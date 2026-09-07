# Smart Access & Security Controller

**Status:** Planned / In Progress  
**Week:** September 7, 2026

## Project Goal

Build an ESP32-based access-control system that reads an RFID card, checks whether the UID is authorized, provides feedback on an OLED display, and controls a servo-based locking mechanism.

This is intentionally different from my earlier RFID attendance/check-in project. The purpose here is not to log who scanned a card, but to build a complete embedded control loop that makes a physical access decision.

## System Concept

```text
RFID Card
   |
   v
RC522 Reader
   |
   v
ESP32
   |
   +--> Validate UID
   |
   +--> OLED Feedback
   |
   +--> Servo Lock / Unlock
```

The default state will be locked. If an authorized UID is detected, the servo will move to the unlocked position for a short period and then automatically return to the locked position. Unauthorized cards will leave the system locked.

## Planned Hardware

- ESP32 DEVKIT V1
- MFRC522 / RC522 RFID reader
- SG90 servo
- SSD1306 128x64 I2C OLED
- Breadboard
- Jumper wires
- External 5 V supply for the servo

## Planned Wiring

### RC522 RFID Reader

| RC522 | ESP32 |
|---|---|
| SDA / SS | GPIO 5 |
| SCK | GPIO 18 |
| MOSI | GPIO 23 |
| MISO | GPIO 19 |
| RST | GPIO 27 |
| 3.3V | 3.3V |
| GND | GND |

> The RC522 will be powered from 3.3 V, not 5 V.

### OLED

| OLED | ESP32 |
|---|---|
| VCC | 3.3 V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

### Servo

| Servo | Connection |
|---|---|
| Signal | GPIO 13 |
| VCC | External 5 V |
| GND | Common ground with ESP32 |

The servo will use an external 5 V source instead of being powered directly from the ESP32. Grounds must be connected together.

## Planned Software Behavior

1. Start in the locked state.
2. Wait for an RFID card.
3. Read the UID.
4. Compare it with the authorized UID list.
5. If authorized:
   - Display `ACCESS GRANTED`.
   - Move servo to unlocked position.
   - Wait approximately 4 seconds.
   - Relock automatically.
6. If unauthorized:
   - Display `ACCESS DENIED`.
   - Keep the servo locked.
7. Return to waiting for the next scan.

## Firmware Concepts I Want to Practice

- SPI communication
- I2C communication
- Servo control
- Input validation
- State-based system behavior
- Safe default states
- Separating sensing, decision-making, output, and feedback
- Basic embedded security logic

## Why This Project Matters

This project moves beyond reading a sensor and displaying a value. It combines an input device, decision logic, physical actuator, and user interface into one complete embedded system.

The same architecture can later be adapted for cabinets, tool storage, equipment access, electronic locks, workshop systems, or other JoyraTech prototypes.

## Planned Testing

- Verify the RC522 consistently reads my authorized tag.
- Verify an unknown UID is denied.
- Confirm the servo starts locked after reset.
- Confirm authorized access unlocks and automatically relocks.
- Confirm the OLED displays the correct state.
- Test repeated scans.
- Verify the servo power supply does not cause ESP32 resets.

## Completion Criteria

This project will be marked complete only after I physically build and test it and can explain:

- How the UID is read
- How authorization is decided
- Why the system defaults to locked
- How the servo is powered safely
- How SPI and I2C are being used simultaneously
- What I would change for a real electronic lock

## Reflection

Not written yet. I will add a reflection after the physical build, testing, debugging, and any design changes are complete.
