# Factibilidad de Early Stopping basado en ΔC

## Resumen por Criterio

### Criterio: d_deltaC
- **Parada temprana**: 100.0%
- **Parada tardía**: 0.0%
- **Exacto**: 0.0%
- **Diferencia media absoluta**: 374.0 muestras

### Criterio: d2_deltaC
- **Parada temprana**: 100.0%
- **Parada tardía**: 0.0%
- **Exacto**: 0.0%
- **Diferencia media absoluta**: 360.0 muestras

### Criterio: ratio
- **Parada temprana**: 100.0%
- **Parada tardía**: 0.0%
- **Exacto**: 0.0%
- **Diferencia media absoluta**: 350.0 muestras

### Criterio: absolute
- **Parada temprana**: 100.0%
- **Parada tardía**: 0.0%
- **Exacto**: 0.0%
- **Diferencia media absoluta**: 400.0 muestras

## Conclusión

✗ **NO FACTIBLE**: Ningún criterio alcanza diferencia media < 50 muestras.
  El mejor criterio (ratio) tiene diferencia media de 350.0 muestras.

## Recomendaciones

1. Usar criterios combinados (e.g., dΔC + ratio)
2. Considerar ventanas móviles para estabilizar la señal
3. Calibrar umbrales por tipo de función