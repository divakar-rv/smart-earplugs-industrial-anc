# Smart Earplugs for Industrial Noise Cancellation with Intelligent Classification

A prototype smart earplug system that suppresses harmful industrial noise while intelligently preserving critical sounds like alarms, sirens, and speech — combining embedded hardware, digital signal processing, and machine learning.

*Team project — collaborative work with Ram Kumar and SrineshKumar Subramanian.*

## Problem

Industrial workers are regularly exposed to hazardous noise levels (>85 dB), risking Noise-Induced Hearing Loss (NIHL) and accidents caused by missed alarms or voice commands. Conventional earplugs block all sound indiscriminately, while commercial ANC headphones are costly and not designed for industrial safety use. There's a gap for affordable, intelligent ear protection that suppresses harmful noise while still letting critical sounds through in real time.

## Objectives

- Protect workers from NIHL, temporary threshold shift (TTS), and acoustic trauma
- Preserve critical sounds — alarms, human voice, machine warnings
- Operate in real time with low latency on embedded hardware
- Deliver a cost-effective, portable prototype that integrates with existing safety equipment

## My Contribution

Worked across all three layers of the system:
- **ML / classification** — MFCC feature extraction and SVM-based classification to distinguish speech/alarms from harmful noise
- **DSP / filtering** — bandpass filtering and Wiener-filtering-based noise suppression
- **Embedded hardware** — ESP32 firmware integrating the MEMS microphone and DAC/amplifier, implementing spectral subtraction and FxLMS-based active noise cancellation

## System Architecture

```
Sound Signal → MEMS Microphone → Preamplifier & ADC → ESP32 Microcontroller
                                                              │
                                    ┌─────────────────────────┴─────────────────────────┐
                                    │                                                     │
                          ML: MFCC + SVM                                   ANC: FxLMS
                       (Alarm/Voice Detection)                        (Suppress Machine Noise)
                                    │                                                     │
                                    └─────────────────────────┬─────────────────────────┘
                                                              │
                                          Selective Pass-Through Logic
                                                              │
                                                    DAC & Amplifier
                                                              │
                                                        Ear Plugs
                                                              │
                                                      Worker's Ear
```

## Methodology

**Phase 1 — Simulation & ML Training (MATLAB/Python)**
- Recorded factory noise/alarms (dataset: MIMII) via microphone
- Removed DC offset, applied bandpass filtering focused on speech and alarm frequencies
- Applied Wiener-filtering-based techniques to suppress industrial noise
- Extracted MFCC features for speech/noise classification
- Saved feature vectors as input for the ML model

**Phase 2 — ESP32 Prototype**
- Connected MEMS microphone and headphone driver
- Implemented spectral subtraction / FxLMS algorithm for active noise cancellation

**Phase 3 — ML Integration**
- Merged Phase 1 and Phase 2 — final output passes alarms/speech through while cancelling background noise

## Hardware Components

| Component | Purpose |
|---|---|
| ESP32 Development Board | Main controller, DSP, ML inference |
| MEMS Microphone (I²S, e.g. INMP441) | Captures audio signal |
| DAC + Amp (MAX98357A / PAM8403) | Converts processed audio to output |
| Headphones/Earphones | Delivers audio to the user |
| Li-ion Battery (3.7V) + TP4056 | Portable power source |

## Software Tools

| Tool | Purpose |
|---|---|
| Arduino IDE | ESP32 programming (C/C++) |
| ESP32 I²S Library | Audio I/O for MEMS mic & DAC |
| ESP-DSP Library | DSP routines (filters, FFT, ANC) |
| MATLAB / Python | Offline processing, MFCC/spectrogram feature extraction, ML training |

## Author

Divakar V — B.Tech Electronics and Communication Engineering, VIT Chennai
