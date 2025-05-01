# Updated Realistic Synthetic Waveguide Dataset

This repository contains a realistic synthetic dataset generator for optical waveguide characterization. It builds on a physics-inspired core, injects controlled noise, and tunes to match real experimental statistics. The final output is:

- **50,000 samples**  
- **15 input features** (geometrical, material, and physical parameters)  
- **14 output targets** (losses, mode properties, effective index, polarization, etc.)  

Use this dataset to train data-driven models that predict waveguide performance from basic design parameters—with the added realism of experimental-data correction.

---

## 📂 Input Parameters (15 Features)

| Name                             | Description                                                                                       | Units / Format                       |
|----------------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------|
| `core_index`                     | Complex refractive index of the core, as string `n_real+n_imagj` (e.g. `1.488000-3.200000e-08j`). | —                                    |
| `clad_index`                     | Complex refractive index of the cladding, same format.                                            | —                                    |
| `core_radius_m`                  | Core radius \(a\).                                                                                | meters (0.5 × 10⁻⁶–10 × 10⁻⁶ m)       |
| `clad_radius_m`                  | Cladding radius \(b\).                                                                            | meters (20–50 µm)                    |
| `length_m`                       | Waveguide length \(L\).                                                                           | meters (1 mm–0.5 m)                  |
| `wavelength_m`                   | Operating wavelength \(\lambda\).                                                                 | meters (500 nm–1600 nm)              |
| `polarization`                   | Input polarization (0 = TE, 1 = TM).                                                              | unitless (0–1)                       |
| `alpha_core`                     | Core intrinsic loss \(\alpha_{\rm core}\).                                                        | m⁻¹ (1e-4–1e-3)                      |
| `alpha_clad`                     | Cladding intrinsic loss \(\alpha_{\rm clad}\).                                                    | m⁻¹ (1e-4–1e-3)                      |
| `photoelastic_coeff`             | Photoelastic coefficient \(p\).                                                                   | unitless (0.20–0.25)                 |
| `delta_rho_over_rho`             | Density variation ratio \(\Delta\rho/\rho\).                                                      | unitless (1e-12–1e-11)               |
| `sigma_rms_m`                    | RMS surface roughness \(\sigma\).                                                                 | meters (1–10 nm)                     |
| `roughness_corr_length_m`        | Roughness correlation length \(L_{\rm corr}\).                                                    | meters (100 nm–1 µm)                 |
| `w_in_m`                         | Input beam waist \(w_{\rm in}\).                                                                  | meters (1–5 µm)                      |
| `input_power`                    | Input optical power \(P_{\rm in}\).                                                               | Watts (1–10 mW)                      |

---

## 🌟 Output Targets (14 Features)

| Name                            | Description                                                        |
|---------------------------------|--------------------------------------------------------------------|
| `propagation_loss_dB`           | Propagation loss (dB)                                              |
| `insertion_loss_dB`             | Insertion (coupling) loss (dB)                                     |
| `coupling_loss_dB`              | Same as insertion loss                                             |
| `mode_field_diameter_m`         | Mode field diameter \(2w\)                                         |
| `mode_confinement_factor`       | Fraction of power confined in the core \(\Gamma\)                 |
| `single_mode`                   | `Y` if single-mode (V<2.405), else `N`                            |
| `multi_mode`                    | Complement of `single_mode`                                        |
| `scattering_loss_dB`            | Scattering loss (dB)                                              |
| `effective_index`               | Effective refractive index \(n_{\rm eff}\)                        |
| `cross_coupling`                | Cross-coupling metric                                             |
| `TE_percent`, `TM_percent`      | Mode polarization percentages                                     |
| `V_parameter`                   | Normalized frequency \(V\)                                        |
| `output_power`                  | Output power \(P_{\rm out}\)                                      |

