# NACA 0012 Aerodynamics in Heavy Rain: CFD Replication Study

**Author:** Sumit Ram (AE25MO62)  
**Keywords:** OpenFOAM, Computational Fluid Dynamics (CFD), Python, Multiphase Flow, DPM, Aerodynamics

## 📌 Project Overview
This repository contains a computational replication of the aerodynamic performance degradation experienced by a NACA 0012 airfoil operating in severe rain. The project utilizes an open-source toolchain (**OpenFOAM** and **Python**) to investigate how heavy Liquid Water Content (LWC) acts as dynamic surface roughness, prematurely tripping the boundary layer and reducing aerodynamic efficiency at a low Reynolds number (Re = 100,000).

This work is a streamlined replication of the experimental and computational study conducted by Douvi et al. (2013).

## 🚀 Key Features & Methodology
* **Continuous Phase (Air):** Solved using the steady-state `simpleFoam` solver with an incompressible assumption and the Standard k-epsilon turbulence model.
* **Discrete Phase (Rain):** Simulated using `icoUncoupledKinematicParcelFoam` employing a Lagrangian Discrete Phase Model (DPM) with one-way momentum coupling for computational stability.
* **Severe Weather Condition:** Focused analysis on a heavy thunderstorm condition with an LWC of 75.491 g/m³ and a fixed droplet diameter of 1.2 mm.
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
├── scripts/                     # Python post-processing and plotting script
├── docs/                        # Detailed engineering report and presentation slides
└── README.md
```

## 🛠️ Prerequisites
To run these simulations, you will need the following installed:
* **OpenFOAM** (Tested on v2306 / v9+)
* **Python 3.x** (with `pandas` and `matplotlib` for data analysis)
* **ParaView** (for flow visualization)

## 💻 How to Run the Simulations

**1. Generate the Mesh**
```bash
blockMesh
```

**2. Run the Dry Baseline Simulation**
```bash
simpleFoam
```

**3. Run the Wet (Rain) Simulation**
*(Ensure you have mapped your initial fields properly if starting from a converged dry state)*
```bash
icoUncoupledKinematicParcelFoam
```

**4. Post-Process the Results**
```bash
python scripts/analyze_aerodynamics.py
```

## 📊 Key Results
* **Lift Penalty:** The simulation successfully captured a maximum lift degradation of **33.2%** at a 9° angle of attack under severe rain conditions.
* **Stall Delay:** Contrary to standard icing conditions, the turbulent energy introduced by the "ejecta fog" at the leading edge delayed aerodynamic stall to a higher angle of attack.
* **Limitations:** As a steady-state RANS replication using one-way DPM, the model accurately captures pre-stall lift trends but predictably struggles to resolve unsteady post-stall vortex shedding and the exact physical magnitude of water-film skin friction.

![Lift Curve](docs/lift_curve.png)

## 📚 Acknowledgments & References
This project was developed as an academic replication study. The baseline parameters and experimental validation targets are derived from:
> Douvi, E. C., Margaris, D. P., Lazaropoulos, S. D., & Svanas, S. G. (2013). *Experimental and Computational Study of the Effects of Different Liquid Water Content on the Aerodynamic Performance of a NACA 0012 Airfoil at Low Reynolds Number.* 5th International Conference on Experiments/Process/System Modeling/Simulation/Optimization, Athens, Greece.
