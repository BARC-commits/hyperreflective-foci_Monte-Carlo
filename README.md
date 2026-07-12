# Monte Carlo Simulation: Retinal Hyperreflective Foci and Microplastics

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![BioSystems](https://img.shields.io/badge/Journal-BioSystems-red.svg)](https://www.sciencedirect.com/journal/biosystems)

## Overview

This repository contains the complete Python code for a Monte Carlo simulation investigating whether retinal hyperreflective foci (HRF) - well-established optical coherence tomography (OCT) biomarkers - could contain microplastics (MNPs). The simulation builds on the empirical confirmation of MNPs in human retinal tissue (Zhang et al., 2025, *Environmental Science & Technology Letters*) and extends the Bayesian framework proposed by Tan Aik Kah (2025a, 2025b, *BioSystems*).

The simulation models HRF as a competitive process between MNP-associated and non-MNP causes, incorporating uncertainty in particle count, spatial congruence, optical match rate, and the non-MNP HRF baseline. It generates all figures presented in the associated manuscript and provides sample size calculations for physical validation studies.

## Key Findings

- **Base simulation:** Median estimates of 30% (Healthy), 70% (Diabetic Retinopathy), and 75% (AMD) - direct consequences of non-MNP baseline assumptions
- **Conservative scenario:** Median 11.31%, with >50% of simulations showing >10% MNP-associated HRF
- **Sensitivity analysis:** Non-MNP HRF baseline is the dominant parameter; MNP mass, spatial congruence, optical match rate, and HRF count show negligible influence
- **Sample size:** 2-3 HRF sufficient for 95% confidence under most likely scenario; 30-40 HRF recommended to account for uncertainty

## Repository Structure

```
├── simulation.py          # Main simulation code
├── requirements.txt       # Python dependencies
├── Figure1_Base_Simulation.png
├── Figure2_Scenario_Analysis.png
├── Figure3_Tornado_Diagram.png
├── Figure4_Density_Curves.png
└── README.md              # This file
```

## Requirements

- Python 3.10 or higher
- NumPy >= 1.24.0
- Pandas >= 2.0.0
- Matplotlib >= 3.7.0
- SciPy >= 1.10.0

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/retinal-mnp-hrf-simulation.git
cd retinal-mnp-hrf-simulation

# Install dependencies
pip install -r requirements.txt
```

## Usage

Run the simulation:

```bash
python simulation.py
```

The script will:
1. Run 1,000,000 iterations for the base simulation
2. Run 500,000 iterations for scenario analyses
3. Generate four figures (saved as PNG files in the current directory)
4. Display output statistics in the console

### Reproducibility Notes

This code does not set a fixed random seed. Results will vary slightly between runs due to random sampling. The values reported in the associated manuscript are from a specific simulation run, recorded in Appendix B. Readers may obtain slightly different values when running the code independently.

## Figures Generated

| Figure | Description |
|--------|-------------|
| **Figure 1** | Base simulation: Bar chart with 95% CI for Healthy, DR, AMD |
| **Figure 2** | Scenario analysis: Comparison of Conservative, Most Likely, Optimistic |
| **Figure 3** | Tornado diagram: Sensitivity analysis showing parameter influence |
| **Figure 4** | Probability density distributions (KDE) for disease states and scenarios |

## Parameter Definitions

| Parameter | Distribution | Description |
|-----------|--------------|-------------|
| Particle Diameter | Log-normal(ln30, 0.3) | MNP size based on Zhang et al. (2025) 20-50 μm range |
| Particle Count | Poisson (mass-derived) | Number of MNPs per retina from 49.21 μg/g |
| C_spatial | Beta(5, 20) | Probability particle is positioned to form HRF |
| Optical Match | Beta(10, 30) | Probability positioned particle generates HRF signal |
| Non-MNP Baseline | Fixed (0.70, 0.30, 0.25) | Proportion of HRF from non-MNP causes |
| HRF Count | Poisson (λ=2, 20, 30) | Number of observable HRF |

## Scenario Definitions

| Scenario | MNP Mass (μg/g) | C_spatial Mean | Optical Match Mean | Non-MNP Fraction |
|----------|-----------------|----------------|-------------------|------------------|
| Conservative | 20.0 | 0.09 | 0.09 | 0.50 |
| Most Likely | 49.21 | 0.20 | 0.25 | 0.30 |
| Optimistic | 91.05 | 0.40 | 0.50 | 0.15 |

## Sample Size Calculation

The simulation provides sample size requirements for physical validation studies:

| Confidence Level | HRF Required (Most Likely) | HRF Required (Conservative) |
|------------------|---------------------------|----------------------------|
| 80% | 2 | ~8 |
| 90% | 2 | ~11 |
| 95% | 3 | ~14 |

**Recommendation:** Sample 30-40 HRF to account for uncertainty across scenarios.

## Limitations

1. **Tautological base case:** Median estimates are direct consequences of the non-MNP baseline assumptions
2. **Non-empirically validated parameters:** Spatial congruence and optical match rate distributions are based on expert judgment
3. **Conversion uncertainties:** Mass-to-particle count conversion involves assumptions about size, shape, and density
4. **Model simplifications:** Binary MNP/non-MNP classification; independent parameter constraints
5. **Absence of empirical validation:** Computational hypotheses requiring physical testing

## Citation

If you use this code in your research, please cite:

```
Tan Aik Kah. (2025). A Monte Carlo Simulation to Estimate the Proportion of 
Retinal Hyperreflective Foci Associated with Microplastics. 
```

And reference the underlying works:

```
Tan AK. A Bayesian approach to investigating presumed retinal micro(nano)plastics. Biosystems. 2025;253:105502. doi:10.1016/j.biosystems.2025.105502

Tan AK. Bayesian consolidation of retinal micro(nano)plastic hypothesis: From existential confirmation to spatial–phenotypic inference. BioSystems. 2025;259:105685. doi:10.1016/j.biosystems.2025.105685

Zhang M, Liu S, Wang Y, et al. Detection and characterization of multiple microplastics in the human retina. Environ Sci Technol Lett. 2025;12(10):1327-1333. doi:10.1021/acs.estlett.5c00903

```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact

For questions or collaborations, please open an issue on GitHub or contact the corresponding author.

---

## Acknowledgments

This work builds on the empirical discovery of MNPs in human retina by Zhang et al. (2025) and the Bayesian framework developed by Tan Aik Kah (2025a, 2025b).

---

**Keywords:** microplastics, retina, hyperreflective foci, Monte Carlo simulation, optical coherence tomography, environmental ophthalmology
