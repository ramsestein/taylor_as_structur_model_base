# Diagnóstico de Inconsistencia Pearson/Spearman

## Resumen Ejecutivo

- Total de funciones analizadas: 9
- Funciones con inconsistencia signo P/S: 1 (11.1%)

## Factores Asociados a Inconsistencia

- Outliers (pct): Inconsistentes=21.8%, Consistentes=22.2%
- Rango gap: Inconsistentes=0.273, Consistentes=5.285
- Normalidad (Shapiro p): Inconsistentes=0.000, Consistentes=0.000

## Efectividad de Correcciones

- Winsorización (5%): Resuelve 7/9 casos
- Transformación log: Resuelve 8/9 casos
- Z-score: Resuelve 8/9 casos

## Hipótesis de Regímenes Separados

- Correlaciones consistentes dentro de regímenes: 21/27 (77.8%)
  - underfit: 9/9 consistentes
  - well_fit: 6/9 consistentes
  - overfit: 6/9 consistentes

## Conclusión

La inconsistencia Pearson/Spearman se observa en 11.1% de las funciones. Los factores principales son: 100% tienen >5% outliers, y 0% tienen rango de gap amplio.

La hipótesis de regímenes mezclados es PARCIALMENTE SOPORTADA: dentro de cada régimen la correlación es consistente.