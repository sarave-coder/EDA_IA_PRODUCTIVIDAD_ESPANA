# Adopción de inteligencia artificial en las empresas españolas (2022–2026)

**Proyecto de análisis exploratorio de datos (EDA)** sobre la implantación de tecnologías de inteligencia artificial (IA) en empresas españolas, sus diferencias por tamaño y sector económico, las tecnologías y aplicaciones más habituales y su posible asociación con la productividad laboral.

## Objetivos y preguntas de investigación

1. **H1 — Evolución:** ¿ha aumentado la adopción de IA entre 2022 y 2026? ¿Cómo se sitúa España respecto a la UE?
2. **H2 — Tamaño:** ¿utilizan más IA las empresas grandes que las pequeñas?
3. **H3 — Sector:** ¿existen diferencias de adopción entre actividades económicas?
4. **H4 — Uso y barreras:** ¿qué tecnologías y aplicaciones se utilizan y qué obstáculos se declaran?
5. **H5 — Productividad:** ¿el aumento de la adopción de IA entre 2023 y 2025 ha ido acompañado de un crecimiento de la productividad laboral real por hora trabajada?

## Fuentes de datos

- **INE:** Encuesta sobre el uso de TIC y comercio electrónico en las empresas; tablas de implantación de IA de 2022 a 2026. [Operación estadística](https://www.ine.es/dyngs/INEbase/es/operacion.htm?c=Estadistica_C&cid=1254736176743&menu=ultiDatos&idp=1254735576799) · [Metodología](https://www.ine.es/daco/daco42/comele/meto_eticce.pdf).
- **Eurostat:** adopción de tecnologías de IA por empresas, indicador `isoc_eb_ai`, para la comparación de España con la UE-27.
- **Eurostat:** tabla [`nama_10_lp_ulc`](https://ec.europa.eu/eurostat/databrowser/view/nama_10_lp_ulc/default/table), indicador `RLPR_HW` (productividad laboral real por hora trabajada), unidad `I15` (índice 2015 = 100), para España en 2021–2025.

Los archivos CSV descargados se almacenan en `src/data/raw/`.

## Principales hallazgos

| Análisis                   | Resultado destacado                                                                                                                                                                                                                                                        |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Evolución en España       | Adopción general del **12,60 % en 2022** al **33,60 % en 2026** (+21,00 puntos porcentuales). La serie no crece todos los años.                                                                                                                              |
| Comparación europea        | En 2025, **España: 20,27 %**; **UE-27: 19,95 %** (serie armonizada de Eurostat). España ocupa el puesto **13 de 27**.                                                                                                                                  |
| Tamaño empresarial         | En 2026, **74,39 %** en empresas de 250 o más personas, frente a **29,14 %** en las de 10 a 49.                                                                                                                                                               |
| Diferencias sectoriales     | En 2025, **información y comunicaciones: 60,57 %**; **construcción: 11,44 %**.                                                                                                                                                                               |
| Tecnologías y aplicaciones | En 2025 destacan la **generación de imágenes, vídeo o audio (53,87 %)** y la **administración y gestión empresarial (29,75 %)**, respectivamente. Los denominadores de estos indicadores deben verificarse antes de compararlos con la adopción general. |
| Barreras                    | La **falta de conocimientos especializados (81,29 %)** es la barrera con mayor porcentaje dentro de su indicador.                                                                                                                                                    |
| Productividad               | Entre 2023 y 2025, la adopción de IA (Eurostat) aumentó **120,8 %** en términos relativos (9,18 % → 20,27 %), mientras que la productividad real por hora creció **1,46 %** (índice 101,761 → 103,250). Comparación descriptiva, **no causal**.  |

## Metodología

1. Carga y unificación de los cinco CSV del INE.
2. Homogeneización de nombres de columnas, años, tamaños de empresa e indicadores.
3. Validaciones de integridad y preparación de un dataset procesado.
4. Análisis descriptivo y visualización de las hipótesis H1–H4.
5. Comparación con la serie europea de Eurostat, manteniendo separadas las series INE y Eurostat.
6. Selección de la productividad laboral real por hora trabajada de España (`RLPR_HW`, `I15`) para 2021–2025.
7. Comparación descriptiva de la adopción de IA (Eurostat) y la productividad real por hora en 2023–2025, expresadas como índices con base 2023 = 100; sin inferencia causal ni correlación estadística con tres observaciones.

## Estructura del proyecto

```text
EDA_IA_PRODUCTIVIDAD_ESPANA/
├── src/
│   ├── main.ipynb                 # Análisis reproducible, gráficos y hallazgos
│   ├── data/
│   │   ├── raw/                   # CSV originales del INE y Eurostat
│   │   └── processed/             # Datos preparados por el notebook
│   └── utils/
├── memoria/                       # Informe del proyecto
├── presentacion/                  # Material de exposición
└── README.md
```

## Limitaciones

- Las definiciones de indicadores y la clasificación sectorial pueden variar entre años; concretamente **2026 utiliza una clasificación sectorial diferente**.
- Algunos indicadores del INE utilizan diferentes poblaciones de referencia. Por ello, los porcentajes de tecnologías, aplicaciones y barreras de adopción deben interpretarse por separado y no necesariamente representan al conjunto de empresas españolas. Queda pendiente verificar las notas específicas de las tablas originales. Es decir, se debe prestar atención a los gráficos de H4 ya que falta información sobre qué significa cada porcentaje y a qué empresas representa.
- Las series de adopción del INE y de Eurostat no son idénticas; la comparación internacional utiliza exclusivamente Eurostat.
- Los datos de adopción y productividad son agregados y tienen coberturas poblacionales diferentes.
- La comparación temporal de H5 dispone de solo **tres años comunes (2023–2025)** y enfrenta indicadores con diferentes coberturas; no mide el efecto de la IA ni permite inferir causalidad.
