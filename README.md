# Rocket Motion Sensing Board — Gaucho Rocket Project

## Overview

This project was developed as part of the onboarding process for Gaucho Rocket Project (GRP). The goal was to design a custom PCB for a rocket motion sensing system capable of collecting inertial measurement data, such as acceleration and angular velocity, and transmitting it wirelessly to other systems.

The board integrates an STM32F446RE microcontroller, an ESP32, an MPU6050 IMU, and an ICM20948 IMU. The STM32 interfaces with both IMUs over I²C and sends the collected sensor data to the ESP32 over UART. This is because the ESP32 is intended to send that data wirelessly to other systems.

Although I had prior experience using KiCad, this was my first project in which I designed most of the schematic and PCB layout independently. It gave me an opportunity to apply what I already knew while developing a deeper understanding of datasheets, circuit implementation, and PCB layout.

## System Architecture

The design consists of four main components:

- **STM32F446RE:** Reads from both IMUs over I²C and forwards sensor data to the ESP32.
- **ESP32:** Receives data from the STM32 over UART and sends that data wirelessly.
- **MPU6050:** Provides accelerometer and gyroscope measurements.
- **ICM20948:** Provides additional inertial measurements.

The board also includes voltage regulation, supporting power circuitry, and connections for programming the STM32 through its Serial Wire Debug (SWD) interface.

## Design Process

The main components were specified by the onboarding assignment, so my focus was on implementing their connections and integrating them into the schematic and PCB layout.

I first used tutorials and the onboarding materials as references for parts of the schematic, particularly the STM32 circuitry. I also consulted the component datasheets to better understand the requirements behind the circuit configurations and the supporting components. Once the schematic was designed, I moved to the PCB layout.

## Schematic
<img width="533" height="361" alt="GRP Onboarding Schematic" src="https://github.com/user-attachments/assets/fb3229c0-14b6-403b-ad11-c70f0af1eff7" />

## PCB Design Considerations

### Component Placement and Routing

My main goal during PCB layout was to keep the design as simple and straightforward as possible. I wanted component placement and trace routing as efficient as possible by keeping the traces routes as short and straight as possible and keeping components that have connecting traces as close to each other as possible. This way, the board can be cleaner and more organized to reduce unwanted effects like parasitic inductance and capacitance. During the layout process, I tried to consider how each component would connect to the rest of the circuit when deciding where to place it.

For example, when laying out the STM32's crystal oscillator (Y1), I positioned the supporting capacitor (C10) along the route between the oscillator and the STM32 so that the connections could be routed naturally without unnecessary detours. I applied the same general approach throughout the board, placing related components close together, keeping the STM32 and ESP32 positioned with their UART connections in mind, and minimizing vias between PCB layers.

<img width="194" height="293" alt="layout consideration example" src="https://github.com/user-attachments/assets/e55a100f-e2a4-40c8-93fb-62b5a5eb968f" />

I also considered power distribution while arranging components and routing traces, including the placement of voltage regulators and the trace widths used for different power nets. I placed the majority of the capacitors close to their corresponding pins on the microcontrollers, IMUs, or regulators to help reduce parasitic inductance in the paths and support stable power delivery.

Overall, I approached the layout largely considering component placement and routing, aiming for a compact, organized board where the connections were as direct as possible and the supporting circuitry was positioned around the components it served.

### Firmware Programming Access

I included access to the STM32's SWDIO and SWCLK pins by adding connector pins that connects to them to support firmware flashing and debugging through the Serial Wire Debug interface, provides a way to program the microcontroller.

## Final PCB Layout
<img width="502" height="366" alt="GRP Onboarding PCB layout" src="https://github.com/user-attachments/assets/80f96eea-44bf-441c-9634-e8d52f54676c" />

## Project Status and Future Work

The schematic and PCB layout were completed in KiCad, but the board was not manufactured or tested. Its electrical performance and functionality have therefore not been validated on physical hardware.

Future work would include reviewing the design against component datasheets and PCB design rules, manufacturing the board, and testing the power supplies, sensor interfaces, UART communication, wireless data path, and overall functionality of the PCB.

## Lessons Learned

This process helped me connect schematic-level decisions to the physical constraints of PCB design. Since this was the first PCB I designed primarily myself, I gained experience balancing component placement and routing, considering power distribution and decoupling, and providing programming access for firmware development.

It also gave me a better appreciation for how initial component placement affects routing complexity and how datasheets can guide hardware implementation and what the overarching design of a PCB would be since datasheets tell exactly what the supporting circuitry for a component is, what the power requirements are, and what the components are capable of.

## Tools and Interfaces

- **KiCad:** Schematic capture and PCB layout
- **I²C:** Communication between the STM32 and IMUs
- **UART:** Communication between the STM32 and ESP32
- **SWD:** STM32 firmware programming and debugging

## 3D PCB View
<img width="574" height="338" alt="GRP Onboarding 3D view" src="https://github.com/user-attachments/assets/8b4b457c-0f4b-44c7-908a-77fb2f88fa36" />

