# 🚀 Release v1.0.0 Preview

We’re excited to unveil **v1.0.0** of [Physics-inspired-ML-dataset-for-Photonic-Waveguide-Design](https://github.com/rayid-mojumder/Physics-inspired-ML-dataset-for-Photonic-Waveguide-Design). This release offers two complementary synthetic datasets tailored for cylindrical waveguides and on‐chip photonic interconnects in glass substrates—perfect for integrated photonics, HBM interposers, AI/GPU accelerators, and beyond.

---

## 📈 Available Datasets

1. **Physics-Only Dataset**  
   - **50 000 samples** generated directly from first‐principles waveguide equations  
   - Computes normalized frequency (V), mode‐field diameter (MFD), confinement (Γ), attenuation (α), effective index (nₑff), polarization ratios, cross‐coupling, and output power  
   - Ideal for pure physics‐inspired ML benchmarks in photonic device design  

2. **Realistic Dataset (Noise + Experimental Infusion)**  
   - Builds on the physics core, then injects **5 % Gaussian noise** to emulate fabrication/measurement variability  
   - **Calibrated** against literature measurements (propagation loss, MFD, etc.) across fused silica, phosphate, chalcogenide, and doped‐glass waveguides  
   - Marries analytical rigor with real‐world data for robust, generalizable model training  

---

## 🔧 Highlights

- **Physics-Inspired Foundations**  
  Marcuse’s empirical MFD formula, Rayleigh scattering theory, Gaussian overlap coupling, exponential loss decay  

- **Noise Injection**  
  Controlled 5 % Gaussian perturbations to simulate device and measurement uncertainties  

- **Experimental Data Infusion**  
  Tuned to match published propagation‐loss and mode‐field statistics for glass and silicon-based waveguides  

- **Target Applications**  
  - **Integrated Photonics**  
  - **High-Bandwidth Memory (HBM) Interposers**  
  - **AI/GPU Photonic Accelerators**  
  - **Optical Neural Networks & On-Chip Optical Links**  

---

## 📂 Quick Start

```bash
git clone https://github.com/rayid-mojumder/Physics-inspired-ML-dataset-for-Photonic-Waveguide-Design.git
cd Physics-inspired-ML-dataset-for-Photonic-Waveguide-Design
```
---

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15319336.svg)](https://doi.org/10.5281/zenodo.15319336)
