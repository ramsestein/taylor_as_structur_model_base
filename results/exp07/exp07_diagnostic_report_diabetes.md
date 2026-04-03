# Diagnóstico Estructural: diabetes

## Análisis por Feature (1D)

### age
- **Mejor grado**: 10
- **R² train/test**: 0.054 / 0.130
- **ΔC**: 1998235883.27
- **Gap**: -0.076
- **Mismatch**: high → Recomendación: **nonparametric**

### sex
- **Mejor grado**: 1
- **R² train/test**: 0.000 / 0.038
- **ΔC**: 0.02
- **Gap**: -0.038
- **Mismatch**: high → Recomendación: **nonparametric**

### bmi
- **Mejor grado**: 10
- **R² train/test**: 0.387 / 0.300
- **ΔC**: 3784449039.23
- **Gap**: 0.087
- **Mismatch**: high → Recomendación: **nonparametric**

### bp
- **Mejor grado**: 10
- **R² train/test**: 0.208 / 0.207
- **ΔC**: 11305950537.67
- **Gap**: 0.002
- **Mismatch**: high → Recomendación: **nonparametric**

### s1
- **Mejor grado**: 10
- **R² train/test**: 0.058 / 0.152
- **ΔC**: 1889046954.71
- **Gap**: -0.094
- **Mismatch**: high → Recomendación: **nonparametric**

### s2
- **Mejor grado**: 10
- **R² train/test**: 0.056 / 0.156
- **ΔC**: 475051686.72
- **Gap**: -0.100
- **Mismatch**: high → Recomendación: **nonparametric**

### s3
- **Mejor grado**: 10
- **R² train/test**: 0.170 / 0.314
- **ΔC**: 1758685331.52
- **Gap**: -0.144
- **Mismatch**: high → Recomendación: **nonparametric**

### s4
- **Mejor grado**: 10
- **R² train/test**: 0.225 / 0.309
- **ΔC**: 166838889717.48
- **Gap**: -0.084
- **Mismatch**: high → Recomendación: **nonparametric**

### s5
- **Mejor grado**: 10
- **R² train/test**: 0.335 / 0.469
- **ΔC**: 4957554309.16
- **Gap**: -0.134
- **Mismatch**: high → Recomendación: **nonparametric**

### s6
- **Mejor grado**: 10
- **R² train/test**: 0.170 / 0.244
- **ΔC**: 1476663322.82
- **Gap**: -0.074
- **Mismatch**: high → Recomendación: **nonparametric**

## Recomendación Agregada

**Familia recomendada**: ensemble

## Validación

- **R² test (recomendado)**: 0.4254
- **R² test (CV)**: 0.4526
- **Regret**: 0.0272

✓ **La recomendación del framework es válida** (regret < 0.05)