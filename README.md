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
| Input amplifier | LMH6629MF/NOPB | Amplifies the filtered RF input signal. |
| Comparator | TLV3601DBVR | Converts the amplified analog signal into clock pulses. |
| Frequency divider | SN74LVC1G80 | Divides the comparator output frequency by two before counting by the microcontroller. |
| Voltage reference | REF2033 | Provides the 1.65 V reference for analog biasing and the comparator threshold. |
| Voltage regulator | AP2112K-3.3 | Provides the regulated 3.3 V supply. |
| Crystal | ABM3B-16.000MHZ-10-1-U-T | Provides the external 16 MHz clock reference for the microcontroller. |
| USB-C connector | USB4105-GF-A | Provides power and USB connectivity. |
| USB ESD protection | USBLC6-2SC6 | Protects the USB data lines against electrostatic discharge. |
| RF input connector | 50 Ω SMA | Connects the measured signal to the RF input filter. |
| Display | I2C OLED module | Displays measurement results. |

This list covers the main components. Refer to the KiCad schematic for passive components, supporting circuitry, and exact part variants.
