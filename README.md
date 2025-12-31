# economics-rp-2026

**Counterfactual Simulation: AI–Tax Labor Polarization DiD**

Shrey Yadav | IBDP1 | shrey.yadav10@gmail.com

---

## Overview

This repository contains a **synthetic** difference‑in‑differences experiment.  
All data here are simulated; there is **no real CPS/ACS microdata**.

The goal is to illustrate how a task‑based DiD design would recover known
treatment effects of a hypothetical 2026 AI‑focused tax reform on wages.

---

## True Data‑Generating Process (DGP)

The simulation hard‑codes the “true” causal effects and then checks whether DiD
recovers them under sampling noise.

- Low‑skill AI×Post effect (non‑college): β = −0.120  
- High‑skill AI×Post effect (college): β = +0.042  
- AI exposure τ ~ N(0.20, 0.15), truncated to [0, 1]  
- Years: 2020–2025, with `post = 1` for year ≥ 2024  
- College indicator: Bernoulli with p = 0.35  
- Age ~ N(40, 12), truncated to [18, 65]  
- Sample size: N = 100,000 synthetic workers  
- Log wage equation: depends on college, age profile, and the baked‑in
  AI×Post effects, plus Gaussian noise

All of these parameters are explicitly set in `shrey_simulation_clean.py`.

---

## Files

- `shrey_simulation_clean.py`  
  Main script. Generates the synthetic microdata and runs the DiD regressions.
  Writes out both the dataset and the summary results.

- `simulated_microdata_100k.csv`  
  100,000‑row simulated dataset with columns:
  `year`, `ai_exposure`, `college`, `post`, `log_wage`.

- `simulation_results.csv`  
  Summary table of true vs recovered coefficients (one row per specification):
  - `true_dgp_low`: true low‑skill AI×Post effect (−0.120)  
  - `true_dgp_high`: true high‑skill AI×Post effect (+0.042)  
  - `recovered_simple`: pooled DiD estimate  
  - `recovered_full_low`: low‑skill DiD estimate from a richer spec  
  - `recovered_full_high`: high‑skill DiD estimate from a richer spec

---

## How to Reproduce

1. Open `shrey_simulation_clean.py` in a Python environment (e.g. Colab).  
2. Run the script. It will:
   - Simulate the microdata,
   - Estimate the DiD models using `statsmodels`,
   - Save `simulated_microdata_100k.csv` and `simulation_results.csv`.
3. Inspect `simulation_results.csv` to compare the recovered β’s to the
   true DGP values.

   ---

## Monte Carlo Extension (Baseline, Light)

The same DGP is also used in a light Monte Carlo experiment to see how the
estimators behave across many simulated samples.

### Files

- `results/monte_carlo_raw_baseline_light.csv`  
  Coefficient draws from R = 50 Monte Carlo replications of the baseline DGP
  (each replication uses n = 50,000 synthetic workers). Each row contains:
  `rep`, `specification`, `target`, `true_beta`, `beta_hat`, and `se`.

- `results/monte_carlo_summary_baseline_light.csv`  
  Summary statistics by specification:
  `true_beta`, `bias`, `rmse`, `coverage_95`, and `size_at_0`.

### How to Reproduce the Monte Carlo

1. Open `code/Shrey-Simulation-Clean.ipynb` in Google Colab (or a local Jupyter environment).  
2. Run all cells, including the final block labeled “MONTE CARLO BASELINE (light)”.  
3. The notebook will regenerate `results/monte_carlo_raw_baseline_light.csv`
   and `results/monte_carlo_summary_baseline_light.csv` in the working directory.
