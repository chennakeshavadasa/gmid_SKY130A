# SKY130 gm/ID Explorer

An interactive, browser-based gm/ID characterisation tool for the **SkyWater SKY130** open-source 130nm CMOS PDK.

### 🔗 Website

Open the tool in your browser. Copy the URL below:

```
https://nithinpuru.github.io/gmid/sky130a/
```

All PDKs (SKY130A, GF180MCU-D, IHP SG13G2):

```
https://nithinpuru.github.io/gmid/
```

> ⚠️ **Note:** The PDK Reference panel is a summary and may contain inaccuracies. Always check values against the official [SkyWater PDK documentation](https://skywater-pdk.readthedocs.io) before relying on them.

---

## What is this?

This tool lets you explore the gm/ID characteristics of 7 MOSFET variants in the SKY130 PDK directly in your browser. You don't need Python, MATLAB or a local install.

Derived from simulation data in [chennakeshavadasa/gmid_SKY130](https://github.com/chennakeshavadasa/gmid_SKY130), converted into a fully interactive Plotly dashboard with a comprehensive PDK reference panel pulled from the official [skywater-pdk documentation](https://skywater-pdk.readthedocs.io).

---

## Features

### 📋 PDK Reference Panel
- Full explanation of all 7 MOSFET variants: LVT / SVT / HVT flavours and HV (5V/10.5V) devices
- Explanation of what LVT, SVT, HVT actually mean in SKY130 (same gate oxide, different Vt-adjust implants)
- Why `nfet_01v8_hvt` does NOT exist in SKY130 (only PMOS HVT)
- HV device explanation — why `g5v0d10v5` is an extended-drain DMOS, not just a thick-oxide FET
- EP electrical specs: Vth₀, SubVt slope, Ioff, Vds limits for all devices
- 7-corner guide: TT / SS / FF / SF / FS / leak / wafer
- Instance parameter limits (Wmin, Lmin) — PMOS Lmin=0.35µm vs NMOS 0.15µm
- Designer's quick-reference cheatsheet

### 📈 gm/ID Explorer
- **7 device variants:** NMOS/PMOS SVT/LVT/HVT + HV family
- **7 interactive Plotly plots:**
  - gm/ID vs Vgs
  - gm/ID vs Vov (= Vgs − Vth)
  - gm/gds vs gm/ID (intrinsic gain)
  - ID/W vs gm/ID (normalised current density)
  - fT vs gm/ID (transit frequency)
  - Cgd/Cgg vs gm/ID
  - Cgs/Cgg vs gm/ID
- **Overview mode** — 6 plots simultaneously
- **Channel length filter** — per-L toggle or quick All/Short/Long
- **Log scale** toggles for X and Y
- **PNG export** of any plot

---

## Device Summary

| Dataset name | PDK model | Type | Vdd | Lmin | Vth₀ typ | Notes |
|---|---|---|---|---|---|---|
| NMOS_01v8_SVT | nfet_01v8 | NMOS SVT | 1.8V | 0.15µm | ~0.49V | Standard workhorse |
| NMOS_01v8_LVT | nfet_01v8_lvt | NMOS LVT | 1.8V | 0.15µm | ~0.40–0.45V | Low-Vt, higher speed |
| PMOS_01v8_SVT | pfet_01v8 | PMOS SVT | 1.8V | 0.35µm | ~0.60–0.65V | Standard PMOS |
| PMOS_01v8_LVT | pfet_01v8_lvt | PMOS LVT | 1.8V | 0.35µm | ~0.52V | Low-Vt PMOS |
| PMOS_01v8_HVT | pfet_01v8_hvt | PMOS HVT | 1.8V | 0.35µm | ~0.74V | Low-leakage, power gating |
| NMOS_g5v0d10v5 | nfet_g5v0d10v5 | NMOS HV | 5V/10.5V | 0.5µm | ~0.78–0.85V | Extended drain DMOS |
| PMOS_g5v0d10v5 | pfet_g5v0d10v5 | PMOS HV | 5V/10.5V | 0.5µm | ~0.90–1.0V | Extended drain DMOS |

---

## Data Source

Simulation data: **[chennakeshavadasa/gmid_SKY130](https://github.com/chennakeshavadasa/gmid_SKY130)**  
ngspice DC sweeps (Vgs step 0.1 mV, W = 2 µm) across 7 device variants and 11–13 channel lengths each.

PDK documentation: **[skywater-pdk.readthedocs.io](https://skywater-pdk.readthedocs.io)**  
Apache 2.0 licensed. © SkyWater Technology / Google.

---

## Technical Notes

- 400 points per curve, uniformly downsampled from 17.5k–49.5k raw points. This is visually lossless for smooth gm/ID curves.
- Single `index.html` with the data embedded. It loads Plotly.js v2.27.0 from a CDN and needs no backend.
- Total file size: ~3.5 MB
- To run it locally, download `index.html` and open it in a browser (internet access is needed for Plotly).

---

## License

Tool code: **MIT License**  
Simulation data: see [original repo](https://github.com/chennakeshavadasa/gmid_SKY130)  
PDK specs: Apache 2.0 © SkyWater Technology / Google

---

## Related

- [gm/ID Explorer (all PDKs)](https://nithinpuru.github.io/gmid/): SKY130A, GF180MCU-D and IHP SG13G2
- [GF180MCU gm/ID Explorer](https://github.com/chennakeshavadasa/gmid_GF180MCUD): the same tool for the GF 180nm MCU PDK
- [gmid_SKY130](https://github.com/chennakeshavadasa/gmid_SKY130): raw simulation data, Xschem testbenches and Python plotting scripts

---

*Built for the open-source silicon community. ⭐ the repo if useful.*
