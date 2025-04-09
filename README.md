# 📡 Physics-Inspired Synthetic Dataset for Photonic Waveguide Machine Learning

This repository contains a synthetic dataset of 50,000 samples created from physics-based equations for supervised training of ML models in photonic waveguide design and optimization.

---

## 📁 Dataset Summary

- **Total Parameters**: 27
- **Total Samples**: 50,000
- **Shape**: `50000 x 27` (Inputs + Outputs)

---

## 📥 Input Features (14)

| Feature Name            | Description                          |
|------------------------|--------------------------------------|
| `core_index`           | Core refractive index (n₁)           |
| `clad_index`           | Cladding refractive index (n₂)       |
| `core_radius_m`        | Core radius (a)                      |
| `clad_radius_m`        | Cladding radius (b)                  |
| `length_m`             | Waveguide length (L)                 |
| `wavelength_m`         | Operating wavelength (λ)             |
| `polarization`         | Input polarization [0 to 1]          |
| `alpha_core`           | Loss coefficient of core (α₁)        |
| `alpha_clad`           | Loss coefficient of cladding (α₂)    |
| `photoelastic_coeff`   | Photoelastic coefficient (p)         |
| `delta_rho_over_rho`   | Density variation ratio (Δρ/ρ)       |
| `sigma_rms_m`          | RMS surface roughness (σ)            |
| `roughness_corr_length_m` | Correlation length (L_corr)       |
| `w_in_m`               | Input beam waist (w_in)              |

---

## 📤 Output Features (13)

| Feature Name              | Description                             |
|--------------------------|-----------------------------------------|
| `propagation_loss_dB`    | Propagation loss (PL)                   |
| `insertion_loss_dB`      | Insertion loss (IL)                     |
| `coupling_loss_dB`       | Coupling loss (CL)                      |
| `mode_field_diameter_m`  | Mode Field Diameter (MFD)               |
| `mode_confinement_factor`| Confinement factor (Γ)                 |
| `single_mode`            | Boolean flag: single mode               |
| `multi_mode`             | Boolean flag: multimode                 |
| `scattering_loss_dB`     | Total scattering loss                   |
| `effective_index`        | Effective refractive index (n_eff)      |
| `cross_coupling`         | Mode cross-coupling                     |
| `TE_percent`             | % TE mode power                         |
| `TM_percent`             | % TM mode power                         |
| `V_parameter`            | Normalized frequency (V-number)         |

---

## ⚙️ Governing Equations
👉 See the Jupyter Notebook file: [click here](https://github.com/rayid-mojumder/Physics-inspired-ML-dataset-for-Photonic-Waveguide-Design/blob/main/data/Governing_Physics_Equations.ipynb)

---


## 🧠 Application

This dataset is used to train machine learning models for:
- Photonic waveguide inside glass for integrated optics or semiconductor packaging 
- Predicting optical performance of waveguides
- Identifying mode behavior (single vs. multimode)
- Estimating loss characteristics without simulation tools

---

## 📜 License

The MIT License (MIT)

Copyright (c) <2025> Rayid Mojumder

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

---

## 🤝 Citation

If you use this dataset, please cite:

> Rayid Mojumder, *"Physics-inspired ML dataset for Photonic Waveguide Design"*, Penn State University, 2025.

---



