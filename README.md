# 📊 Análisis del Precio en el Mercado de Alojamientos Airbnb

> Exploración, análisis estadístico y modelización del precio por noche en Airbnb en cinco ciudades europeas: **Madrid, Mallorca, Valencia, Sevilla y Milán**.

---

## 📊 Dashboard

![IMG_3955 2](https://github.com/user-attachments/assets/feac83f8-3291-4edd-8651-68b1c7917763)

> Vista general del dashboard interactivo desarrollado en Power BI.

> 📁 El archivo interactivo (`.pbix`) está disponible en la carpeta `/dashboard/`.

---

## 🧠 Descripción del Proyecto

Este proyecto realiza un análisis exhaustivo del mercado de alojamientos turísticos en Airbnb con el objetivo de identificar qué variables predicen mejor el precio por noche.

**Pregunta principal:**
> ¿Qué variables predicen mejor el precio por noche de un alojamiento en Airbnb?

**Contexto:** El alquiler turístico a través de plataformas como Airbnb ha transformado el mercado de alojamiento en las principales ciudades europeas. Comprender qué factores determinan el precio es relevante tanto para propietarios que fijan precios como para analistas que estudian el impacto del turismo en el mercado.

Este análisis demuestra que el precio en Airbnb está determinado principalmente por características estructurales del alojamiento y el contexto del mercado, mientras que los factores reputacionales tienen un impacto secundario.

**Técnicas y enfoques utilizados:**
- Limpieza y transformación de datos con `pandas` (pipeline en 3 pasos)
- Análisis exploratorio de datos (EDA): distribuciones, correlaciones, segmentación por ciudad y tipo
- Tests estadísticos no paramétricos: Shapiro-Wilk, Kruskal-Wallis, Mann-Whitney, Spearman
- Modelado explicativo: regresión lineal con `scikit-learn` (R² = 0,39 · MAE = 76,39 €)
- Visualización: `Matplotlib` y `Seaborn` (9 figuras exportadas)
- Dashboard interactivo: Power BI con KPIs, filtros y 10 visualizaciones
- Fuentes externas: Eurostat (`tour_occ_nin3`) para contexto turístico

---

## 📂 Estructura del Proyecto

```
Proyecto_Final/
│
├── data/
│   ├── raw/                        # Datos originales — intocables
│   │   ├── madrid_listings.csv
│   │   ├── mallorca_listings.csv
│   │   ├── valencia_listings.csv
│   │   ├── sevilla_listings.csv
│   │   ├── milan_listings.csv
│   │   └── turismo.csv             # Eurostat tour_occ_nin3
│   │
│   └── processed/                  # Datos transformados
│       ├── madrid_clean.csv
│       ├── mallorca_clean.csv
│       ├── valencia_clean.csv
│       ├── sevilla_clean.csv
│       ├── milan_clean.csv
│       ├── listings_merged.csv     # Concat + merge con Eurostat
│       └── listings_final.csv      # Dataset final (66.411 × 28)
│
├── notebooks/
│   ├── 01_limpieza_transformacion.ipynb
│   ├── 02_analisis_descriptivo.ipynb
│   ├── 03_analisis_estadistico.ipynb
│   └── 04_visualizaciones.ipynb
│
├── dashboard/
│   └── Dashboard_Alojamientos_Turisticos.pbix
│
├── reports/
│   ├── analisis_exhaustivo.md
│   ├── informe_analisis.pdf
│   └── figures/                    # Gráficos exportados
│
└── README.md
```

---

## ⚙️ Instalación y Requisitos

Este proyecto usa **Python 3.11** y requiere las siguientes bibliotecas:

```bash
# Clonar el repositorio
git clone https://github.com/carmenperalgil-cyber/Proyecto_Final.git
cd Proyecto_Final

# Instalar dependencias
pip install -r requirements.txt
```

**Contenido del `requirements.txt`:**

```
pandas>=2.0
numpy>=1.24
matplotlib>=3.7
seaborn>=0.12
scipy>=1.11
scikit-learn>=1.3
openpyxl>=3.1
jupyter>=1.0
```

**Para reproducir el análisis completo, ejecuta los notebooks en orden:**

```bash
jupyter notebook notebooks/01_limpieza_transformacion.ipynb
```

> ⚠️ Los archivos de datos originales deben colocarse en `data/raw/` antes de ejecutar el notebook 01. El resto de archivos se generan automáticamente a lo largo del pipeline.

---

## 📊 Resultados y Conclusiones

### Hallazgos principales

| Indicador | Valor |
|-----------|-------|
| Total alojamientos analizados | 66.411 (5 ciudades · 2 países) |
| Precio medio global | 178,72 €/noche |
| Precio mediano global | 130 €/noche |
| Ciudad más cara (mediana) | **Mallorca** — 239 €/noche |
| Ciudad más asequible (mediana) | **Valencia** — 101 €/noche |
| Predictor más fuerte del precio | Capacidad del alojamiento (`accommodates`, rho = 0,61) |
| R² del modelo de regresión | 0,39 — el modelo explica el 39% de la varianza |
| MAE del modelo | 76,39 € |

### Conclusiones

- **Mallorca** es el mercado más caro del conjunto analizado (mediana 239 €/noche, +137% sobre Valencia).
- **La capacidad** (`accommodates`, rho = 0,61) y **el número de baños** (coef. estandarizado +49,1) son las variables más asociadas al precio.
- **Las valoraciones** tienen efecto positivo real, pero débil (rho = 0,06); no discriminan bien el precio.
- **La disponibilidad** no explica el precio (rho = +0,001, p = 0,79).
- **El modelo lineal** (R² = 0,39, MAE = 76,39 €) confirma que los atributos físicos pesan más que los reputacionales.

> En conjunto, el precio de un alojamiento Airbnb está dominado por variables estructurales — capacidad, número de baños y dormitorios — junto con el contexto del mercado local. Los factores reputacionales tienen un impacto marginal y la disponibilidad no presenta capacidad explicativa relevante. Esto sugiere que el mercado Airbnb se comporta de forma similar al mercado inmobiliario tradicional, donde el valor está determinado principalmente por las características físicas del activo.

Estos resultados pueden ser utilizados por hosts para optimizar estrategias de pricing, priorizando mejoras estructurales del alojamiento frente a esfuerzos marginales en reputación.

---

## 🚀 Líneas Futuras de Trabajo

- Incorporar variables de localización exacta (distancia al centro, barrio) para mejorar el R² del modelo.
- Explorar modelos no lineales (Random Forest, Gradient Boosting) para capturar interacciones entre variables.
- Ampliar el análisis a más ciudades europeas para identificar patrones a escala continental.
- Incorporar datos de estacionalidad para analizar variación de precios a lo largo del año.
- Desarrollar un modelo de predicción de precio en producción (API REST).

---

## 🤝 Contribuciones

Este proyecto forma parte de un trabajo académico y no está abierto activamente a contribuciones externas.

---

## ✍️ Autores y Agradecimientos

**Autora:** Carmen Peral  
**Programa:** Bootcamp de Análisis de Datos — Módulo Python for Data

**Fuentes de datos:**
- [Inside Airbnb](http://insideairbnb.com) — datos de anuncios bajo licencia Creative Commons
- [Eurostat](https://ec.europa.eu/eurostat) — tabla `tour_occ_nin3`, pernoctaciones turísticas por región NUTS3

**Herramientas utilizadas:**
- Python 3.11 · pandas · numpy · scipy · scikit-learn · matplotlib · seaborn
- Power BI Desktop · Jupyter Notebook

---

## 📌 Nota

Este proyecto tiene un enfoque explicativo. No está diseñado como modelo predictivo en producción, sino como análisis para entender los factores que influyen en el precio de los alojamientos turísticos en Airbnb.
