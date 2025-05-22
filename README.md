# Live Spectrum & Waterfall Scanner

A comprehensive GNU Radio Companion (GRC) flowgraph and supporting Python script for real-time visualization, demodulation, and recording of the NOAA APT downlink at 137.1 MHz. This project demonstrates the full software-defined radio pipeline—from RF capture to image decoding—and serves as a teaching and research demonstration.

---

## Table of Contents
1. [Project Overview](#project-overview)  
2. [Hardware Requirements](#hardware-requirements)  
3. [Software Requirements](#software-requirements)  
4. [Flowgraph Architecture](#flowgraph-architecture)  
5. [Installation & Setup](#installation--setup)  
6. [Running the Project](#running-the-project)  
7. [Generated Files](#generated-files)  
8. [Data Analysis & Presentation](#data-analysis--presentation)  
9. [Coursework & Academic Context](#coursework--academic-context)  
10. [Challenges & Tuning](#challenges--tuning)  
11. [Future Work](#future-work)  
12. [References & License](#references--license)  

---

## Project Overview
Use an RTL-SDR dongle and GNU Radio Companion to:
- **Tune** to the NOAA APT SSTV downlink at **137.1 MHz**
- **Visualize** incoming RF:
  - Instantaneous FFT (**Live Spectrum**)
  - Scrolling time-history **Waterfall**
- **Demodulate** FM-encoded SSTV audio
- **Record** raw I/Q samples and decoded audio
- **Decode** audio into weather images with an external SSTV decoder

This end-to-end SDR example is ideal for labs, demonstrations, or prototype development.

---

## Hardware Requirements
- **RTL-SDR USB dongle** (e.g., RTL2832U)  
- **VHF antenna** (whip or patch, tuned near 137 MHz)  
- **PC** with GNU Radio and Python support (Linux/macOS/Windows)  

---

## Software Requirements
- **GNU Radio Companion** (version ≥ 3.7) with Osmocom module  
- **Python 3.7+**  
- **Optional:** SSTV decoder (e.g., QSSTV, WXtoImg) for weather image reconstruction  

---

## Flowgraph Architecture
```text
Osmocom Source
   ↓
FIR Low-Pass Filter (2.4 MHz → 100 kHz)
   ↙       ↘       ↘       ↘
FFT Sink  WF Sink  File Sink  Quadrature Demod
                             ↓
                   Multiply Const_ff → Rational Resampler_ff
                                      ↙                ↘
                                Audio Sink         WAV File Sink
