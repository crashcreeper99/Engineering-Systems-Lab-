# FreeRTOS Multi-Sensor Control System

**Status:** Planned / In Progress  
**Week:** September 7, 2026

## Project Goal

Build a multitasking ESP32 system using FreeRTOS so sensing, distance measurement, and display updates run as separate tasks instead of being handled sequentially inside one large `loop()` function.

This is the main firmware-learning project for the week.

## System Concept

```text
                 ESP32 + FreeRTOS
                       |
        --------------------------------
        |              |               |
        v              v               v
 Temperature Task  Distance Task   Display Task
        |              |               |
        ---------------+---------------
                       |
                       v
               Shared System State
```

The system will continuously read temperature and humidity from a DHT22, measure distance with an HC-SR04 ultrasonic sensor, and show the current system state on an OLED display.

## Planned Hardware

- ESP32 DEVKIT V1
- DHT22 temperature/humidity sensor
- HC-SR04 ultrasonic distance sensor
- SSD1306 128x64 I2C OLED
- Breadboard
- Jumper wires
- Resistors for HC-SR04 Echo voltage divider

## Planned Wiring

### DHT22

| DHT22 | ESP32 |
|---|---|
| VCC | 3.3 V |
| DATA | GPIO 4 |
| GND | GND |

### HC-SR04

| HC-SR04 | ESP32 |
|---|---|
| VCC | 5 V |
| TRIG | GPIO 5 |
| ECHO | GPIO 18 through voltage divider |
| GND | GND |

The HC-SR04 Echo output can be near 5 V, so it will not be connected directly to an ESP32 GPIO.

Planned divider:

```text
HC-SR04 ECHO
     |
    1kΩ
     |
     +------> GPIO 18
     |
    2kΩ
     |
    GND
```

### OLED

| OLED | ESP32 |
|---|---|
| VCC | 3.3 V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

## Planned Task Architecture

### Temperature Task

- Read DHT22 temperature and humidity.
- Validate the sensor readings.
- Update shared system data.
- Run at a slower rate appropriate for the DHT22.

### Distance Task

- Trigger the HC-SR04.
- Measure Echo pulse duration.
- Convert the result to centimeters.
- Update shared system data several times per second.

### Display Task

- Read the latest shared sensor data.
- Show temperature, humidity, distance, and system status on the OLED.
- Display a warning when an object is closer than the selected threshold.

## Shared Data and Concurrency

The tasks will share a system-state structure containing values such as:

- Temperature
- Humidity
- Distance
- Sensor-valid flags

A FreeRTOS mutex will protect this shared data so multiple tasks do not read and modify it at unsafe times.

## Firmware Concepts I Want to Learn

- FreeRTOS tasks
- Task scheduling
- Task priorities
- `vTaskDelay()`
- Multicore ESP32 operation
- Shared data
- Mutexes / semaphores
- Concurrency
- Independent task timing
- Sensor validation
- System-state architecture

## Why This Project Matters

Many of my earlier ESP32 projects handled everything sequentially inside `loop()`. This project is meant to teach a more scalable firmware architecture that can later be reused in robots, monitoring systems, motor-control projects, and larger JoyraTech builds.

The important part is not simply connecting three devices. The goal is to understand why independent tasks are useful and how to share information safely between them.

## Planned Testing

- Confirm each sensor works independently before enabling all tasks.
- Confirm each task continues running at its intended rate.
- Verify invalid DHT22 readings are handled instead of displayed as real data.
- Verify timeout handling for the ultrasonic sensor.
- Confirm the OLED continues updating while other tasks run.
- Test the near-object warning threshold.
- Observe serial output to understand how the tasks interleave.

## Completion Criteria

I will mark this project complete only after I can explain:

- What a FreeRTOS task is
- Why the tasks do not need one shared loop timing
- What the scheduler does
- Why shared data needs protection
- What a mutex does
- Why the DHT and distance tasks use different update rates
- How I could expand the architecture for a robot or larger embedded system

## Reflection

Not written yet. I will write the reflection after building, testing, debugging, and experimenting with the task architecture.
