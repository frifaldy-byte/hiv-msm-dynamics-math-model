# HIV–MSM Dynamics: A Compartmental Mathematical Model

## Overview

This repository contains the computational implementation and numerical analysis of a compartmental ordinary differential equation (ODE) model of HIV transmission and engagement in prevention and care among men who have sex with men (MSM).

The model describes HIV transmission alongside key prevention and treatment pathways, including pre-exposure prophylaxis (PrEP), HIV diagnosis, antiretroviral therapy (ART), viral suppression, treatment disengagement, and re-engagement in care.

Two dynamic social variables are incorporated into the model: HIV-related stigma and confidence in prevention and care services. These variables represent aggregate social conditions and influence selected transition rates within the epidemiological system. Rather than being treated as fixed external parameters, stigma and service confidence are modelled as endogenous state variables that evolve over time and interact with the epidemiological dynamics.

The analysis covers the mathematical formulation of the model, disease-free equilibrium, the basic reproduction number, local stability, numerical equilibrium searches, time-dependent simulations, parameter sensitivity, parameter-scenario analysis, and intervention scenarios.

## Model Structure

The model consists of six epidemiological compartments and two additional social state variables.

| Variable | Description |
|---|---|
| $S$ | Susceptible individuals not using PrEP |
| $P$ | Susceptible individuals protected by PrEP |
| $I_u$ | HIV-positive individuals who remain undiagnosed |
| $D$ | Diagnosed individuals not yet virally suppressed |
| $T$ | Individuals receiving ART with sustained viral suppression |
| $L$ | Individuals disengaged from ART care |
| $\sigma$ | HIV-related stigma index |
| $C$ | Confidence in HIV prevention and care services |

The epidemiological compartments are connected through infection, PrEP initiation and discontinuation, diagnosis, ART-mediated viral suppression, treatment disengagement, and re-engagement in care.

The force of infection accounts for the relative infectiousness contributions of undiagnosed, diagnosed but unsuppressed, virally suppressed, and ART-disengaged individuals. PrEP protection is represented by a reduced acquisition risk among individuals in compartment $P$. Under the baseline sustained viral suppression assumption, the relative infectiousness weight assigned to compartment $T$ is zero ($\eta_T=0$).

The social subsystem describes changes in stigma and service confidence over time. Both variables jointly regulate selected prevention and care transition rates through bounded logistic functions. The service-confidence feedback term is specifically linked to diagnosis and ART-mediated viral suppression flows; it does not represent every form of prevention or care engagement.

The total population is defined as the sum of the six epidemiological compartments. The stigma and service-confidence variables are dimensionless indices and are not included in the population total.

## Mathematical and Numerical Analysis

The computational framework includes the following analyses:

- **Disease-free equilibrium (DFE):** determination of the infection-free state, including the corresponding equilibrium values of the social variables.
- **Basic reproduction number ($R_0$):** analytical derivation using the next-generation matrix framework, with an independent numerical check based on the spectral radius of the next-generation matrix.
- **Equilibrium analysis:** numerical identification of disease-free and endemic equilibrium candidates, with residual and feasibility checks.
- **Local stability:** assessment using the eigenvalues of the Jacobian matrix evaluated at the relevant equilibrium states.
- **Time-dependent simulations:** numerical integration of the ODE system to examine changes in epidemiological compartments and social variables over time.
- **Sensitivity analysis:** assessment of the effects of selected parameter changes on the basic reproduction number.
- **Parameter-scenario analysis:** exploration of variation in $R_0$ under independently sampled uniform parameter intervals.
- **Intervention scenarios:** comparison of baseline conditions, stigma reduction, confidence enhancement, and their combined implementation.

The analyses are intended to examine the mathematical behaviour of the proposed system under specified assumptions and parameter scenarios.

## Repository Contents

The repository provides a standalone Jupyter Notebook and a compressed research package containing the organised analysis files.

### Main files

- `hiv-msm-math-model.ipynb` — Jupyter Notebook containing the model implementation and numerical analysis.
- `HIV_MSM_Research_Package.zip` — compressed package containing the analysis notebook, Python source code, figures, numerical results, parameter files, and documentation.
- `LICENSE` — MIT License.

### Contents of the research package

After extracting the ZIP archive, the project is organised as follows:

