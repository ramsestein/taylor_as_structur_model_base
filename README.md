# ΔC Framework: Polynomial Complexity-Based Mismatch Detection

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Experiments](https://img.shields.io/badge/experiments-7%2F7%20passing-green.svg)](./results/)

> **A machine learning framework for detecting model-data mismatch using polynomial complexity metrics**

This repository contains the implementation and validation of the ΔC (Delta Complexity) framework, a novel approach for quantifying the mismatch between parametric (polynomial) and non-parametric (spline) model fits to identify when data requires more sophisticated modeling approaches.

## 🎯 Core Concept

The ΔC framework introduces a **complexity gap metric** defined as:

```
ΔC = C_test - C_train
```

Where:
- **C_train**: Complexity of polynomial fit on training data
- **C_test**: Complexity of polynomial fit on test data
- **Complexity (C)**: α·degree + β·n_terms + γ·coef_norm

A large ΔC indicates that the polynomial model is unstable across data splits, suggesting the data may benefit from non-parametric or more complex modeling approaches.

## 📁 Repository Structure

```
delta-c-framework/
├── README.md                    # This file
├── LICENSE                      # MIT License
├── requirements.txt             # Core dependencies
├── .gitignore                   # Git ignore rules
│
├── src/                         # Core framework implementation
│   ├── polynomial_fitting/      # Polynomial complexity calculation
│   ├── complexity_estimation/   # Complexity metrics
│   ├── data_generation/         # Synthetic data generators
│   ├── model_training/          # Training utilities
│   └── evaluation/              # Evaluation metrics
│
├── experiments/                 # Experimental framework (Exp01-Exp07)
│   ├── requirements_experiments.txt
│   ├── README.md
│   ├── run_all_experiments.py   # Master runner
│   ├── exp01_*.py - exp07_*.py   # Individual experiments
│   └── legacy/                   # Previous experimental code
│
├── validation/                  # Original validation blocks (1-3)
│   ├── validation_block1_overfitting.py
│   ├── validation_block2_temporal.py
│   ├── validation_block3_surrogates.py
│   └── validation_master.py
│
├── demos/                       # Demo scripts
│   └── run_demos.py
│
├── scripts/                     # Utility scripts
│   └── (various utilities)
│
├── results/                     # Experimental outputs (gitignored)
│   └── .gitkeep
│
└── docs/                        # Additional documentation
    ├── README_Framework.md      # Technical details
    └── README_Results.md        # Validation results
```

## 🚀 Quick Start

### Installation

```bash
# Clone the repository
git clone https://github.com/ramsestein/taylor_as_structur_model_base.git
cd taylor_as_structur_model_base

# Install dependencies
pip install -r requirements.txt

# For experimental features
pip install -r experiments/requirements_experiments.txt
```

### Basic Usage

```python
import numpy as np
from src.polynomial_fitting.fitter import PolynomialFitter

# Generate synthetic data
X = np.linspace(0, 10, 500)
y = np.sin(2 * np.pi * X) + np.random.normal(0, 0.1, 500)

# Create fitter and evaluate complexity
fitter = PolynomialFitter(max_degree=15)
results = fitter.evaluate_thresholds(X.reshape(-1, 1), y)

# Get complexity curve
for tau, result in results.items():
    print(f"τ={tau}: degree={result['degree']}, C={result['complexity']:.2f}")
```

### Running Experiments

```bash
# Run all experiments (Exp01-Exp07)
python experiments/run_all_experiments.py

# Run individual experiments
python experiments/exp03_correlation_analysis.py
```

## 📊 Key Results

### Experimental Validation (7/7 Passing)

| Experiment | Description | Key Finding |
|------------|-------------|-------------|
| **Exp01** | 30-Function Benchmark | ΔC varies significantly across 7 functional categories |
| **Exp02** | vs AIC/BIC/CV | CV accuracy (8-23%) consistently outperforms ΔC (0-19%) |
| **Exp03** | P/S Correlation | 11.1% functions show Pearson/Spearman sign inconsistency |
| **Exp04** | Selection Algorithm | 27.6% accuracy (fails >70% threshold) |
| **Exp05** | Scalability | Practical limit: dim ≤ 20 with extensions |
| **Exp06** | Early Stopping | ΔC NOT viable as early stopping signal |
| **Exp07** | Real Data | Valid for ensemble selection, regret < 0.03 |

See [docs/README_Results.md](docs/README_Results.md) for detailed analysis.

## 🔬 Framework Capabilities

### ✅ What It Detects
- **Polynomial mismatch**: When spline significantly outperforms polynomial (delta_R2_ps > 0.5)
- **Functional family differences**: 8 separable functional categories
- **Incremental value**: +37% over simple linear baseline

### ❌ Limitations
- **Early overfitting detection**: Low confidence (weak evidence)
- **High-dimensional data**: Explodes combinatorially above 10D
- **Overlapping families**: Cannot distinguish piecewise vs. oscillatory

### 📐 Operating Ranges

| Parameter | Useful Range | Degradation | Failure |
|-----------|--------------|-------------|---------|
| Dimension | 1-5 | 6-10 | >10 |
| Samples | 100-1000 | 50-5000 | <50, >10k |
| Noise (σ) | < 0.5 | < 1.0 | > 2.0 |

## 📖 Documentation

- **[docs/README_Framework.md](docs/README_Framework.md)**: Detailed framework architecture, complexity metrics, and theoretical foundations
- **[docs/README_Results.md](docs/README_Results.md)**: Complete experimental validation results (Q1 2026)
- **[results/MASTER_SUMMARY.md](results/MASTER_SUMMARY.md)**: Auto-generated consolidated results

## 🧪 Reproducibility

All experiments use fixed random seeds (`random_seed = 42`) with 30 repetitions per condition. Results are empirically supported with:

- CSV data files in `results/exp*/`
- Publication-ready figures (300 DPI, colorblind palette)
- Detailed Markdown reports per experiment
- Bonferroni-corrected statistical tests

## 🤝 Citation

If you use this framework in your research, please cite:

```bibtex
@software{delta_c_framework_2026,
  title = {ΔC Framework: Polynomial Complexity-Based Mismatch Detection},
  author = {Author Name},
  year = {2026},
  note = {Experimental validation framework for model selection},
  url = {https://github.com/ramsestein/taylor_as_structur_model_base}
}
```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Validation standards follow NeurIPS/ICML/Nature ML guidelines
- Experimental design inspired by rigorous ML reproducibility standards
- Colorblind-friendly visualizations using seaborn colorblind palette

---

**Status**: Framework validated with documented limitations  
**Last Updated**: 2026-04-03  
**Experiments**: 7/7 passing (1607s total runtime)
