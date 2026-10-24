# STM32 Frequency Meter PCB

A custom frequency meter built around the STM32G431KBT6 microcontroller, combining an analog input stage, a four-layer PCB, and an OLED display in a compact embedded system.

## Repository Contents

KiCad project files, schematics and PCB layout.

## Project Status

The project is under development. Measurement range, accuracy, and input limits will be documented after hardware assembly and validation.

## Key components

| Component | Part / type | Role |
| --- | --- | --- |
| Microcontroller | STM32G431KBT6 | Frequency measurement, USB communication, and display control. |
| Input amplifier | AD8021ARZ | Amplifies the filtered RF input signal. |
| Comparator | AD8611ARZ | Converts the analog signal into clock pulses. |
| Frequency divider | 74LVC1G74DC,125 | Divides the clock frequency by two before the microcontroller counts it. |
| Voltage reference | REF3125AIDBZT | Provides the 2.5 V reference for analog biasing and the comparator threshold. |
| Voltage regulator | AP2112K-3.3 | Provides the 3.3 V supply for the digital circuitry and display. |
| Crystal | ABM3B-16.000MHZ-10-1-U-T | Provides the external 16 MHz clock reference for the microcontroller. |
| USB-C connector | USB4105-GF-A | Provides power and USB connectivity. |
| USB ESD protection | USBLC6-2SC6 | Protects the USB data lines against electrostatic discharge. |
| RF input connector | 50 Ω SMA | Connects the measured signal to the analog input stage. |
| Display | I2C OLED module | Displays measurement results. |

This list covers the main components. Refer to the KiCad schematic for passive components and supporting circuitry.
