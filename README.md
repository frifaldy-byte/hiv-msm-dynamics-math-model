# HIV–MSM Dynamics: A Compartmental Mathematical Model

## Overview

This repository contains the computational implementation and numerical analysis of a compartmental ordinary differential equation (ODE) model of HIV transmission and engagement in prevention and care among men who have sex with men (MSM).

The model considers the progression of HIV infection alongside key prevention and treatment pathways, including pre-exposure prophylaxis (PrEP), HIV diagnosis, antiretroviral therapy (ART), viral suppression, treatment disengagement, and re-engagement in care.

An important part of the formulation is the inclusion of two dynamic social variables: HIV-related stigma and confidence in prevention and care services. These variables influence selected transition rates within the epidemiological system and are incorporated into the model as endogenous state variables rather than fixed external factors.

The work combines mathematical formulation, equilibrium analysis, reproduction-number calculations, numerical simulation, parameter sensitivity assessment, and intervention scenario analysis.

## Model Structure

The model consists of six population compartments and two additional social state variables.

| Variable | Description |
|---|---|
| \(S\) | Susceptible individuals not using PrEP |
| \(P\) | Susceptible individuals protected by PrEP |
| \(I_u\) | HIV-positive individuals who remain undiagnosed |
| \(D\) | Diagnosed individuals not yet virally suppressed |
| \(T\) | Individuals receiving ART with sustained viral suppression |
| \(L\) | Individuals temporarily disengaged from ART |
| \(\sigma\) | HIV-related stigma index |
| \(C\) | Confidence in HIV prevention and care services |

The epidemiological compartments are connected through infection, prevention, diagnosis, treatment, disengagement, and re-engagement pathways.

The force of infection accounts for contributions from undiagnosed, diagnosed, virally suppressed, and ART-disengaged individuals. PrEP protection is represented through a reduced acquisition risk among individuals in the protected compartment.

The social subsystem describes changes in stigma and service confidence over time. Stigma and confidence jointly regulate selected prevention and care transition rates through bounded logistic functions. Service engagement also contributes feedback to the confidence variable.

The total population is defined over the six epidemiological compartments only. The stigma and service-confidence variables are not population compartments.

## Mathematical and Numerical Analysis

The computational framework includes the following analyses:

- **Disease-free equilibrium (DFE):** determination of the infection-free state, including the equilibrium of the social subsystem.
- **Basic reproduction number (\(R_0\)):** analytical derivation using the next-generation framework, with an independent numerical check based on the spectral radius of the next-generation matrix.
- **Equilibrium analysis:** numerical identification of disease-free and endemic equilibrium candidates, followed by residual and feasibility checks.
- **Local stability:** assessment using eigenvalues of the Jacobian matrix evaluated at the equilibrium candidates.
- **Time-dependent simulations:** numerical integration of the ODE system to examine changes in susceptible, infected, treatment, and social states.
- **Sensitivity analysis:** assessment of how selected model parameters influence the reproduction number.
- **Parameter uncertainty:** exploration of the resulting \(R_0\) distribution under independent uniform parameter scenarios.
- **Intervention scenarios:** comparison of baseline conditions, stigma reduction, confidence enhancement, and their combined implementation.

The numerical analyses are intended to examine the mathematical behaviour of the proposed model under the stated assumptions and parameter scenarios.

## Repository Contents

The repository contains a standalone Jupyter Notebook and a compressed package with the organized research files.

### Main files

- `hiv-msm-math-model.ipynb` — Jupyter Notebook containing the model implementation and numerical workflow.
- `HIV_MSM_Research_Package.zip` — organized package containing the analysis notebook, Python source code, figures, numerical results, parameter files, and documentation.
- `LICENSE` — MIT License.

### Contents of the research package

After extracting the ZIP archive, the project is organized as follows:

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

The complete analysis can be reproduced using Python and JupyterLab.

### 1. Download the repository

Clone the repository:

```bash
git clone <REPOSITORY_URL>
```

Alternatively, download the repository as a ZIP file from GitHub.

### 2. Extract the research package

Extract:

```text
HIV_MSM_Research_Package.zip
```

Open a terminal in the extracted `HIV_MSM_Research_Package` directory.

### 3. Install dependencies

Install the required Python packages:

```bash
python -m pip install -r 05_documentation/requirements.txt
```

The main dependencies are NumPy, Pandas, SciPy, Matplotlib, IPython, and JupyterLab.

### 4. Run the Jupyter Notebook

Start JupyterLab:

```bash
jupyter lab
```

Open:

```text
01_notebooks/hiv-msm-math-model_FINAL.ipynb
```

Run the notebook cells sequentially, starting from the first cell.

The analysis can also be executed as a standalone Python script from the project root:

```bash
python 02_source_code/hiv-msm-math-model_FINAL.py
```

The compartment diagram can be regenerated separately using `compartment_diagram_builder.ipynb`.

## Figures and Numerical Outputs

Figures are saved in the `03_figures/` directory, while numerical tables and parameter files are stored under `04_results/`.

The outputs include compartment trajectories, prevalence curves, equilibrium candidates, reproduction-number sensitivity, parameter-scenario distributions, and intervention comparisons.

The CSV files provide the underlying numerical values for further inspection, plotting, and use in scientific manuscripts.

The compartment diagram is available in PNG, PDF, and SVG formats. Vector formats are provided for use in manuscripts and presentation materials.

## Reproducibility and Interpretation

A fixed random seed is used for the parameter-scenario sampling procedure. Numerical integration, equilibrium searches, residual checks, and stability calculations are implemented in the notebook and corresponding Python source.

The parameter set is illustrative and includes proxy-based values and explicit modelling assumptions. The baseline reproduction number is set to a target value by calibrating the transmission parameter; it should not be interpreted as an independently estimated epidemiological quantity.

In particular:

- The baseline PrEP transition rates imply a high PrEP coverage scenario at the disease-free equilibrium.
- The sustained viral suppression assumption is represented by setting the corresponding infectiousness contribution to zero in the baseline scenario.
- Prevalence at the end of the 100-year simulation is a transient value unless convergence to equilibrium is separately established.
- Uniform parameter sampling describes a range of model scenarios, not an empirical confidence interval or posterior distribution.
- The numerical equilibrium scan is exploratory and does not establish uniqueness or the formal direction of a bifurcation.

The results should therefore be interpreted in relation to the model structure, parameter choices, and stated assumptions. The framework is intended for mathematical investigation and scenario analysis, rather than direct clinical prediction or population-level forecasting.

## License

This project is distributed under the MIT License. See the `LICENSE` file for details.
