# ΔC Framework: Polynomial Complexity as a Diagnostic Probe

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> An exploratory framework that uses polynomial fitting complexity to diagnose data-model compatibility. Open-sourced as-is with full experimental results and honest limitations.

---

## What this is (and what it isn't)

This project started as an attempt to build a **universal complexity metric** for functions and a **model family selector** based on polynomial surrogate analysis. After extensive experimentation (29 synthetic functions, 7 formal experiments, 3 real datasets), the results showed that:

- **It does not work** as a model family selector (27.6% accuracy, CI [0.138, 0.448])
- **It does not work** as an early stopping signal (100% premature stopping, ~350 samples off)
- **It does not compete** with cross-validation for model selection (CV consistently wins)

**What it does do**, modestly but reliably:

- Detects when polynomial bases are structurally inadequate for a dataset (mismatch detection)
- Produces a typology of complexity curves C(τ) — flat, jump, diverging, failed — that characterizes function-base compatibility
- Shows extremely high reproducibility (CV < 0.001 across seeds)

This repo is published as an open record of the exploration: what was tried, what worked, what didn't, and why.

---

## Core idea

Fit polynomials of increasing degree to data. Measure a complexity metric:

```
C = α·degree + β·n_terms + γ·‖coefficients‖
```

Compare C across train/test splits (ΔC) and against non-parametric fits (splines, GAMs). Large discrepancies signal that the polynomial basis is a poor match for the data structure.

The interesting finding is not ΔC itself, but the **pattern of failure**: how and where polynomials break tells you something about the data.

---

## Key results

### What works

| Finding | Evidence |
|---------|----------|
| Mismatch detection | Oscillatory functions: poly R²=0.06 vs spline R²=0.95 (delta_R2 ≈ 0.94) |
| Regime separation | ΔC separates underfit/well-fit/overfit regimes (ANOVA F=246.9, p<0.001) |
| Curve typology | 4 curve types (flat/jump/diverging/failed) map to function-base compatibility |
| Reproducibility | CV < 0.001 across all multi-seed tests |
| Robustness | Stable under perturbation (scale, noise): variation < 5% |

### What doesn't work

| Claim tested | Result | Verdict |
|-------------|--------|---------|
| Model family selection | 27.6% accuracy (target was >70%) | ✗ Failed |
| Beats cross-validation | CV accuracy 8-23% vs ΔC 0-19% | ✗ CV wins |
| Early stopping signal | All criteria stop ~350 samples too early | ✗ Not viable |
| High-dimensional data | Combinatorial explosion above dim 5-10 | ✗ Structural limit |
| Universal complexity metric | Measures poly-compatibility, not intrinsic complexity | ✗ Reframed |

### Pearson/Spearman inconsistency

ΔC vs gap shows Pearson r=0.607 but Spearman ρ=−0.139 (sign inversion). Log-transform and winsorization partially resolve this (8/9 and 7/9 cases respectively), but the underlying non-monotonicity remains a methodological issue. This is documented, not resolved.

---

## Experiments

Seven experiments were run, all reproducible with fixed seeds:

| Exp | What | Runtime | Key number |
|-----|------|---------|------------|
| 01 | 30-function benchmark across 7 categories | 18.7s | ΔC varies significantly by category |
| 02 | Head-to-head vs AIC/BIC/CV | 250s | CV wins on selection accuracy |
| 03 | Pearson/Spearman diagnostic | 6.6s | 11.1% sign inconsistency rate |
| 04 | Formal selection algorithm with grid search | 29s | 27.6% accuracy, below 70% target |
| 05 | Dimensional scaling (2D to 20D) | 66s | Practical limit: dim ≤ 5 standard, ≤ 20 with extensions |
| 06 | Early stopping feasibility | 4.8s | Not feasible (100% premature) |
| 07 | Real datasets (diabetes, california, friedman) | 30s | Regret < 0.03 but recommends "ensemble" for everything |

Total runtime: ~27 minutes on local GPU. All results in `results/`.

---

## Operating range

| Parameter | Works | Degrades | Fails |
|-----------|-------|----------|-------|
| Dimensions | 1–5 | 6–10 | >10 |
| Samples | 100–1000 | 50–5000 | <50 or >10k |
| Noise (σ) | < 0.5 | < 1.0 | > 2.0 |

---

## Repo structure

```
├── src/                         # Core framework
│   ├── polynomial_fitting/      # Polynomial complexity calculation
│   ├── complexity_estimation/   # C metric components
│   ├── data_generation/         # Synthetic data generators
│   ├── model_training/          # Training utilities
│   └── evaluation/              # Surrogate comparison (spline, GAM, piecewise)
│
├── experiments/                 # Exp01–Exp07
│   ├── run_all_experiments.py   # Master runner (supports --exp N, --skip N)
│   └── exp01_*.py – exp07_*.py
│
├── validation/                  # Original validation blocks (1–3)
├── results/                     # All outputs: CSV, PNG (300 dpi), JSON
└── docs/
    ├── README_Framework.md      # Technical architecture
    └── README_Results.md        # Full results with tables
```

## Setup

```bash
git clone https://github.com/ramsestein/taylor_as_structur_model_base.git
cd taylor_as_structur_model_base
pip install -r requirements.txt
pip install -r experiments/requirements_experiments.txt

# Run everything
python experiments/run_all_experiments.py

# Run one experiment
python experiments/run_all_experiments.py --exp 3
```

---

## What I learned

1. **Polynomial mismatch is informative but not actionable enough.** Knowing that "your data doesn't fit a polynomial" is less useful than just trying several models — which is what CV already does, faster.

2. **The trade-off between fidelity and detectability is real.** Flexible bases (splines, GAMs) fit everything well but eliminate the complexity signal. The diagnostic power comes precisely from the polynomial's rigidity. This is conceptually interesting but practically limiting.

3. **Negative results matter.** The early stopping failure (Exp06) and the model selection failure (Exp04) are clear, reproducible results. They save others from going down the same path.

4. **The Pearson/Spearman sign inversion is a real problem.** Post-hoc corrections (winsorization, log-transform) help but don't fully resolve it. Anyone building on this work needs to address the non-monotonicity of ΔC vs generalization gap.

5. **Reproducibility was the easy part.** CV < 0.001 across seeds. The hard part is having something worth reproducing.

---

## License

MIT. Use it, extend it, learn from the negative results.

---

*Last updated: 2026-04-03*
*Status: Exploration complete. Results documented. Moving on.*
