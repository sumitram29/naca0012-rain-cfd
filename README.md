
# NACA 0012 Aerodynamics in Heavy Rain: CFD Replication Study

**Author:** Sumit Ram (AE25MO62)  
**Keywords:** OpenFOAM, Computational Fluid Dynamics (CFD), Python, Multiphase Flow, DPM, Aerodynamics

## 📌 Project Overview
This repository contains a computational replication of the aerodynamic performance degradation experienced by a NACA 0012 airfoil operating in severe rain. The project utilizes an open-source toolchain (**OpenFOAM** and **Python**) to investigate how heavy Liquid Water Content (LWC) acts as dynamic surface roughness, prematurely tripping the boundary layer and reducing aerodynamic efficiency at a low Reynolds number ($Re = 1 \times 10^5$).

This work is a streamlined replication of the experimental and computational study conducted by Douvi et al. (2013).

## 🚀 Key Features & Methodology
* **Continuous Phase (Air):** Solved using the steady-state `simpleFoam` solver with an incompressible assumption and the Standard $k-\epsilon$ turbulence model.
* **Discrete Phase (Rain):** Simulated using `icoUncoupledKinematicParcelFoam` employing a Lagrangian Discrete Phase Model (DPM) with one-way momentum coupling for computational stability.
* **Severe Weather Condition:** Focused analysis on a heavy thunderstorm condition with an LWC of $75.491 \text{ g/m}^3$ and a fixed droplet diameter of 1.2 mm.
* **Automation:** Python scripts utilized to parse OpenFOAM force coefficient logs and automatically calculate lift degradation percentages.

## 📁 Repository Structure
```text
├── 0/                           # Initial boundary conditions and phase fields
├── constant/
│   ├── blockMeshDict            # C-type grid generation dictionary
│   ├── kinematicCloudProperties # DPM droplet injection settings
│   └── turbulenceProperties     # k-epsilon model configuration
├── system/
│   ├── controlDict              # Solver control and forceCoeffs function objects
│   ├── fvSchemes                # Discretization schemes
│   └── fvSolution               # Linear solver settings
├── scripts/
│   └── analyze_aerodynamics.py  # Python post-processing and plotting script
├── docs/
│   └── Final_Report.pdf         # Detailed engineering report and methodology
└── README.md
