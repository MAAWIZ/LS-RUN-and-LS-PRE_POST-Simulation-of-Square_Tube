# LS-DYNA Tutorial: Static and Dynamic Axial Tube Crush


This repository contains the setup files, keyword definitions, and documentation for performing numerical simulations of **Static and Dynamic Axial Tube Crushing** using **LS-DYNA**. 

The tutorial demonstrates how to model thin-walled tubular structures subjected to axial compressive loads, evaluating energy absorption, deformation modes (folding/buckling), and force-displacement characteristics.

---

## 📌 Project Overview

Axial crushing of tubes is a classic problem in impact mechanics and crashworthiness engineering (e.g., automotive crash boxes, energy absorbers). This project covers both **quasi-static** and **dynamic dynamic** loading conditions to observe strain rate effects and inertial response.

### Objectives
- Build geometric and finite element models of thin-walled circular/square tubes.
- Define appropriate material models considering plasticity and strain rate sensitivity (`*MAT_024` / `*MAT_PIECEWISE_LINEAR_PLASTICITY`).
- Set up boundary conditions for both static (implicit/slow explicit) and dynamic (high-velocity explicit) loading.
- Configure contact interfaces (`*CONTACT_AUTOMATIC_SINGLE_SURFACE`, `*CONTACT_AUTOMATIC_SURFACE_TO_SURFACE`).
- Post-process energy absorption (internal energy vs. kinetic energy) and force-displacement response.

---

## 🛠️ Software & Key Commands

### Prerequisites
- **Pre/Post Processor:** LS-PrePost
- **Solver:** LS-DYNA (Explicit/Implicit)

### Key LS-DYNA Keywords Used
| Keyword | Description |
| :--- | :--- |
| `*SECTION_SHELL` | Formulations for thin-walled elements (Belytschko-Tsay / Fully Integrated). |
| `*MAT_PIECEWISE_LINEAR_PLASTICITY` | Elastoplastic material model (`*MAT_024`) with failure and strain-rate dependence. |
| `*BOUNDARY_PRESCRIBED_MOTION_SET` | Applying displacement/velocity profiles for static and dynamic cases. |
| `*CONTACT_AUTOMATIC_SINGLE_SURFACE` | Self-contact definition to prevent element interpenetration during folding. |
| `*CONTACT_AUTOMATIC_SURFACE_TO_SURFACE` | Contact between tube ends and rigid impactor/plate. |
| `*CONTROL_TERMINATION` | Setting simulation end time. |
| `*DATABASE_BINARY_D3PLOT` | Requesting animation output states. |

---


## 🚀 Setup & Execution Guide

1. **Open Model in LS-PrePost:**
   - Launch LS-PrePost and open the desired keyword file (`.k` or `.key`) from the `models/` directory.

2. **Verify Keyword Settings:**
   - Ensure units are consistent (e.g., $\text{mm}, \text{ms}, \text{g}, \text{N}, \text{MPa}$).
   - Check shell thickness parameters in `*SECTION_SHELL`.

3. **Run Simulation:**
   - Execute the job via LS-DYNA Manager or Command Line:
     ```bash
     ls-dyna i=dynamic_crush.k memory=100m ncpu=4
     ```

4. **Post-Processing (LS-PrePost):**
   - Open `d3plot` file to visualize axial buckling modes (concertina/diamond patterns).
   - Plot **Global Statistics (`glstat`)** to verify energy conservation ($\text{Hourglass Energy} < 5\text{--}10\%$ of Total Energy).
   - Extract contact interface forces via **`rcforc`** to plot force-displacement curves.

---

## 📊 Key Results & Findings

- **Deformation Modes:** Comparison of folding modes under static vs. dynamic rate conditions.
- **Energy Absorption:** Calculation of Mean Crushing Force ($F_{\text{mean}}$) and Peak Crush Force ($F_{\text{peak}}$).
- **Strain Rate Sensitivity:** Observation of dynamic hardening effects on force response.



## 📜 License

This project is open-source and available under the [MIT License](LICENSE).
