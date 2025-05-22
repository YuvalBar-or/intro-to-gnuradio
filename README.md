# Live Spectrum & Waterfall Scanner

A comprehensive GNU Radio Companion (GRC) flowgraph and supporting Python script for real-time visualization, demodulation, and recording of the NOAA APT downlink at 106 MHz. This project demonstrates the full software-defined radio pipeline—from RF capture to image decoding—and serves as a teaching and research demonstration.
---

## Project Overview
Use an RTL-SDR dongle and GNU Radio Companion to:
- **Tune** to the NOAA APT SSTV downlink at **106 MHz**
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
- **PC** with GNU Radio and Python support (Linux/macOS/Windows)  

---

## Software Requirements
- **GNU Radio Companion** (version ≥ 3.7) with Osmocom module  
- **Python 3.7+**  
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
