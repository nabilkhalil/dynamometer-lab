# Cutting Force Dynamometer Lab

**An interactive virtual lab for learning how cutting forces are measured in milling.**

You set up a virtual milling machine, mount a force sensor (a *dynamometer*) under the workpiece, cut metal, and watch the force signals appear live. Then you change the cutting conditions and see how the forces respond.

**▶ [Open the lab in your browser](https://nabilkhalil.github.io/dynamometer-lab/)**: nothing to install, works on any recent computer browser.

> **Note:** Every force value in this lab comes from a computer model. It behaves like a real instrument, but it is **not real measured data**. Don't cite these numbers as experimental results.

---

## What you will learn

By the end of a session you should be able to:

- Explain how a piezoelectric dynamometer turns a force into an electrical signal you can record.
- Set up a force measurement in the right order: mount, clamp, connect, configure, zero, cut.
- Read a force–time plot and pick out the pulse each tooth makes as it cuts.
- Predict how feed, depth of cut, tool and material change the cutting forces.
- Choose sensible measurement settings (sampling rate, filter, amplifier range) and spot what goes wrong when you don't.

---

## Quick start (5 minutes)

1. **Open the lab** using the link above. A 3D milling bench appears with force plots beside it.
2. Stay in **Guided learning** (the default tab at the top).
3. Click through the **13 steps** in order. Each step animates the bench and explains what you are doing and why.
4. At step 9, the tool starts cutting. Watch the **Fx, Fy, Fz** plots fill with force pulses.
5. Click **any part of the 3D model** (sensor, cable, amplifier, tool…) to read what it does.

That's it. Once you've done the guided run, try the other modes.

---

## The four modes

| Mode | Use it to… |
|---|---|
| **Guided learning** | Walk through the full measurement procedure step by step. Start here. |
| **Free exploration** | Skip the setup: the bench is ready to cut. Change any setting, even while cutting, and see what happens. |
| **Virtual experiment** | Plan and run a series of cuts, record each one as a *trial*, compare them on a chart, and export the results. |
| **Assessment** | Answer 14 concept questions and complete 4 hands-on tasks in the simulator, then generate a report for your instructor. |

---

## A tour of the screen

### 3D bench (top left)

- Drag to rotate, scroll to zoom. Camera buttons (**Iso, Front, Top, Dyno, Chain**) jump to useful viewpoints.
- View buttons let you look inside the dynamometer: **External, Transparent, Section, Exploded, Sensor,** and **Force path**, which shows how force travels from the tool to the sensors.
- **Deflection ×** exaggerates how much the dynamometer bends under load so you can see it. The real deflection is tiny: a few micrometres.
- **Force vectors** draws arrows for the forces acting on the workpiece.

### Control buttons

- **Start machining**: start or stop the cut.
- **New pass**: cut again from the start.
- **Reset / zero amplifier**: clear any leftover charge before cutting. Always do this before a measurement.

### Force plots

- One plot each for **Fx, Fy, Fz** (and the combined force **Fr**). The strip under each plot shows when a tooth is in contact with the metal.
- Tick **Overlay true model force** to see the "perfect" force as a dashed line. The gap between the two is the error added by the measurement equipment.

### Tabs at the bottom

| Tab | What's there |
|---|---|
| Cutting & chain parameters | All the settings: material, tool, speeds, feeds, and the measurement equipment. |
| Analysis | Mean / peak / RMS forces, the frequency spectrum, and an automatic interpretation of your signal. |
| Experiment log | Record trials, compare them, run a parameter sweep, export CSV files. |
| Assessment | Questions, tasks and the report generator. |
| Constants & sources | Every number the model uses, and where it comes from. |
| Theory | Short explanations of the physics and equations. |

---

## Settings you can change

### Cutting parameters

| Setting | Symbol | What it means | Range |
|---|---|---|---|
| Workpiece material | — | Aluminium 6061, mild steel, or stainless steel 316L | — |
| Tool diameter | D | Width of the end mill | 6–25 mm |
| Number of teeth | z | Cutting edges on the tool | 2–6 |
| Cutting speed | Vc | How fast the cutting edge moves through the metal | 20–600 m/min |
| Feed per tooth | fz | How far the tool advances each time one tooth cuts. Sets the chip thickness. | 0.01–0.3 mm |
| Axial depth of cut | ap | How deep the tool cuts (along the tool axis) | 0.5–12 mm |
| Radial width of cut | ae | How much of the tool's width is cutting | 0.5 mm – D |
| Tool engagement | — | **Full slot** (whole tool width cuts), **down milling** (climb), or **up milling** (conventional) | — |

### Measurement equipment

| Setting | What it does |
|---|---|
| Amplifier range | Force that gives full-scale output. Too small and the signal clips; too large and small forces get lost in noise. |
| Sampling rate fs | How many readings per second are recorded. |
| Low-pass filter fc | Removes high-frequency content above this frequency. |
| Mounted natural frequency fn | How stiff the dynamometer setup is. Heavy workpieces lower it. |
| Playback speed | Slows the animation so you can follow it. Doesn't change the forces. |

You can also switch real-world imperfections on and off: **structural vibration, crosstalk** between channels, **noise, charge drift,** and **skipping the amplifier reset**.

---

## Experiments to try

Each one takes a few minutes. Write down a prediction before you run it.

1. **Double the feed.** Change fz from 0.05 to 0.10 mm. Does the force double? (Hint: it rises, but by less than double. Why?)
2. **Count the pulses.** Change the number of teeth from 2 to 4. What happens to the number of force pulses per second? Check the peak in the Analysis spectrum.
3. **Up vs down milling.** Compare the two with the same ae. Which direction does the force point in each case?
4. **Speed it up.** Increase Vc. The pulses come faster, but does the force size change much in this model? (See *Model limitations* below.)
5. **Forget to zero.** Tick *Skip amplifier reset* and cut. What happens to the mean force?
6. **Sample too slowly.** Set fs to 2 kHz with a high-speed, many-tooth setup. Does the signal still look right?
7. **Change material.** Cut aluminium, then stainless steel, with the same settings. How much higher are the forces?

Use the **Parameter sweep** in the Experiment log to predict the trend instantly, then check it with real (simulated) cuts.

---

## Key terms

| Term | Plain-language meaning |
|---|---|
| **Dynamometer** | A force sensor placed under the workpiece. It measures the force in three directions at once. |
| **Piezoelectric** | Some crystals, such as quartz, produce an electric charge when squeezed. More force gives more charge. |
| **Charge amplifier** | Converts the tiny charge from the crystals into a voltage a computer can record. |
| **Fx, Fy, Fz** | Force components: Fx along the feed direction, Fy sideways, Fz along the tool axis. |
| **Fr** | Resultant (total) force: √(Fx² + Fy² + Fz²). |
| **Spindle speed N** | Tool revolutions per minute: N = 1000 · Vc / (π · D). |
| **Feed rate Vf** | How fast the table moves: Vf = N · z · fz (mm/min). |
| **Tooth-passing frequency** | How many times per second a tooth hits the metal: f = N · z / 60 Hz. The force signal repeats at this rate. |
| **Natural frequency** | The frequency at which the setup "rings" if struck. Cutting near it distorts the signal. |
| **Crosstalk** | A force in one direction showing up slightly on another channel. |
| **Drift** | Slow wandering of the signal caused by charge leaking away. |
| **Aliasing** | False, low-frequency patterns that appear when you sample too slowly. |

---

## Tips and troubleshooting

- **3D view doesn't appear?** The lab needs an internet connection the first time to load its 3D library. If the 3D view still fails, the plots, settings and analysis keep working. Try another browser (Chrome, Edge or Firefox).
- **Your trials are saved in this browser only.** Clearing browser data or switching computers erases them. Use **Export trials CSV** to keep a copy.
- **Exported CSV files** open in Excel, MATLAB or Python. Each file starts with lines that record the setup you used.
- **Use a laptop or desktop.** The lab works on tablets but is easier with a mouse and a larger screen.

---

## For instructors

### Hosting on GitHub Pages

1. In this repository go to *Settings → Pages*.
2. Under *Build and deployment*, choose *Deploy from a branch*, then `main` and `/ (root)`. Save.
3. After about a minute the lab is live at `https://<user>.github.io/dynamometer-lab/`.

**Adding it to Moodle / URLearn:** add a *URL* resource pointing to that address, or embed it with an iframe in a *Page* resource (height ≈ 1600 px).

**Running locally:** double-click `index.html`, or serve the folder with `python -m http.server`.

**Fully offline labs:** download `three.min.js` and `OrbitControls.js` (Three.js version 0.128.0), place them next to `index.html`, and change the two `<script src>` lines to the local file names.

### Files

| File | Purpose |
|---|---|
| `index.html` | The whole application (HTML, CSS and JavaScript). No build step, no server code. |
| `README.md` | This guide. |

---

## Under the hood (technical reference)

This section is for anyone who wants to check the model or extend the code.

### The instrument

The dynamometer is modelled on a **Kistler 9257B-type** three-component piezoelectric dynamometer on a CNC vertical milling machine.

### Equations

#### Kinematics

```
N    = 1000 · Vc / (π · D)        rpm
Vf   = N · z · fz                 mm/min
f_TP = N · z / 60                 Hz (tooth-passing frequency)
```

#### Mechanistic force model (Altintas, 2012)

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

Forces are summed over all teeth and 8 axial discs. A tooth contributes only while it is inside the workpiece, so the model shows entry and exit transients.

#### Measurement chain

```
Structure   G(s) = ωn² / (s² + 2ζωn s + ωn²)   per axis (bilinear biquad)
Crosstalk   F' = C · F
Charge      Q  = S · F' + Q_offset + Q_drift + noise
Amplifier   V  = Q / (S · range),  clipped at ±10 V   (ideal: V = −Q/Cf)
Filter/ADC  2nd-order Butterworth at fc, sampled at fs, 16-bit
Displayed   F  = V · range
```

Per-sensor vertical loads (educational): `Fz,i = Fz/4 + Mx·yi/(4b²) − My·xi/(4a²)`, with moments taken about the sensor plane.

### Where the numbers come from

The lab labels every constant with one of three categories, also shown in the *Constants & sources* tab:

- **A: Verified manufacturer specifications** (Kistler 9257B product page). Cover plate 170 × 100 mm; range Fx, Fy ±5 kN, Fz −5…+10 kN; sensitivity −7.5, −7.5, −3.7 pC/N (nominal); natural frequency ≈ 3.5 kHz (sensor, free); stiffness Cx, Cy 1 kN/µm; Fischer 9-pin flange connector; preloaded sensors.
- **B: Engineering equations and published data.** The equations above; Al7050-T7451 cutting coefficients Ktc 796, Krc 168.8, Kac 222 N/mm², Kte 27.7, Kre 30.8, Kae 1.8 N/mm (Altintas); quartz d11 ≈ 2.3 pC/N.
- **C: Educational assumptions.** Al7050 coefficients stand in for Al6061; mild-steel and 316L coefficients are illustrative; dynamometer height, internal sensor geometry and positions; Cz = 2 kN/µm; ζ = 0.03; adjustable mounted fn; crosstalk matrix; residual offset, drift (exaggerated) and noise; ADC; workpiece size; tool travel compressed ×10 visually (chip thickness unchanged); 30° helix.

The lab never invents Kistler calibration coefficients. A real instrument is always used with its own calibration sheet.

### Model limitations

The model does **not** include tool run-out, tool wear, tool or workpiece deflection, chatter, temperature effects, the size effect, or any change in cutting coefficients with speed. Use the lab to build intuition and plan experiments. Only publish forces measured with a calibrated instrument.

### Code structure

Everything is in `index.html`, split into independent modules:

| Module | Responsibility | Depends on |
|---|---|---|
| 1 `Model` | Specifications, material coefficients, kinematics, mechanistic milling force model, steady statistics. Pure JS. | — |
| 2 `Chain` | Measurement chain: 2nd-order structure, crosstalk, quartz charge, offset/drift/noise, charge amplifier, saturation, low-pass filter. | Model |
| 3 `Sim` | Simulation clock at 100 kHz internal rate; tool rotation and feed; sampling at fs with 16-bit ADC; ring buffer. | Model, Chain |
| 4 Plotting | Canvas plots (force–time, spectrum, trials, sweep). No chart library. | — |
| 5 `Scene3D` | Three.js bench: machine, spindle/tool, dynamometer with four sensors, workpiece, cable, charge amplifier, DAQ, monitor; anatomy views, deflection, vectors, force path, picking. | Sim (read-only) |
| 6 Content | Component notes, constants table with categories, sources. | — |
| 7 UI | Guided procedure (13 steps), free mode, parameter controls, dashboard, export. | all |
| 8 Experiment log | `localStorage` trials, CSV export, parameter sweep. | Model |
| 9 Assessment | 14 concept questions, 4 simulator-based tasks, scoring, report. | Sim, Model |

To split the code into separate files, move each module into `js/<module>.js` in the order above and load them as plain scripts. The modules talk to each other only through the objects named in the table.

External dependencies: Three.js r128 (from jsDelivr) and Google Fonts (optional, with fallbacks).

---

## Sources

- Kistler, *Multicomponent dynamometer, 5 kN, cover plate 100x170 mm / 9257B*, item 18007542. https://www.kistler.com/CH/en/p/multicomponent-dynamometers-9257b/000000000018007542
- Y. Altintas, *Manufacturing Automation*, 2nd ed., Cambridge University Press, 2012.
- IEEE Std 176-1987, *IEEE Standard on Piezoelectricity*.
