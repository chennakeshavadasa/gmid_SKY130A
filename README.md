# SKY130 gm/ID Explorer

An interactive, browser-based gm/ID characterisation tool for the **SkyWater SKY130** open-source 130nm CMOS PDK.

🔗 **Live demo:** [https://chennakeshavadasa.github.io/gmid_SKY130A](https://chennakeshavadasa.github.io/gmid_SKY130A)

---

---
Note: PDK Reference isnt accurate please be careful!!!

---

## What is this?

This tool lets you visually explore the gm/ID characteristics of 7 MOSFET variants in the SKY130 PDK directly in your browser — no Python, no MATLAB, no local install required.

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

## How to Deploy (GitHub Pages)

```bash
# Option A — use this as your gmid_SKY130 repo's gh-pages
git clone https://github.com/<you>/gmid_SKY130
cd gmid_SKY130
# copy index.html, README.md, LICENSE, .nojekyll here
git add index.html .nojekyll LICENSE
git commit -m "Add interactive gmid explorer"
git push

# Then: Settings → Pages → main branch → / (root) → Save
```

```bash
# Option B — standalone repo
git init && git add . && git commit -m "Initial deploy"
git remote add origin https://github.com/<you>/gmid_SKY130
git push -u origin main
# Then enable Pages in Settings
```

Site live at: `https://<you>.github.io/gmid_SKY130`

---

## Data Source

Simulation data: **[chennakeshavadasa/gmid_SKY130](https://github.com/chennakeshavadasa/gmid_SKY130)**  
ngspice DC sweeps across 7 device variants and 11–13 channel lengths each.

PDK documentation: **[skywater-pdk.readthedocs.io](https://skywater-pdk.readthedocs.io)**  
Apache 2.0 licensed. © SkyWater Technology / Google.

---

## Technical Notes

- 300 pts/curve (uniformly downsampled from 8k–42k raw points) — lossless for monotonic gm/ID curves
- Plotly.js v2.27.0 from CDN — fully self-contained, no backend needed
- Total file size: ~2.5MB

---

## License

Tool code: **MIT License**  
Simulation data: see [original repo](https://github.com/chennakeshavadasa/gmid_SKY130)  
PDK specs: Apache 2.0 © SkyWater Technology / Google

---

## Related

- [GF180MCU gm/ID Explorer](https://github.com/chennakeshavadasa/gmid_GF180MCUD) — same tool for GF 180nm MCU PDK

---

*Built for the open-source silicon community. ⭐ the repo if useful.*
