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

| Name                            | Description                                                                                                                                                                                                           |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `propagation_loss_dB`           | Propagation loss (dB):  
```latex
\[ 
P_{\rm out} = P_{\rm in}\,\exp(-\alpha_{\rm total} L), 
\quad 
\mathcal{L}_{\rm prop} = 10\log_{10}\frac{P_{\rm in}}{P_{\rm out}}.
\]
```  |
| `insertion_loss_dB`             | Insertion (coupling) loss (dB) via Gaussian overlap.                                                                                                                                                                 |
| `coupling_loss_dB`              | Same as insertion loss.                                                                                                                                                                                               |
| `mode_field_diameter_m`         | Mode field diameter:  
```latex
\[
w = a\Bigl(0.65 + 1.619\,V^{-1.5} + 2.879\,V^{-6}\Bigr),
\quad
\mathrm{MFD} = 2w.
\]
```  |
| `mode_confinement_factor`       | Confinement factor Γ:  
```latex
\[
\Gamma = \frac{u^2}{V^2},\quad
u = 
\begin{cases}
0.9\,V, & V<2.405,\\
V-0.5,   & V\ge2.405.
\end{cases}
\]
```  |
| `single_mode`                   | `Y` if \(V<2.405\), else `N`.                                                                                                                                                                                         |
| `multi_mode`                    | Complement of `single_mode`.                                                                                                                                                                                         |
| `scattering_loss_dB`            | Scattering loss (dB):  
```latex
\[
\alpha_{\rm scatt,bulk} = \frac{8\pi^3}{3\lambda^4}p^2\Bigl(\tfrac{\Delta\rho}{\rho}\Bigr)^2\Gamma,
\quad
\alpha_{\rm scatt,surf} = \frac{4\pi^3}{\lambda^2}\sigma^2L_{\rm corr},
\quad
\mathcal{L}_{\rm scatt} = 4.343\bigl(\alpha_{\rm scatt,bulk} + \alpha_{\rm scatt,surf}\bigr)L.
\]
```  |
| `effective_index`               | Effective index:  
```latex
\[
n_{\rm eff} = \sqrt{n_{2}^2 + \frac{u^2}{V^2}(n_{1}^2 - n_{2}^2)}.
\]
```  |
| `cross_coupling`                | Cross-coupling:  
```latex
\[
\mathrm{CrossCoupling} = 
\begin{cases}
0, & V < 2.405,\\
\tfrac12\,(V-2.405)/V, & V \ge 2.405.
\end{cases}
\]
```  |
| `TE_percent`, `TM_percent`      | Mode polarization percentages.                                                                                                                                                                                        |
| `V_parameter`                   | Normalized frequency:  
```latex
\[
V = \frac{2\pi\,a}{\lambda}\sqrt{n_1^2 - n_2^2}.
\]
```  |
| `output_power`                  | Output power:  
```latex
\[
P_{\rm out} = P_{\rm in}\,\exp(-\alpha_{\rm total}L).
\]
```  |

---

## 🧮 Key Equations

```latex
\[
V = \frac{2\pi\,a}{\lambda}\sqrt{n_1^2 - n_2^2}
\]
\[
w = a\Bigl(0.65 + 1.619\,V^{-1.5} + 2.879\,V^{-6}\Bigr),\quad \mathrm{MFD}=2w
\]
\[
\Gamma = \frac{u^2}{V^2},\quad
u = 
\begin{cases}
0.9\,V, & V<2.405,\\
V-0.5,   & V\ge2.405,
\end{cases}
\]
\[
\alpha_{\rm eff} = \alpha_{\rm core}\,\Gamma + \alpha_{\rm clad}\,(1-\Gamma)
\]
\[
\alpha_{\rm scatt,bulk}
  = \frac{8\pi^3}{3\lambda^4}\,p^2\Bigl(\tfrac{\Delta\rho}{\rho}\Bigr)^2\Gamma,
\quad
\alpha_{\rm scatt,surf}
  = \frac{4\pi^3}{\lambda^2}\,\sigma^2\,L_{\rm corr}
\]
\[
\alpha_{\rm total} = \alpha_{\rm eff} + \alpha_{\rm scatt,bulk} + \alpha_{\rm scatt,surf}
\]
\[
P_{\rm out} = P_{\rm in}\,\exp(-\alpha_{\rm total}L),
\quad
\mathcal{L}_{\rm prop} = 10\log_{10}\!\Bigl(\tfrac{P_{\rm in}}{P_{\rm out}}\Bigr)
\]
```

---

## ⚙️ Data Generation Procedure

1. **Load experimental data**  
   Read propagation losses and MFDs from the literature table; compute mean & std.  
2. **Sample inputs & compute physics**  
   Uniformly sample inputs; compute \(V\), \(w\), \(\Gamma\), loss coefficients, \(n_{\rm eff}\), polarization, etc.  
3. **Inject noise**  
   Apply 5\% Gaussian noise to each computed output.  
4. **Experimental correction**  
   Tune loss & MFD values to match the experimental mean and standard deviation.  
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
