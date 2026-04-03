# Diagnóstico Estructural: california

## Análisis por Feature (1D)

### MedInc
- **Mejor grado**: 8
- **R² train/test**: 0.494 / 0.473
- **ΔC**: 0.50
- **Gap**: 0.021
- **Mismatch**: high → Recomendación: **nonparametric**

### HouseAge
- **Mejor grado**: 7
- **R² train/test**: 0.030 / 0.023
- **ΔC**: -0.00
- **Gap**: 0.006
- **Mismatch**: high → Recomendación: **nonparametric**

### AveRooms
- **Mejor grado**: 6
- **R² train/test**: 0.091 / 0.127
- **ΔC**: 0.00
- **Gap**: -0.036
- **Mismatch**: high → Recomendación: **nonparametric**

### AveBedrms
- **Mejor grado**: 8
- **R² train/test**: 0.012 / 0.007
- **ΔC**: 0.50
- **Gap**: 0.005
- **Mismatch**: high → Recomendación: **nonparametric**

### Population
- **Mejor grado**: 3
- **R² train/test**: 0.001 / 0.001
- **ΔC**: 0.00
- **Gap**: 0.000
- **Mismatch**: high → Recomendación: **nonparametric**

### AveOccup
- **Mejor grado**: 4
- **R² train/test**: 0.042 / 0.079
- **ΔC**: 0.50
- **Gap**: -0.037
- **Mismatch**: high → Recomendación: **nonparametric**

### Latitude
- **Mejor grado**: 10
- **R² train/test**: 0.048 / 0.079
- **ΔC**: 1.50
- **Gap**: -0.032
- **Mismatch**: high → Recomendación: **nonparametric**

### Longitude
- **Mejor grado**: 3
- **R² train/test**: 0.018 / 0.023
- **ΔC**: 0.34
- **Gap**: -0.005
- **Mismatch**: high → Recomendación: **nonparametric**

## Recomendación Agregada

**Familia recomendada**: ensemble

## Validación

- **R² test (recomendado)**: 0.8037
- **R² test (CV)**: 0.8037
- **Regret**: 0.0000

✓ **La recomendación del framework es válida** (regret < 0.05)