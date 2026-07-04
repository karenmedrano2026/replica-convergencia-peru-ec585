# Réplica: Disparidades socioeconómicas y convergencia regional en el Perú

Réplica adaptada del estudio de Duran, Değerli Çifçi, Karabakan y Doğan (2024), *"Socio-economic and development disparities over the long-run: exploring spatial heterogeneities in the case of Turkey"* (Regional Statistics, Vol. 14, No. 4), aplicando la misma metodología de convergencia regional y heterogeneidad espacial a los departamentos del Perú.

**Curso:** EC-585 Economía Urbana y Regional — Universidad Nacional de San Cristóbal de Huamanga (UNSCH)
**Autora:** Karen Medrano
**Trabajo:** individual

## Objetivo

Analizar la evolución de las disparidades de desarrollo socioeconómico (IDH) e ingreso (PBI per cápita) entre los 24 departamentos del Perú, explorando la heterogeneidad espacial del proceso de convergencia mediante econometría espacial (Moran's I, SEM, Durbin-SEM, GWR) y regresión no paramétrica (LOESS, Kernel).

## Estructura del repositorio

```
├── data/
│   ├── raw/           # data bruta descargada de fuentes oficiales (ver FUENTES.md)
│   └── processed/     # panel de datos ya construido, listo para el análisis
├── notebooks/         # notebook R (Colab) con todo el pipeline de análisis
├── figures/           # mapas, gráficos de Moran, resultados de GWR, etc.
├── report/            # informe final (Word/LaTeX) en formato JARS
└── FUENTES.md         # detalle de todas las fuentes de datos y sus enlaces oficiales
```

## Variables

| Variable | Definición | Fuente |
|---|---|---|
| `dev_2007`, `dev_2019` | IDH departamental | PNUD Perú |
| `d_dev` | Cambio en IDH (2019-2007) | Cálculo propio |
| `ln(pbipc_2007)`, `ln(pbipc_2019)` | Log del PBI per cápita relativo (departamento / promedio nacional) | INEI (PBI) + INEI (población) |
| `d_rgdpc` | Cambio en log del PBI per cápita relativo | Cálculo propio |

## Unidad de análisis

24 departamentos del Perú (Callao excluido por no contar con serie propia de PBI departamental en la fuente utilizada).

## Metodología

1. Estadística descriptiva y ESDA (densidad kernel, mapas, Moran's I)
2. Tests de dependencia espacial (LM-lag, LM-error, robustas, SARMA)
3. Modelos espaciales SEM y Durbin-SEM (máxima verosimilitud)
4. Regresión Geográficamente Ponderada (GWR)
5. Regresión no paramétrica (LOESS y Kernel)

## Cómo reproducir el análisis

El notebook en `notebooks/` lee la data directamente desde este repositorio (vía `raw.githubusercontent.com`), por lo que puede ejecutarse completo desde Google Colab (runtime de R) sin necesidad de descargar archivos manualmente.
