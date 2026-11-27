# STM32 Frequency Meter PCB

A four-layer KiCad board for measuring the frequency of periodic signals in the **50–100 MHz** range. A 50 Ω SMA input feeds an analog filter and amplifier. The STM32 counts pulses from that front end and is intended to show the result on a small OLED display.

| Design target | Value |
|---|---|
| Input frequency | 50–100 MHz |
| Minimum input amplitude | 10 mV peak (20 mV peak-to-peak for a sine wave) |
| Counter input after division | 25–50 MHz |
| Timebase | 16 MHz crystal |
| Power and data | 5 V from USB-C; USB 2.0 Full-Speed data lines routed to the STM32 |
| Display | 1.3-inch, 128 × 64 I²C OLED |

## Signal path

1. The signal enters through a 50 Ω edge-mount SMA connector and passes through a Butterworth LC band-pass filter designed for 50–100 MHz. A 49.9 Ω resistor terminates the filter output.
2. The LMH6629 amplifies the filtered signal. The REF2033 supplies a 1.65 V bias for the amplifier and comparison threshold.
3. The TLV3601 converts the amplified waveform into digital pulses. The SN74LVC1G80 divides the pulse rate by two before it reaches the STM32 on PA1.
4. The firmware is intended to count rising edges in a timed gate and calculate the input frequency as `f_in = 2 × counted_edges / gate_time`. With a 75 MHz input, the expected rate at PA1 is 37.5 MHz.

The board includes BOOT0 and RESET buttons, SWD access pads and test points for the comparator output, divided clock, reference and power rails.

## Key components

| Reference | Part | Role |
|---|---|---|
| IC1 | LMH6629MF/NOPB | RF amplifier |
| IC2 | SN74LVC1G80DBVR | Divide-by-two stage |
| IC3 | REF2033AIDDCT | 1.65 V bias output |
| IC4 | TLV3601DBVR | High-speed comparator |
| IC5 | USBLC6-4SC6 | USB data-line ESD protection |
| IC6 | STM32G431KBT6 | Timer-based pulse counting, USB and display control |
| U2 | AP2112K-3.3 | 3.3 V regulator |
| Y1 | ABM3B-16.000MHZ-10-1-U-T | External 16 MHz crystal |
| J1 | 50 Ω edge-mount SMA | RF input; PCB footprint based on Amphenol 132289 |
| J2 | USB4105-GF-A | USB-C power and data |
| DS1 | 1.3-inch, 128 × 64 I²C OLED | Display; header order: GND, 3.3 V, SCL, SDA |

The current PCB uses the **USBLC6-4SC6**. The board traces join pads 3 and 4 for D+ and pads 1 and 6 for D−; the four-channel protection device does not bridge those pairs internally.

## KiCad files

- [Project](pcb_design/Frequency_Meter.kicad_pro)
- [Schematic](pcb_design/Frequency_Meter.kicad_sch)
- [Four-layer PCB](pcb_design/Frequency_Meter.kicad_pcb)

Open the project in KiCad and use the schematic for passive component values and reference designators. Full library editing requires the local symbol and footprint libraries and their project library tables. Those files, along with the simulation workspaces and custom design rules, are excluded by the current `.gitignore`. If working from a clean clone, obtain the missing files separately and place the libraries where the tables expect them.

## Validation status

The schematic and four-layer layout are available. Transient simulations at **75 MHz and 10 mV peak** checked whether the front end still produced the expected pulse train in the presence of out-of-band interference. At **20 mV peak**, the tested interferers at **18, 21, 23 and 207 MHz** did not visibly add or remove pulses in the plotted windows. A stronger **207 MHz** interferer at **355 mV peak** produced extra transitions. These are simulation results for specific test cases, not a hardware interference limit.
