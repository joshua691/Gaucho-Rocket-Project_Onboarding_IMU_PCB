# Rocket Motion Sensing Board — Gaucho Rocket Project

## Overview

This project was developed as part of the onboarding process for Gaucho Rocket Project. The goal was to design a custom PCB capable of collecting inertial measurement data and transmitting it to other systems wirelessly.

The board integrates an STM32F446RE microcontroller, an ESP32, an MPU6050 IMU, and an ICM-20948 IMU. The STM32 communicates with the IMUs over I²C and forwards the sensor data to the ESP32 over UART, allowing the ESP32 to handle wireless communication.

I designed the schematic and PCB layout in KiCad. Although I had prior experience using KiCad, this was my first project in which I independently developed most of the hardware design.

## System Architecture

- **Sensing:** The MPU6050 and ICM-20948 provide inertial measurements, including acceleration and angular velocity.
- **Sensor interface:** The STM32 communicates with both IMUs over I²C.
- **Data communication:** The STM32 forwards sensor measurements to the ESP32 over UART.
- **Wireless interface:** The ESP32 is responsible for transmitting data to other systems wirelessly.
- **Power management:** The design includes voltage regulation and supporting circuitry for the board's power requirements.

## Design Considerations

One aspect of the design was integrating multiple microcontrollers, sensors, and power circuits into a single PCB while accounting for component placement, routing, and the ESP32 antenna keep-out region.

This project gave me practical experience translating a system-level architecture into a schematic and PCB layout, connecting hardware interfaces across subsystems, and working through the constraints of a physical board design.

## Project Status

The schematic and PCB layout were completed in KiCad. The board was not manufactured, so its electrical performance and functionality have not been validated on physical hardware.

## Tools

- KiCad
- Embedded systems hardware design
- I²C and UART interface design
