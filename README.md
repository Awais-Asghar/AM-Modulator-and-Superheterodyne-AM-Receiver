# AM Modulator and Superheterodyne AM Receiver

![Project Status](https://img.shields.io/badge/status-Completed-brightgreen.svg)
![Platform](https://img.shields.io/badge/platform-Proteus-blue.svg)
![Environment](https://img.shields.io/badge/environment-Proteus%208-orange.svg)
![Language](https://img.shields.io/badge/language-Circuit%20Design-blue.svg)

## Overview

This project implements an **Amplitude Modulation (AM)** transmitter and a corresponding **Superheterodyne AM receiver** for the **medium-wave (MW)** band (535 kHz – 1605 kHz). The entire design and testing were performed in **Proteus 8**, using discrete electronic components (resistors, capacitors, inductors, diodes, MOSFETs) and frequency down-conversion to 455 kHz IF, and signal recovery via envelope detection.

## Objective

- Design a MOSFET‑based AM transmitter that modulates a 120 kHz message onto a 1.2 MHz carrier.  
- Build a Superheterodyne receiver that down‑converts the incoming 1.2 MHz AM signal to a 455 kHz IF, then recovers the original audio via an envelope detector.  
- Verify and visualize each stage—message, carrier, modulated RF, IF, and demodulated output—using Proteus’s oscilloscope.

## Key Components & Circuit Design

### AM Transmitter
- **Carrier Frequency**: 1.2 MHz (displayed at 12 MHz in Proteus for clearer oscilloscope traces)  
- **Message Signal**: 120 kHz sine wave from VSM Signal Generator  
- **Modulator Topology**: Common‑source MOSFET (2N7000) with passive bias network  
  - Gate bias network: 10 kΩ & 100 kΩ resistors  
  - RF coupling capacitor: 0.01 µF (gate to carrier source)  
  - Drain resistor: 4.7 kΩ 
![Image](https://github.com/user-attachments/assets/3628669a-d90d-4f47-a269-ad5acaa6bd33)
 
- **RF Amplifier Stage**:  
  - LC tank tuned to 1.2 MHz (L = 10 µH, C = 100 pF)  
  - Common‑source MOSFET amplifier for post‑modulation gain
![Image](https://github.com/user-attachments/assets/b9922307-e24a-42e2-91cd-8d2ad0e109b3)

### Superheterodyne Receiver

1. **RF Front End**  
   - Band‑pass LC filter centered at 1.2 MHz (L = 10 µH, C = 120 pF)  
   - Low-noise MOSFET amplifier for initial RF gain  
![Image](https://github.com/user-attachments/assets/597067c4-a193-4bc0-b2c5-4482c2ccdbc8)

2. **Mixer / Frequency Converter**  
   - Local Oscillator: 1.655 MHz (to mix 1.2 MHz → 455 kHz IF)  
   - Mixer implemented with a diode ring (or single‑balanced MOSFET mixer)  
   - Output filtered to isolate 455 kHz IF  
![Image](https://github.com/user-attachments/assets/bf07db12-8c6a-4455-ace5-c32f63dd4de3)

3. **IF Amplifier**  
   - Tuned LC amplifier at 455 kHz (L = 100 µH, C = 1000 pF) for selectivity and gain  

4. **Envelope Detector**  
   - Diode (1N4148) + RC network (R = 10 kΩ, C = 0.1 µF)  
   - Recovers the 120 kHz message envelope → baseband audio  
![Image](https://github.com/user-attachments/assets/5baf8967-a05a-4ae6-becd-8c2a8f1403d4)

4. **Complete Circuit**  
![Image](https://github.com/user-attachments/assets/8ec238d6-2679-4350-922c-90df28a32688)

## Simulation Environment
- **Tool**: Proteus 8 (Version 8.x or higher)  
- **Key Instruments**: Virtual Signal Generator (VSM), Virtual Oscilloscope  
- **Carrier Display Workaround**: Proteus oscilloscope struggled to show a clean 1.2 MHz trace, so all “carrier” screenshots were taken at 12 MHz, though component values are calculated for 1.2 MHz.
![Image](https://github.com/user-attachments/assets/b2f563fd-a417-45a9-a5ba-26f53610ff0d)

## Results (Oscilloscope Captures)

| Stage                  | Frequency Shown | Observations                                      |
|------------------------|-----------------|---------------------------------------------------|
| Message Input          | 120 kHz         | Clean sine wave from VSM generator                |
| Carrier (displayed)    | 12 MHz          | Stable sinusoid (actual tuned to 1.2 MHz)         |
| AM Modulated Output    | 12 MHz          | Envelope follows 120 kHz message                   |
| IF Signal After Mixer  | 455 kHz         | Clean IF sine wave, ready for IF amplifier         |
| Demodulated Audio      | 120 kHz (envelope) | Recovered baseband envelope after RC filter      |

![Image](https://github.com/user-attachments/assets/50b7cf3d-c1e0-489e-9097-c1ff1a3f25dc)

- **Modulation Depth**: Approximately 80 – 90%  
- **IF Selectivity**: Good rejection of unwanted mixer products  
- **Audio Recovery**: Envelope detector output matches original 120 kHz message envelope

---
