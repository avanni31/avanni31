# 📡 Simulating and Analysing Antenna Array (2×1) Using CST Microwave Studio

> **ECE-205: Electromagnetic Engineering**  
> A simulation-based study of a 2×1 microstrip patch antenna array operating at **2.45 GHz**, designed and analyzed using CST Microwave Studio.


---

## 📌 Table of Contents

- [Introduction](#introduction)
- [Working Principle](#working-principle)
- [Design Specifications](#design-specifications)
- [Methodology](#methodology)
- [Results and Observations](#results-and-observations)
  - [VSWR Analysis](#vswr-analysis)
  - [S-Parameter Analysis](#s-parameter-analysis)
  - [E-Field Distribution](#e-field-distribution)
  - [H-Field Analysis](#h-field-analysis)
  - [Farfield Radiation Pattern](#farfield-radiation-pattern)
  - [Gain and Directivity](#gain-and-directivity)
- [Conclusion](#conclusion)
- [Applications](#applications)

---

## 📖 Introduction

A **microstrip patch antenna** is a low-profile, compact antenna widely used in wireless communication systems due to its ease of fabrication. However, a single patch antenna suffers from **low gain** and a **broad radiation pattern**, limiting its performance in high-precision applications.

To overcome these limitations, this project combines two identical patch antennas into a **2×1 antenna array**, which significantly improves radiation characteristics — providing higher gain and more directional radiation.

**Key goals of this project:**
- Design a single microstrip patch antenna resonating at 2.45 GHz
- Extend it into a 2×1 array configuration
- Simulate and analyze performance using CST Microwave Studio
- Verify results against theoretical calculations

---

## ⚙️ Working Principle

```
Input Signal → Feed Port → T-Junction Power Divider
                                  ↓              ↓
                           Patch Antenna 1   Patch Antenna 2
                                  ↓              ↓
                           Radiation (constructive interference in space)
```

1. **Signal Feeding** — A signal is injected via a wave port through the microstrip feed line.
2. **Substrate Role** — The FR4 substrate controls wave speed and field distribution between the patch and the ground plane.
3. **Ground Plane** — Forces all radiation upward (broadside direction).
4. **Power Splitting** — A T-junction divider splits the input signal equally, ensuring both patches receive the same power and remain in phase.
5. **Resonance** — Each patch acts as a resonator; fringing fields at the patch edges cause radiation.
6. **Array Effect** — The two patches radiate together, and their signals combine via **constructive interference**, resulting in higher gain and narrower beamwidth.

---

## 📐 Design Specifications

| Parameter | Value |
|-----------|-------|
| Operating Frequency | 2.45 GHz |
| Substrate Material | FR4 |
| Relative Permittivity (εᵣ) | 4.4 |
| Substrate Height (h) | 1.6 mm |
| Patch Length (L) | 28.81 mm |
| Patch Width (W) | 37.23 mm |
| Inter-element Spacing | λ/2 |

### Quarter-Wave Transformer (QWT) Parameters

| Parameter | Value |
|-----------|-------|
| Impedance (Z) | 70.7 Ω |
| Feed Line Length (Lf) | 14.58 mm |
| Feed Line Width (Wf2) | 1.62 mm |

### Design Equations

**Patch Width:**

$$W = \frac{c}{2f_0\sqrt{\frac{\varepsilon_R + 1}{2}}}$$

**Effective Permittivity:**

$$\varepsilon_{eff} = \frac{\varepsilon_R + 1}{2} + \frac{\varepsilon_R - 1}{2} \left(\frac{1}{\sqrt{1 + 12\frac{h}{W}}}\right)$$

**Patch Length:**

$$L = \frac{c}{2f_0\sqrt{\varepsilon_{eff}}} - 0.824h \left(\frac{(\varepsilon_{eff}+0.3)\left(\frac{W}{h}+0.264\right)}{(\varepsilon_{eff}-0.258)\left(\frac{W}{h}+0.8\right)}\right)$$

**Quarter-Wave Transformer Impedance:**

$$Z_1 = \sqrt{Z_0 \cdot Z_L}$$

---

## 🔬 Methodology

```
Step 1: Define Requirements & Calculate Patch Dimensions
        ↓
Step 2: Design Single Patch Antenna in CST
        ↓
Step 3: Convert to 2×1 Array
        (Duplicate patch, λ/2 spacing, T-junction feed network)
        ↓
Step 4: Run Array Simulation
        (Add wave port, simulate for S-parameters, E-field, H-field)
        ↓
Step 5: Analyze Results & Optimize
        (Adjust dimensions/spacing/feed position to match theory)
```

---

## 📊 Results and Observations

### Simulated Structure

The final simulated structure consists of:
- Two microstrip patch elements (yellow)
- FR4 substrate (beige)
- Ground plane (bottom layer)
- T-junction microstrip feed network
- Wave port (excitation point)

---

### VSWR Analysis

The **Voltage Standing Wave Ratio (VSWR)** measures how well the antenna is matched to its feed line.

| VSWR Value | Interpretation |
|------------|----------------|
| VSWR = 1 | Perfect matching |
| VSWR < 2 | Acceptable operation |
| VSWR > 2 | Poor matching |

**Result:** VSWR ≈ **1.1 – 1.3** at 2.45 GHz

The VSWR plot shows a sharp dip near 2.5 GHz, confirming:
- Excellent impedance matching in the target band
- Suitable for wireless communication (2.45 GHz ISM band)
- Efficient radiation with minimal power loss

---

### S-Parameter Analysis

#### S11 — Return Loss

$$S_{11} = 20\log_{10}|\Gamma|$$

- A deep dip is observed at **~2.45 GHz**
- Minimum S11 ≈ **−30 dB**
- Only **~3%** of power is reflected
- About **~97%** of input power is radiated
- Bandwidth is defined for S11 < −10 dB

> A return loss of −30 dB indicates excellent impedance matching at the target frequency.

#### S21/S31 — Transmission Coefficient (Power Split)

Power is divided using a **T-junction power divider**. For an ideal equal split:

$$P_{out} = \frac{P_{in}}{2} \quad \Rightarrow \quad 10\log_{10}\left(\frac{1}{2}\right) = -3 \text{ dB}$$

**Result:** Obtained S21/S31 ≈ **−3.5 dB**

The small deviation from the ideal −3 dB is attributed to:
- Dielectric loss in the FR4 substrate
- Radiation loss from the feed network
- Minor impedance mismatches

---

### E-Field Distribution

Simulated at **f = 2.45 GHz** | Maximum E-field: **5001.85 V/m**

Key observations:
- Maximum field intensity concentrated at **patch radiating edges** (fringing fields)
- Strong field along feeding network confirms proper signal excitation
- Fringing fields at patch boundaries validate the radiation mechanism
- Uniform field distribution across both patch elements confirms the array is working symmetrically
- Field spreading outward indicates effective radiation into free space

---

### H-Field Analysis

Simulated at **f = 2.45 GHz** | Maximum H-field: **23.5087 A/m**

Key observations:
- High magnetic field concentration near the feed line
- Magnetic field loops indicate surface current flow on the patches
- Balanced field distribution across both patches confirms symmetric excitation
- Outward field propagation contributes to radiation

#### Power Density Calculation from H-Field

$$S = \eta_0 H^2 = 377 \times (23.5087)^2 \approx 208{,}000 \text{ W/m}^2$$

---

### Farfield Radiation Pattern

The 3D farfield pattern at 2.45 GHz shows:

| Feature | Observation |
|---------|-------------|
| Pattern Type | Directional (broadside) |
| Main Lobe Direction | Along +Y axis (broadside) |
| Side Lobes | Low — confirms directional behavior |
| Peak Directivity | 8.88 dBi |
| Color Scale | Red = max radiation, Blue = min radiation |

The pattern confirms the array radiates predominantly in one direction (broadside), with minimal back radiation and low sidelobes — behavior characteristic of a well-designed linear array.

---

### Gain and Directivity

**Farfield simulation data (f = 2.45 GHz):**

| Parameter | Value |
|-----------|-------|
| Radiation Efficiency | −3.729 dB |
| Total Efficiency | −3.759 dB |
| Directivity | 8.875 dBi |

#### Derived Calculations

**Wavelength:**
$$\lambda = \frac{c}{f} = \frac{3 \times 10^8}{2.45 \times 10^9} \approx 0.122 \text{ m}$$

**Directivity (linear scale):**
$$D = 10^{8.875/10} \approx 7.72$$

**Realized Gain:**
$$G = D + \eta = 8.57 - 6.44 = 2.13 \text{ dBi}$$

**Effective Aperture Area:**
$$A_e = \frac{\lambda^2 D}{4\pi} \approx 0.0091 \text{ m}^2$$

---

## ✅ Conclusion

The 2×1 microstrip patch antenna array was successfully designed and simulated at 2.45 GHz using CST Microwave Studio. The simulation results validate the design and demonstrate significant performance advantages over a single patch antenna.

### Summary of Key Results

| Metric | Result | Interpretation |
|--------|--------|----------------|
| Return Loss (S11) | ≈ −30 dB | Excellent impedance matching |
| VSWR | ≈ 1.1 – 1.3 | Minimal reflection |
| S21/S31 | ≈ −3.5 dB | Near-equal power split |
| Directivity | ≈ 8.875 dBi | Improved radiation performance |
| Radiation Pattern | Broadside, low sidelobes | Directional and focused |
| E-field max | 5001.85 V/m | Proper excitation confirmed |
| H-field max | 23.5087 A/m | Balanced current distribution |

The array configuration successfully demonstrated:
- Higher gain and directivity compared to a single patch
- Narrower beamwidth due to constructive interference
- Efficient power transfer with minimal losses
- Slight losses attributed to FR4 dielectric and minor impedance mismatch

---

## 📡 Applications

This 2×1 patch antenna array is suitable for:

- **Wi-Fi / ISM Band** — Operates in the 2.4–2.5 GHz band, compatible with IEEE 802.11b/g/n standards
- **Wireless Communication Systems** — High gain and directivity make it suitable for point-to-point links
- **IoT and Short-Range Devices** — Compact size and low profile fit embedded applications
- **Radar Systems** — Directional radiation pattern is beneficial for target detection
- **Satellite Communication** — Broadside radiation useful for satellite uplink/downlink

---

## 🛠️ Tools Used

- **CST Microwave Studio** — EM simulation and analysis
- **Solver:** Time Domain (FIT - Finite Integration Technique)

---

## 📚 References

- C. A. Balanis, *Antenna Theory: Analysis and Design*, 3rd Edition, Wiley
- D. M. Pozar, *Microwave Engineering*, 4th Edition, Wiley
- CST Studio Suite Documentation
