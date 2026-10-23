# Cutting Force Dynamometer Lab

Browser-based educational simulator of a three-component piezoelectric cutting-force dynamometer (modelled on a Kistler 9257B-type instrument) in a CNC vertical milling setup. It answers: *How does a piezoelectric dynamometer measure cutting forces, and how do cutting parameters influence the measured forces?*

All force data produced by the simulator are **simulated**, not experimental measurements.

## Files

| File | Purpose |
|---|---|
| `index.html` | Complete standalone application (HTML + CSS + JavaScript). Open it directly or host it on GitHub Pages. |
| `README.md` | This documentation: deployment, architecture, equations, assumptions. |

No build step and no backend. Three.js r128 is loaded from jsDelivr; fonts from Google Fonts (optional, with fallbacks).

## Deploy on GitHub Pages

1. Create a public repository, e.g. `dynamometer-lab`.
2. Upload `index.html` and `README.md` to the repository root (web UI: *Add file → Upload files*, or `git push`).
3. *Settings → Pages → Build and deployment → Source: Deploy from a branch*. Choose `main` and `/ (root)`. Save.
4. After about a minute the site is live at `https://<user>.github.io/dynamometer-lab/`.
5. To embed in Moodle/URLearn, add a *URL* resource pointing to that address (or an iframe in a Page resource, height ≈ 1600 px).

Local use: double-click `index.html` (internet needed once for Three.js), or serve the folder with `python -m http.server`.

For offline labs, download `three.min.js` and `OrbitControls.js` (version 0.128.0) next to `index.html` and change the two `<script src>` lines to local paths.

## Architecture (independent modules inside `index.html`)

| Module | Responsibility | Depends on |
|---|---|---|
| 1 `Model` | Specifications, material coefficients, kinematics, mechanistic milling force model, steady statistics. Pure JS. | — |
| 2 `Chain` | Measurement chain: 2nd-order structure, crosstalk, quartz charge, offset/drift/noise, charge amplifier, saturation, low-pass filter. | Model |
| 3 `Sim` | Simulation clock at 100 kHz internal rate; tool rotation and feed; sampling at fs with 16-bit ADC; ring buffer. | Model, Chain |
| 4 Plotting | Canvas plots (force–time, spectrum, trials, sweep). No chart library required. | — |
| 5 `Scene3D` | Three.js bench: machine, spindle/tool, dynamometer with four sensors, workpiece, cable, charge amplifier, DAQ, monitor; anatomy views, deflection, vectors, force path, picking. | Sim (read-only) |
| 6 Content | Component notes, constants table with categories, sources. | — |
| 7 UI | Guided procedure (13 steps), free mode, parameter controls, dashboard, export. | all |
| 8 Experiment log | `localStorage` trials, CSV export, parameter sweep. | Model |
| 9 Assessment | 14 concept questions, 4 simulator-based tasks, scoring, report. | Sim, Model |

To split into files for a larger project: move each module into `js/<module>.js` in the order above and load them as plain scripts; the modules communicate only through the objects named in the table.

## Equations

Kinematics

```
N    = 1000 · Vc / (π · D)        rpm
Vf   = N · z · fz                 mm/min
f_TP = N · z / 60                 Hz (tooth-passing frequency)
```

Mechanistic force model (Altintas, 2012)

```
φ_j(θ, z) = θ + j·2π/z_t − (tan β / R)·z
h(φ)      = fz · sin φ,                      φst ≤ φ ≤ φex
dFt = (Ktc·h + Kte)·dz   dFr = (Krc·h + Kre)·dz   dFa = (Kac·h + Kae)·dz
Fx  = Σ(−dFt cos φ − dFr sin φ)   Fy = Σ(dFt sin φ − dFr cos φ)   Fz = Σ dFa
up milling:   φst = 0,                φex = acos(1 − ae/R)
down milling: φst = π − acos(1 − ae/R), φex = π
slot:         φst = 0,                φex = π
F_workpiece = −F_tool,   Fr = √(Fx² + Fy² + Fz²)
```

Summation over teeth and 8 axial discs; a tooth contributes only while it is inside the workpiece (entry/exit transients).

Measurement chain

```
Structure   G(s) = ωn² / (s² + 2ζωn s + ωn²)   per axis (bilinear biquad)
Crosstalk   F' = C · F
Charge      Q  = S · F' + Q_offset + Q_drift + noise
Amplifier   V  = Q / (S · range),  clipped at ±10 V   (ideal: V = −Q/Cf)
Filter/ADC  2nd-order Butterworth at fc, sampled at fs, 16-bit
Displayed   F  = V · range
```

Per-sensor vertical loads (educational): `Fz,i = Fz/4 + Mx·yi/(4b²) − My·xi/(4a²)` with moments about the sensor plane.

## Categories of information

**A — Verified manufacturer specifications** (Kistler 9257B product page): cover plate 170 × 100 mm; range Fx, Fy ±5 kN, Fz −5…+10 kN; sensitivity −7.5, −7.5, −3.7 pC/N (nominal); natural frequency ≈ 3.5 kHz (sensor, free); stiffness Cx, Cy 1 kN/µm; Fischer 9-pin flange connector; preloaded sensors.

**B — Engineering equations and referenced data**: equations above; Al7050-T7451 coefficients Ktc 796, Krc 168.8, Kac 222 N/mm², Kte 27.7, Kre 30.8, Kae 1.8 N/mm (Altintas); quartz d11 ≈ 2.3 pC/N.

**C — Educational assumptions**: Al7050 coefficients used as a proxy for Al6061; mild-steel and 316L coefficients are illustrative; dynamometer height, internal sensor geometry and positions; Cz = 2 kN/µm; ζ = 0.03; mounted fn adjustable; crosstalk matrix; residual offset, drift (exaggerated) and noise; ADC; workpiece size; ×10 visual compression of tool travel (chip thickness unchanged); 30° helix.

Kistler calibration coefficients are never invented. A real instrument is used with its individual calibration sheet.

## Model limitations

No tool run-out, wear, tool/workpiece deflection, chatter, temperature, size effect or speed dependence of coefficients. Use the simulator for intuition and experiment planning; publish only calibrated measurements.

## Sources

- Kistler, *Multicomponent dynamometer, 5 kN, cover plate 100x170 mm / 9257B*, item 18007542. https://www.kistler.com/CH/en/p/multicomponent-dynamometers-9257b/000000000018007542
- Y. Altintas, *Manufacturing Automation*, 2nd ed., Cambridge University Press, 2012.
- IEEE Std 176-1987, *IEEE Standard on Piezoelectricity*.
