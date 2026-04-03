# Límite Práctico Dimensional

## Hallazgos

- **standard**: Funciona hasta dimensión 20
- **sparse**: Funciona hasta dimensión 20
- **random_projection**: Funciona hasta dimensión 20
- **additive**: Funciona hasta dimensión 20

## Recomendaciones

1. Para dim ≤ 5: Usar método estándar
2. Para 5 < dim ≤ 10: Usar LASSO (sparse)
3. Para 10 < dim ≤ 20: Usar proyección aleatoria o descomposición aditiva
4. Para dim > 20: El framework requiere modificaciones sustanciales
