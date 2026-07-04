# Fuentes de datos

Este documento detalla el origen de cada base de datos utilizada en la réplica, siguiendo el requisito de la rúbrica de acompañar la data bruta con su link oficial o fuente.

## 1. PBI departamental (Valor Agregado Bruto)

- **Institución:** Instituto Nacional de Estadística e Informática (INEI)
- **Serie:** PBI de los Departamentos, según Actividades Económicas, 2007-2022 (año base 2007)
- **Enlace:** https://m.inei.gob.pe/estadisticas/indice-tematico/pbi-de-los-departamentos-segun-actividades-economicas-9110/
- **Archivos:** `data/raw/pbi/pbi_dep01_17.xlsx` a `pbi_dep24_17.xlsx` (un archivo por departamento, en orden alfabético) + `pbi_peru_actividades_17.xlsx` (total nacional, usado para validación)
- **Variable extraída:** Valor Agregado Bruto (VAB) a precios constantes de 2007, miles de soles, suma de las 11 actividades económicas reportadas
- **Nota:** Callao no cuenta con archivo departamental propio en esta serie; el análisis final trabaja con 24 departamentos.

## 2. Población departamental

- **Institución:** INEI
- **Serie:** Estimaciones y Proyecciones de Población
- **Enlace:** https://m.inei.gob.pe/estadisticas/indice-tematico/poblacion-y-vivienda/
- **Archivo:** `data/raw/poblacion/proy_03_4.xlsx`
- **Variable extraída:** Población total estimada al 30 de junio, por departamento y año (2000-2026)
- **Uso:** cálculo del PBI per cápita departamental (`pbi_real / poblacion`)

## 3. Índice de Desarrollo Humano (IDH) departamental

- **Institución:** Programa de las Naciones Unidas para el Desarrollo (PNUD) Perú
- **Publicaciones:** https://www.undp.org/es/peru/publicaciones
- **Fuente principal (panel 2003-2019):** `data/raw/idh/IDH-y-Componentes-2003-2019.xlsx`
- **Fuente complementaria (serie 2017-2024, usada como robustez):** `data/raw/idh/anexo_1-idh_2017-2024_a_nivel_distrital.xlsx`
- **Referencia metodológica adicional:** Informe de Evidencia IDH 2019 — Universidad del Pacífico
  https://www.up.edu.pe/egp/programas-especializacion_copy(1)/SiteAssets/Lists/Observatorio/AllItems/Informe%20de%20Evidencia%20IDH%202019.pdf
- **Referencia complementaria:** Instituto Peruano de Economía (IPE), Índice de Desarrollo Humano
  https://ipe.org.pe/indice-de-desarrollo-humano-idh/
- **Variable extraída:** IDH departamental, identificado mediante código UBIGEO terminado en "0000"
- **Ventana de análisis principal:** 2007-2019 (mismo informe/metodología, evita mezclar criterios de cálculo entre reportes distintos del PNUD)

## 4. Shapefile de límites departamentales

- **Institución:** Instituto Geográfico Nacional (IGN) / Plataforma Nacional de Datos Abiertos
- **Enlace:** https://www.datosabiertos.gob.pe/dataset/limites-departamentales
- **Archivos:** `data/raw/shapefile_departamentos/DEPARTAMENTOS.shp/.shx/.dbf/.prj/.CPG`
- **Contenido:** 25 polígonos (24 departamentos + Callao), sistema de coordenadas WGS84
- **Uso:** construcción de la matriz de pesos espaciales (W) para Moran's I, tests LM, SEM/Durbin-SEM y GWR

## Nota metodológica general

A diferencia del estudio original (Duran et al., 2024, sobre Turquía, con series de 46-54 años), Perú no cuenta con series departamentales largas y metodológicamente homogéneas. Por ello, el periodo de análisis se acota a la ventana más larga disponible con data consistente: **2007-2019**. Esta limitación se discute explícitamente en la sección de método del informe.