> **Note:** All detailed equations are listed in the [Key Equations](#key-equations) section below.

---

## 🧮 Key Equations

---

### 1. Normalized Frequency \(V\)
\[
V = \frac{2\pi\,a}{\lambda}\,\sqrt{n_{\rm core,real}^2 - n_{\rm clad,real}^2}
\]
- \(a\) = core radius (m)  
- \(\lambda\) = operating wavelength (m)  
- \(n_{\rm core,real}\), \(n_{\rm clad,real}\) = real parts of core/clad indices  

---

### 2. Mode Field Diameter (MFD)
\[
w = a\Bigl(0.65 + 1.619\,V^{-1.5} + 2.879\,V^{-6}\Bigr),
\quad
\mathrm{MFD} = 2\,w
\]
- \(w\) = Gaussian mode‐field radius (m)  
- \(\mathrm{MFD}\) = mode‐field diameter (m)  

---

### 3. Mode Confinement Factor \(\Gamma\)
\[
u = 
\begin{cases}
0.9\,V, & V < 2.405,\\
V - 0.5, & V \ge 2.405,
\end{cases}
\qquad
\Gamma = \frac{u^2}{V^2}
\]
- \(u\) = eigenvalue parameter  
- \(\Gamma\) = fraction of power in the core (unitless)  

---

### 4. Intrinsic (Effective) Attenuation
\[
\alpha_{\rm eff} = \alpha_{\rm core}\,\Gamma
  + \alpha_{\rm clad}\,(1 - \Gamma)
\]
- \(\alpha_{\rm core}, \alpha_{\rm clad}\) = intrinsic loss coeffs (m\(^{-1}\))  

---

### 5. Scattering Loss Coefficients
\[
\alpha_{\rm scatt,bulk}
  = \frac{8\pi^3}{3\,\lambda^4}\,p^2
    \Bigl(\frac{\Delta\rho}{\rho}\Bigr)^2\,\Gamma,
\qquad
\alpha_{\rm scatt,surf}
  = \frac{4\pi^3}{\lambda^2}\,\sigma_{\rm rms}^2\,L_{\rm corr}
\]
- \(p\) = photoelastic coefficient (unitless)  
- \(\Delta\rho/\rho\) = density fluctuation ratio (unitless)  
- \(\sigma_{\rm rms}\) = RMS roughness (m)  
- \(L_{\rm corr}\) = roughness correlation length (m)  

---

### 6. Total Attenuation
\[
\alpha_{\rm total}
  = \alpha_{\rm eff}
  + \alpha_{\rm scatt,bulk}
  + \alpha_{\rm scatt,surf}
\]
- \(\alpha_{\rm total}\) = total loss coefficient (m\(^{-1}\))  

---

### 7. Output Power
\[
P_{\rm out}
  = P_{\rm in}\,\exp\bigl(-\alpha_{\rm total}\,L\bigr)
\]
- \(P_{\rm in}\) = input optical power (W)  
- \(L\) = waveguide length (m)  

---

### 8. Propagation Loss (dB)
\[
\mathcal{L}_{\rm prop}
  = 10 \,\log_{10}\!\frac{P_{\rm in}}{P_{\rm out}}
\]
- \(\mathcal{L}_{\rm prop}\) = propagation loss in dB  

---

### 9. Coupling / Insertion Loss
First compute Gaussian overlap:
\[
\Delta x \sim \mathcal{U}(0,2w), 
\quad
T_{\rm nom}
  = \frac{2\,w_{\rm in}\,w}{w_{\rm in}^2 + w^2}
    \exp\!\Bigl(-\frac{\Delta x^2}{w_{\rm in}^2 + w^2}\Bigr),
\qquad
T_{\rm nom} \ge 10^{-12}
\]
Then
\[
\mathrm{IL}_{\rm dB}
  = -20 \log_{10}(T_{\rm nom}),
\quad
\mathrm{CL}_{\rm dB} = \mathrm{IL}_{\rm dB}
\]
- \(w_{\rm in}\) = input beam waist (m)  
- \(\Delta x\) = lateral misalignment (m)  
- \(\mathrm{IL}_{\rm dB}\), \(\mathrm{CL}_{\rm dB}\) = insertion/coupling loss (dB)  

---

### 10. Effective Refractive Index
\[
b = \frac{u^2}{V^2},
\quad
n_{\rm eff}
  = \sqrt{n_{\rm clad,real}^2 
    + b\,\bigl(n_{\rm core,real}^2 - n_{\rm clad,real}^2\bigr)}
\]
- \(n_{\rm eff}\) = effective index of guided mode  

---

### 11. Cross-Coupling Metric
\[
\mathrm{CrossCoupling} =
\begin{cases}
0, & V < 2.405,\\
\frac12\,(V - 2.405)/V, & V \ge 2.405.
\end{cases}
\]

---

### 12. Polarization Percentages
\[
\begin{aligned}
&\text{If }V<2.405:\quad
&&\mathrm{TE}\% = (1 - p_{\rm pol})\times100,\quad
\mathrm{TM}\% = p_{\rm pol}\times100,\\
&\text{Else:}\quad
&&\mathrm{TE}\% =
   \bigl((1-p_{\rm pol})(1-C)+0.5\,C\bigr)\times100,\\
&&&\mathrm{TM}\% =
   \bigl((p_{\rm pol})(1-C)+0.5\,C\bigr)\times100.
\end{aligned}
\]
- \(p_{\rm pol}\) = raw polarization fraction (0–1)  
- \(C\) = cross-coupling  

---

### 13. Noise Injection
For each computed output \(x\):
\[
\eta \sim \mathcal{N}\bigl(0,\;(\tfrac{\%}{100})^2\bigr),
\quad
x' = x\,(1 + \eta)
\]
- \(\%\) = noise percentage (e.g.\ 5 %)  
- \(\eta\) = Gaussian noise factor  

---

### 14. Clamping / Experimental Correction
- Enforce non-negative losses:  
  \(\mathcal{L}_{\rm prop} \ge 0.1\);  
  \(\mathrm{IL}_{\rm dB}, \mathrm{CL}_{\rm dB}, \mathrm{scattering\_loss\_dB} \ge 0\).  
- Prevent zero/negative power:  
  \(P_{\rm out} \ge 10^{-20}\) W.  
---


## ⚙️ Data Generation Procedure

1. **Load experimental data**  
   Read propagation losses and MFDs from the literature; compute mean & std.  
2. **Sample inputs & compute physics**  
   Uniformly sample inputs; compute parameters \(V\), \(w\), \(\Gamma\), loss coefficients, \(n_{\rm eff}\), polarization, etc.  
3. **Inject noise**  
   Apply 5\% Gaussian noise to each computed output.  
4. **Experimental correction**  
   Adjust loss & MFD distributions to match experimental statistics.  
5. **Persist to CSV**  
   Batch-write 1,000 samples at a time into `final_realistic_synthetic_dataset.csv`.

---

## 📋 Usage Example

```bash
git clone https://github.com/yourusername/waveguide-dataset.git
cd waveguide-dataset
python generate_waveguide_dataset.py
# Output: final_realistic_synthetic_dataset.csv
```

---

## 📄 License

This project is licensed under the MIT License.  