```text
HIV_MSM_Research_Package/
│
├── 01_notebooks/
│   ├── hiv-msm-math-model_FINAL.ipynb
│   └── compartment_diagram_builder.ipynb
│
├── 02_source_code/
│   ├── hiv-msm-math-model_FINAL.py
│   └── create_compartment_diagram.py
│
├── 03_figures/
│   ├── Compartment diagram
│   ├── Susceptible and infected trajectories
│   ├── HIV prevalence dynamics
│   ├── Social-state dynamics
│   ├── Equilibrium analysis
│   ├── R0 sensitivity and uncertainty
│   └── Intervention scenarios
│
├── 04_results/
│   ├── parameters/
│   │   ├── model_parameters.json
│   │   └── parameter_register.csv
│   │
│   └── tables/
│       ├── Numerical diagnostics
│       ├── Equilibrium results
│       ├── Time-series data
│       ├── Sensitivity analysis
│       ├── Parameter uncertainty
│       └── Intervention comparisons
│
└── 05_documentation/
    ├── README.md
    ├── FIGURE_GUIDE.md
    ├── MODEL_ASSUMPTIONS_AND_LIMITATIONS.md
    └── requirements.txt
```

## Getting Started

The analysis can be reproduced using Python and JupyterLab.

### 1. Download the repository

Clone the repository using Git:

```bash
git clone <repository-url>
```

Replace `<repository-url>` with the HTTPS or SSH URL of this repository.

Alternatively, download the repository as a ZIP file from GitHub and extract it locally.

### 2. Extract the research package

If you downloaded the repository ZIP, locate and extract:

```text
HIV_MSM_Research_Package.zip
```

Open a terminal in the extracted `HIV_MSM_Research_Package` directory.

### 3. Install dependencies

Install the required Python packages:

```bash
python -m pip install -r 05_documentation/requirements.txt
```

The main dependencies include NumPy, Pandas, SciPy, Matplotlib, IPython, and JupyterLab.

### 4. Run the Jupyter Notebook

Start JupyterLab:

```bash
jupyter lab
```

Open the following notebook:

```text
01_notebooks/hiv-msm-math-model_FINAL.ipynb
```

Run the notebook cells sequentially, starting from the first cell.

The analysis can also be executed using the standalone Python script from the research package root:

```bash
python 02_source_code/hiv-msm-math-model_FINAL.py
```

The compartment diagram can be regenerated separately using `compartment_diagram_builder.ipynb`.

## Figures and Numerical Outputs

Figures are stored in the `03_figures/` directory, while numerical tables and parameter files are organised under `04_results/`.

The outputs include:

- Epidemiological compartment trajectories.
- HIV prevalence trajectories.
- Social-state dynamics.
- Disease-free and endemic equilibrium results.
- Basic reproduction number sensitivity analysis.
- Parameter-scenario distributions.
- Intervention scenario comparisons.

The accompanying CSV files provide numerical values for further inspection and plotting. Parameter files are provided in JSON and CSV formats to document the values used in the model.

The compartment diagram is available in PNG, PDF, and SVG formats. The vector formats can be used in manuscripts and presentations.

## Reproducibility and Interpretation

A fixed random seed is used for parameter-scenario sampling. Numerical integration, equilibrium searches, residual checks, and local stability calculations are implemented in the Jupyter Notebook and corresponding Python source code.

The parameter set is illustrative and combines explicit modelling assumptions with selected literature-based time-scale anchors. The baseline reproduction number is set to a target value of $R_0=1.20$ by calibrating the transmission parameter $\beta$. It should therefore not be interpreted as an independently estimated epidemiological quantity.

Several assumptions are important when interpreting the results:

- The baseline PrEP transition rates imply a high PrEP coverage scenario at the disease-free equilibrium. This represents a specified modelling scenario rather than a general estimate of PrEP coverage among MSM.
- Sustained viral suppression is represented by assigning zero relative infectiousness to compartment $T$ under the baseline assumption.
- The prevalence at the end of the 100-year simulation is a finite-time result and should not be interpreted as an endemic equilibrium unless convergence to that equilibrium has been established.
- Independent uniform parameter sampling describes variation across the specified parameter intervals. The resulting percentile range is not an empirical confidence interval or posterior distribution.
- The numerical equilibrium search uses multiple initial conditions and a finite parameter grid. It is exploratory and does not establish the uniqueness of endemic equilibria or the formal direction of a bifurcation.
- The model assumes homogeneous mixing and does not explicitly represent individual-level sexual networks or all sources of behavioural heterogeneity.
- The social variables represent aggregate conditions and do not distinguish individual experiences or separate dimensions of stigma.

The framework is intended for mathematical investigation and scenario analysis. Its results should be interpreted in relation to the model structure, parameter choices, and stated assumptions. The model has not been calibrated or externally validated against a defined population dataset and is not intended for direct clinical prediction or population-level forecasting.

## License

This project is distributed under the MIT License. See the `LICENSE` file for details.
