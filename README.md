# SIR Epidemic Model with ODE Solvers

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Course](https://img.shields.io/badge/Course-AM609L-purple.svg)]()

SIR Epidemic ODE Solver

## Data

This project uses the Our World in Data (OWID) COVID-19 dataset.
The data file (174 MB) is not stored in this repository.

**Download options:**
- Original source: [OWID catalog](https://catalog.ourworldindata.org/garden/covid/latest/compact/compact.csv)
- Exact snapshot used in this project (Required dataset in .csv) : [Google Drive](https://drive.google.com/drive/folders/1fPyLxnXKO_jU8PdrIHXcAVY0bvDW1YY4?usp=sharing)

**Snapshot details:**
- Downloaded: 21 October 2026
- SHA-256: `paste-your-hash-here`

Save the file as `data/owid_covid_full.csv`.

**Source:** Our World in Data, COVID-19 dataset (CC BY 4.0).


**DSTT G5 Project**  
**Course:** Data Science Tools & Techniques (AM609L)  
**Group 5 Members:**  
- Sanghakara Manwar (26-27-13)  
- Rohit Satpute (26-27-14)  
- Shreya (26-27-15)  
- Tanesh Devhare (26-14-05)

---

## Project Overview

This project implements and analyzes the classic **SIR (Susceptible-Infected-Recovered) epidemic model** using numerical methods and real-world COVID-19 data. The work covers four main objectives:

1. **Numerical Methods Implementation** – Euler and RK4 methods for SIR ODEs with convergence analysis
2. **Parameter Estimation** – Grid search fitting of β (transmission rate) and γ (recovery rate) to real COVID-19 data
3. **R₀ Estimation & "Flattening the Curve"** – Scenario analysis demonstrating intervention impact
4. **Bonus: Historical Validation** – Digitization and fitting of 1905-06 Bombay plague data

---

## SIR Model

The classic SIR model divides a population of size $N$ into three compartments:

$$
\begin{aligned}
\frac{dS}{dt} &= -\beta \frac{S I}{N} \\
\frac{dI}{dt} &= \beta \frac{S I}{N} - \gamma I \\
\frac{dR}{dt} &= \gamma I
\end{aligned}
$$

Where:
- $S(t)$ = Susceptible individuals
- $I(t)$ = Infectious individuals  
- $R(t)$ = Recovered/Removed individuals
- $\beta$ = Transmission rate (per day)
- $\gamma$ = Recovery rate (per day)
- $R_0 = \beta/\gamma$ = Basic reproduction number

**Analytical Invariant:** $S + I - \frac{\gamma N}{\beta} \ln S = C$ (constant along trajectories)

---

## Repository Structure

```
SIR-Epidemic-Model/
├── DSTT_G5_SIR_Epidemic_Model_with_ODE_Solvers.ipynb   # Main project notebook
├── requirements.txt                                     # Python dependencies
├── LICENSE                                              # MIT License
├── .gitignore                                           # Git ignore rules
├── README.md                                            # This file
├── Data/
│   ├── india_covid_cleaned.csv                          # India COVID-19 data (OWID/JHU)
│   ├── japan_covid_cleaned.csv                          # Japan COVID-19 data (OWID/JHU)
│   ├── bombay_plague_data_1905.xlsx                     # 1905-06 Bombay plague weekly deaths
│   └── owid_covid_full.csv                              # Full OWID COVID dataset
├── Figures/
│   ├── Convergence_Analysis.png                         # Euler vs RK4 convergence
│   ├── Analytical.png                                   # SIR invariant verification
│   ├── IND_Actual_vs_Predicted.png                      # India COVID fit
│   ├── IND_Fitted_SIR.png                               # India SIR curves
│   ├── IND_C19_Second_Wave.png                          # India wave visualization
│   ├── IND_Transmission.png                             # India transmission scenarios
│   ├── JPN_Actual_vs_Predicted.png                      # Japan COVID fit
│   ├── JPN_Fitted_SIR.png                               # Japan SIR curves
│   ├── JPN_C19_Main_Wave.png                            # Japan wave visualization
│   ├── JPN_Transmission.png                             # Japan transmission scenarios
│   ├── IND_vs_JPN.png                                   # Comparative analysis
│   ├── Bombay_Plague.png                                # Bombay plague fit
│   └── SIR_Model.png                                    # SIR compartment diagram
├── Report/
│   └── DSTT_G5_SIR_Epidemic_Model_Report.pdf           # Project report
├── PPT/
│   ├── DSTT_G5_SIR_Epidemic_Model_PPT.pptx             # Presentation slides
│   └── DSTT_G5_SIR_Epidemic_Model_PPT.pdf              # Presentation (PDF)
└── kermack1927a.pdf                                     # Original Kermack-McKendrick paper
```

---

## Key Results

### 1. Numerical Methods Convergence

| Method | Theoretical Order | Observed Order |
|--------|------------------|----------------|
| Euler  | 1.0              | ~0.99          |
| RK4    | 4.0              | ~3.95          |

**RK4 dramatically outperforms Euler** – at step size $h=0.165$, Euler error ≈ $6.7 \times 10^4$ while RK4 error ≈ $4.3 \times 10^{-4}$.

**Analytical Invariant Preservation:**
- Euler max invariant error: $3.2 \times 10^4$
- RK4 max invariant error: $2.3 \times 10^{-5}$

### 2. COVID-19 India (Second Wave, Feb–Aug 2021)

| Parameter | Value |
|-----------|-------|
| $\beta$ (transmission rate) | 0.095 /day |
| $\gamma$ (recovery rate) | 0.0196 /day |
| $R_0 = \beta/\gamma$ | **4.85** |
| Avg. infectious period | 51.1 days |
| Effective population | 37.1M (2.6% of total) |
| Weekly $R^2$ | 0.811 |
| Weekly RMSE | 347,831 |

### 3. COVID-19 Japan (Summer Wave, Jul–Oct 2022)

| Parameter | Value |
|-----------|-------|
| $\beta$ (transmission rate) | 0.266 /day |
| $\gamma$ (recovery rate) | 0.109 /day |
| $R_0 = \beta/\gamma$ | **2.44** |
| Avg. infectious period | 9.2 days |
| Effective population | 28.3M (22.7% of total) |
| Weekly $R^2$ | 0.949 |
| Weekly RMSE | 115,079 |

### 4. Comparative Insights

| Aspect | India | Japan |
|--------|-------|-------|
| $R_0$ | 4.85 (high) | 2.44 (moderate) |
| Infectious period | 51 days (long) | 9 days (short) |
| Effective pop. fraction | 2.6% | 22.7% |
| Model fit ($R^2$) | 0.81 | 0.95 |

**Key Insight:** Japan's lower $R_0$, shorter infectious period, and larger effective population fraction suggest more homogeneous mixing and better containment dynamics.

### 5. Flattening the Curve – Scenario Analysis

Simulating ~26% reduction in $\beta$ (representing NPIs: masks, distancing, lockdowns):

| Country | Scenario | Peak Infections | Peak Day | Reduction | Delay |
|---------|----------|----------------|----------|-----------|-------|
| **India** | High $\beta$ (no intervention) | 9.75M | Day 123 | — | — |
| | Low $\beta$ (intervention) | 6.79M | Day 175 | **30%** | **52 days** |
| **Japan** | High $\beta$ (no intervention) | 1.89M | Day 49 | — | — |
| | Low $\beta$ (intervention) | 0.51M | Day 65 | **73%** | **16 days** |

**Critical Finding:** Early intervention is disproportionately effective for high-$R_0$ epidemics. Japan's low-$\beta$ scenario stays **below healthcare capacity** (750K), while India still exceeds capacity (3M) even with intervention.

### 6. Bonus: Bombay Plague 1905–06

- **Data:** Weekly plague deaths for Bombay City (digitized from historical records)
- **Model Fit:** SIR successfully fits the 1905-06 epidemic wave
- **Result:** Fitted $R_0$ and infectious period are epidemiologically plausible
- **Significance:** Demonstrates SIR framework's applicability across diseases and eras

---

## Requirements

```bash
pip install -r requirements.txt
```

Or manually:
```bash
pip install numpy pandas matplotlib scipy openpyxl jupyter
```

- Python 3.8+
- Jupyter Notebook / JupyterLab

---

## How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/SIR-Epidemic-Model.git
   cd SIR-Epidemic-Model
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Open the main notebook:**
   ```bash
   jupyter notebook DSTT_G5_SIR_Epidemic_Model_with_ODE_Solvers.ipynb
   ```

4. **Run all cells** sequentially (Cell → Run All)

The notebook is organized in sections matching the Table of Contents. All figures and tables are generated in-place.

---

## Data Sources

- **COVID-19 Data:** Our World in Data / Johns Hopkins CSSE
  - `Data/india_covid_cleaned.csv` – India daily cases, deaths, vaccinations, mobility
  - `Data/japan_covid_cleaned.csv` – Japan daily cases, deaths, hospitalizations
- **Bombay Plague Data:** Historical weekly mortality records (1905-06), digitized from Bombay Plague Committee reports
  - `Data/bombay_plague_data_1905.xlsx` – Weekly cases/deaths for Bombay City and districts

---

## Methodology Summary

### Parameter Estimation (Grid Search)
- **Objective:** Minimize normalized weekly squared error between observed and predicted new infections
- **Two-stage approach:**
  1. Coarse grid: $\beta \in [0.05, 1.0]$, $\gamma \in [0.03, 0.5]$, fraction $\in [0.01, 0.2]$
  2. Fine grid: ±5% around coarse best estimates
- **Time discretization:** RK4 with daily steps
- **Aggregation:** Weekly sums for noise reduction


### I(t) and R(t) Estimation from Case Data

Since only cumulative COVID-19 cases are reported, the number of infectious individuals and recovered individuals is estimated using the following assumptions:

**Assumptions:**
- Infectious period: \(D = 14\) days (assumed average infectious period).
- Cumulative cases are used as a proxy for the total number of reported infections.

**Mathematical Formulation:**

The number of infectious individuals at time \(t\) is estimated as:

\[
I(t) = \text{Total Cases}(t) - \text{Total Cases}(t-D)
\]

The number of recovered individuals at time \(t\) is estimated as:

\[
R(t) = \text{Total Cases}(t-D)
\]

**Where:**
- \(I(t)\) = Estimated number of currently infectious individuals at time \(t\).
- \(R(t)\) = Estimated cumulative number of recovered individuals at time \(t\).
- \(\text{Total Cases}(t)\) = Cumulative reported cases on day \(t\).
- \(\text{Total Cases}(t-D)\) = Cumulative reported cases 14 days before day \(t\).
- \(D\) = Assumed infectious period (14 days).

**Note:** These are simplified estimates based on a fixed infectious period. They assume that individuals are no longer infectious after 14 days and that reported cumulative cases adequately represent infections. Actual infectious and recovered counts may differ due to reporting delays, reinfections, deaths, and variations in recovery times.


---

## Conclusions

1. **RK4 is strongly preferred** over Euler for epidemiological modeling – 4th-order convergence validated, analytical invariant preserved to machine precision
2. **Grid search effectively fits** $\beta$ and $\gamma$ to real epidemic data
3. **India's 2nd wave** driven by very high $R_0 \approx 4.85$ with long infectious period (~51 days)
4. **Japan's wave** characterized by lower $R_0 \approx 2.44$ but faster dynamics (~9 days infectious period)
5. **Intervention timing is critical** – modest $\beta$ reduction (~26%) yields dramatic peak reduction and delay, especially for high-$R_0$ settings
6. **SIR framework generalizes** – successfully applied to 1905-06 Bombay plague, validating cross-disease applicability

---

## Future Work / Limitations

- **Constant parameters** – no time-varying $\beta(t)$ for dynamic interventions
- **Homogeneous mixing assumption** – no age structure, spatial coupling, or network effects
- **Effective population fraction** – simplified proxy for under-reporting/asymptomatic cases
- **Extensions to explore:** SEIR/SEAIR models, vaccination compartments, stochastic formulations, Bayesian parameter inference

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Academic project for educational purposes. Data sources retain their original licenses.

---

## Acknowledgments

- Our World in Data for COVID-19 datasets
- Johns Hopkins CSSE for pandemic data infrastructure
- Historical archives for Bombay plague records
- Course instructors for guidance on DSTT G5 Project
- Kermack & McKendrick (1927) for the foundational SIR model