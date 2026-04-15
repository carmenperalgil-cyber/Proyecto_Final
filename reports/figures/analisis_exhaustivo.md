# Análisis Exhaustivo del Dataset — listings_final.csv

Este documento presenta el análisis exhaustivo del dataset final `listings_final.csv`, compuesto por 66.411 anuncios de Airbnb en cinco ciudades europeas: Madrid, Mallorca, Valencia, Sevilla y Milán. El objetivo es describir la estructura del mercado, identificar patrones de precio y disponibilidad, y evaluar qué variables influyen más en el comportamiento del precio por noche.

El análisis sigue un orden progresivo: comienza por la composición y calidad del dato, avanza por el análisis descriptivo y la segmentación, contrasta hipótesis con tests estadísticos, y culmina con un modelo explicativo y una conclusión orientada a la pregunta principal del proyecto. Se apoya en un dashboard interactivo desarrollado en Power BI, que permite explorar los resultados de forma dinámica, facilitando la interpretación de los principales drivers del precio.

---

## 1. Composición del dataset

| Ciudad | País | Nº Anuncios | % del total |
|--------|------|-------------|-------------|
| Milán | Italia | 20.338 | 30,6% |
| Madrid | España | 18.741 | 28,2% |
| Mallorca | España | 12.919 | 19,5% |
| Sevilla | España | 7.505 | 11,3% |
| Valencia | España | 6.908 | 10,4% |
| **TOTAL** | | **66.411** | **100%** |

Milán y Madrid concentran el 58,8% del dataset. Mallorca, con menor volumen de anuncios, presenta la estructura de precios más diferenciada. Este dataset permite analizar tanto características estructurales de los alojamientos como factores contextuales del mercado turístico.

---

## 2. Calidad del dato

- **Nulos:** solo `host_antiguedad_años` presenta 111 nulos (0,17%) — ausencia legítima de fecha de registro que no afecta al análisis principal.
- **Duplicados:** 0 tras la limpieza global.
- **Variables clave sin nulos:** precio, ciudad, tipo de alojamiento, capacidad, disponibilidad, valoración media.

> **El dataset presenta una alta calidad estructural:** sin valores nulos en variables clave, lo que permite aplicar análisis estadísticos con fiabilidad. Este nivel de calidad permite aplicar directamente los análisis sin riesgo de sesgos por datos faltantes.

---

## 3. Análisis descriptivo

### 3.1 Precio por noche

| Ciudad | Media | Mediana | Desv. típica | Mínimo | Máximo |
|--------|-------|---------|--------------|--------|--------|
| Mallorca | 314,76 € | **239 €** | 257,56 € | 10 € | 2.000 € |
| Milán | 168,04 € | 124 € | 149,98 € | 9 € | 1.200 € |
| Sevilla | 151,07 € | 124 € | 112,92 € | 12 € | 1.145 € |
| Madrid | 131,33 € | 110 € | 96,48 € | 8 € | 773 € |
| Valencia | 114,39 € | **101 €** | 75,10 € | 8 € | 826 € |
| **Global** | **178,72 €** | **130 €** | — | 8 € | 2.000 € |

La distribución del precio presenta una fuerte asimetría a la derecha (asimetría = 3,75), lo que significa que la media global (178,72 €) no es representativa del precio típico — la mediana (130 €) es la métrica más adecuada. La elevada dispersión y asimetría indican la presencia de valores extremos y justifican el uso de medidas robustas como la mediana.

Mallorca destaca como mercado estructuralmente diferente: su precio mediano (239 €) es un **136,6% superior** al de Valencia (101 €). Esta distribución asimétrica es típica en mercados de alquiler turístico, donde un pequeño porcentaje de alojamientos premium eleva la media.

### 3.2 Precio por persona

| Ciudad | Media | Mediana |
|--------|-------|---------|
| Mallorca | 56,62 € | 47,6 € |
| Milán | 54,46 € | 41,0 € |
| Madrid | 43,49 € | 36,4 € |
| Sevilla | 42,99 € | 34,6 € |
| Valencia | 35,86 € | **30,0 €** |

Al normalizar el precio por la capacidad del alojamiento, la brecha entre ciudades se modera. Madrid y Milán presentan valores similares en precio por persona a pesar de sus diferencias en precio bruto. Esto sugiere que **parte de las diferencias entre ciudades se explica por el tamaño de los alojamientos**, no solo por el nivel de precios del mercado.

### 3.3 Tipos de alojamiento

| Tipo | Nº Anuncios | % | Precio Medio | Precio Mediano |
|------|-------------|---|--------------|----------------|
| Vivienda completa *(Entire home/apt)* | 55.256 | 83,2% | 196,70 € | 142 € |
| Habitación privada *(Private room)* | 10.815 | 16,3% | 89,06 € | 58 € |
| Habitación de hotel *(Hotel room)* | 115 | 0,2% | 184,01 € | 155 € |
| Habitación compartida *(Shared room)* | 225 | 0,3% | 71,40 € | 33 € |

La vivienda completa domina en todas las ciudades (>79%). **La dominancia de este tipo condiciona el comportamiento global del precio en el mercado.** En Sevilla, las habitaciones de hotel en Airbnb (232 € de mediana) superan a la vivienda completa (131 €), indicando que los hoteles sevillanos usan la plataforma para el segmento premium.

**Precio mediano por ciudad y tipo (€/noche):**

| Ciudad | Vivienda completa | Hotel | Hab. privada | Hab. compartida |
|--------|-------------------|-------|--------------|-----------------|
| Mallorca | 250 € | 211 € | 114 € | 184 € |
| Milán | 129 € | 183 € | 78 € | 41,5 € |
| Sevilla | 131 € | **232 €** | 60 € | 55 € |
| Madrid | 128 € | 152 € | 50 € | 29 € |
| Valencia | 113 € | 125 € | 46 € | 45,5 € |

### 3.4 Disponibilidad

| Ciudad | Media (días) | Mediana (días) |
|--------|--------------|----------------|
| Madrid | 212,7 | 245,0 |
| Milán | 203,4 | 214,0 |
| Valencia | 198,5 | 207,0 |
| Sevilla | 192,2 | 205,0 |
| Mallorca | 190,2 | 188,0 |

El **56,5%** de los anuncios tiene alta disponibilidad (>180 días/año). Mallorca presenta la menor disponibilidad media, coherente con su marcada estacionalidad estival. Madrid supera los 212 días de media, indicando un mercado activo durante todo el año.

### 3.5 Valoraciones

| Ciudad | Valoración media | Valoración mediana |
|--------|------------------|--------------------|
| Milán | 4,723 | 4,79 |
| Mallorca | 4,710 | 4,79 |
| Sevilla | 4,705 | 4,79 |
| Valencia | 4,681 | 4,79 |
| Madrid | 4,657 | 4,79 |

Las medianas son idénticas en todas las ciudades (4,79). Las valoraciones presentan muy poca variabilidad en el mercado Airbnb — los alojamientos con malas reseñas desaparecen de la plataforma, lo que comprime la distribución y elimina su capacidad discriminante. Esto limita su utilidad como variable explicativa del precio en modelos predictivos.

---

## 4. Perfil del host

### 4.1 Superhosts

| Ciudad | % Superhost | Mediana precio Superhost | Mediana precio No Superhost |
|--------|-------------|--------------------------|------------------------------|
| Sevilla | 39,1% | 129 € | 120 € |
| Valencia | 32,4% | 105 € | 99 € |
| Milán | 30,2% | 116 € | 128 € |
| Madrid | 25,2% | 113 € | 108 € |
| Mallorca | 25,4% | 240 € | 238,5 € |

### 4.2 Hosts profesionales y antigüedad

| Ciudad | % Host profesional |
|--------|-------------------|
| Mallorca | 64,7% |
| Madrid | 60,4% |
| Sevilla | 59,0% |
| Valencia | 49,1% |
| Milán | 48,3% |

- Antigüedad media: **7,34 años** · mediana: **8,0 años** · rango: 0,2–16,9 años
- El 50% de los hosts lleva más de 8 años en la plataforma, lo que indica un mercado con experiencia consolidada.

---

## 5. Top 5 barrios más caros por ciudad *(referencia geográfica)*

| Madrid | Mallorca | Milán | Sevilla | Valencia |
|--------|----------|-------|---------|----------|
| Recoletos — 173 € | Esporles — 478 € | SACCO — 262 € | Santa Cruz — 177 € | CARPESA — 360 € |
| Castellana — 172 € | Deyá — 451 € | DUOMO — 252 € | Prado/Parque M.ª Luisa — 164 € | FAITANAR — 178 € |
| Goya — 152 € | Marratxí — 352 € | BRERA — 209 € | Arenal — 160 € | EL PLA DEL REMEI — 158 € |
| Sol — 148 € | Consell — 347 € | GUASTALLA — 178 € | San Bartolomé — 151 € | MAHUELLA-TAULADELLA — 150 € |
| Jerónimos — 146 € | Bunyola — 319 € | MAGENTA–S. Vittore — 171 € | Museo — 148 € | PENYA-ROJA — 138 € |

*Precios medianos por barrio. Confirma la concentración de precios altos en zonas prime.*

---

## 6. Análisis estadístico

### 6.1 Normalidad — Shapiro-Wilk *(n = 5.000)*

- W = 0,6624 · p < 0,001 · asimetría = 3,747 · curtosis = 21,45

La distribución del precio no es normal. **Dado el gran tamaño de la muestra, incluso pequeñas desviaciones de la normalidad resultan estadísticamente significativas, por lo que se prioriza el uso de métodos no paramétricos en todo el análisis.**

### 6.2 H1 — Diferencias entre ciudades — Kruskal-Wallis

- H = 12.503,43 · p < 0,001

**✅ Confirmada.** Existen diferencias estadísticamente significativas entre los pares de ciudades analizados. **Esto confirma que la ciudad no solo introduce diferencias, sino que actúa como un factor estructural determinante del precio** — el mercado no es homogéneo y el precio depende fuertemente del contexto local.

| Par | Mediana A | Mediana B | Diferencia | p-valor |
|-----|-----------|-----------|------------|---------|
| Mallorca vs Valencia | 239 € | 101 € | +136,6% | <0,001 |
| Mallorca vs Madrid | 239 € | 110 € | +117,3% | <0,001 |
| Mallorca vs Milán | 239 € | 124 € | +92,7% | <0,001 |
| Mallorca vs Sevilla | 239 € | 124 € | +92,7% | <0,001 |
| Milán vs Valencia | 124 € | 101 € | +22,8% | <0,001 |
| Sevilla vs Valencia | 124 € | 101 € | +22,8% | <0,001 |
| Madrid vs Valencia | 110 € | 101 € | +8,9% | <0,001 |
| Milán vs Sevilla | 124 € | 124 € | 0,0% | 0,0003 |
| Madrid vs Milán | 110 € | 124 € | -11,3% | <0,001 |

### 6.3 H2 — Superhosts y precio — Mann-Whitney bilateral

- Superhost: mediana = 126 € · No Superhost: mediana = 131 € · p < 0,001

**⚠️ Resultado matizado — Paradoja de Simpson.** A nivel global los No Superhost tienen precio ligeramente mayor, pero dentro de cada ciudad los superhosts presentan precios iguales o superiores. La paradoja se explica por la composición: Mallorca (precios altos) tiene bajo porcentaje de superhosts, lo que invierte la tendencia global.

### 6.4 H3 — Disponibilidad y precio — Mann-Whitney bilateral

- Alta disponibilidad: mediana = 131 € · Baja: mediana = 128 € · p = 0,74

**❌ No confirmada.** Sin diferencias significativas. Correlación de Spearman: rho = +0,001.

### 6.5 H4 — Popularidad y valoración — Mann-Whitney unilateral

- Popular: mediana = 4,790 · No popular: mediana = 4,790 · p = 1,000

**❌ No confirmada.** Medianas idénticas. Las valoraciones presentan muy poca variabilidad y por eso pierden capacidad discriminante.

### 6.6 H5 — Correlaciones con el precio — Spearman

| Variable | Nombre descriptivo | Rho | p-valor | Sig. |
|----------|--------------------|-----|---------|------|
| `accommodates` | Capacidad del alojamiento | +0,606 | <0,001 | ✅ |
| `bedrooms` | Nº de dormitorios | +0,526 | <0,001 | ✅ |
| `beds` | Nº de camas | +0,522 | <0,001 | ✅ |
| `bathrooms` | Nº de baños | +0,454 | <0,001 | ✅ |
| `calculated_host_listings_count` | Anuncios activos del host | +0,222 | <0,001 | ✅ |
| `reviews_per_month` | Reseñas por mes | -0,181 | <0,001 | ✅ |
| `review_scores_location` | Valoración de ubicación | +0,142 | <0,001 | ✅ |
| `number_of_reviews` | Nº total de reseñas | -0,105 | <0,001 | ✅ |
| `minimum_nights` | Mínimo de noches | -0,104 | <0,001 | ✅ |
| `review_scores_rating` | Valoración media | +0,060 | <0,001 | ✅ |
| `availability_365` | Días disponibles/año | +0,001 | 0,789 | ❌ |

**✅ Confirmada.** La capacidad del alojamiento es la variable más correlacionada con el precio (rho = 0,61). Aunque casi todas las correlaciones resultan significativas por el tamaño muestral, **lo relevante es la magnitud del efecto**: las variables estructurales tienen una asociación prácticamente relevante; las de reputación son significativas pero con impacto real pequeño.

Esto refuerza la idea de que el precio está dominado por variables estructurales, mientras que las variables de comportamiento y reputación tienen un papel secundario.

---

## 7. Contexto turístico — Eurostat *(ciudades españolas)*

Los datos de pernoctaciones proceden de Eurostat (tabla `tour_occ_nin3`). El análisis se restringe a las ciudades españolas para mantener comparabilidad territorial. Milán se excluye al proceder de un marco estadístico diferente (ISTAT/Eurostat-Italia).

| Ciudad | Precio medio | Precio mediano | Pernoctaciones | Presión turística |
|--------|-------------|----------------|----------------|-------------------|
| Mallorca | 314,76 € | 239 € | 55,3 M | 1,000 |
| Madrid | 131,33 € | 110 € | 32,3 M | 0,585 |
| Valencia | 114,39 € | 101 € | 13,2 M | 0,238 |
| Sevilla | 151,07 € | 124 € | 10,2 M | 0,185 |

Correlación Spearman (pernoctaciones vs precio, España): **rho = 0,38** · p < 0,001.

La relación es positiva moderada pero no lineal: Madrid, con más turismo que Sevilla y Valencia, tiene precios similares. **Esto refuerza la idea de que el precio no depende únicamente de la demanda turística, sino también de la estructura de la oferta disponible.**

---

## 8. Modelo de regresión lineal

**Regresión lineal OLS · partición 80/20 · `random_state=42` · n = 66.411**

| Métrica | Valor |
|---------|-------|
| R² | 0,3927 |
| MAE | 76,39 € |

**El modelo captura parte relevante de la varianza (39,3%), pero existe una gran variabilidad no explicada, probablemente asociada a factores no observados como la ubicación exacta, la calidad del inmueble o la temporada de reserva.** Este resultado es esperable para un modelo explicativo simple sobre un mercado tan heterogéneo.

| Variable | Nombre descriptivo | Coef. bruto | Coef. estand. | Interpretación |
|----------|--------------------|-------------|---------------|----------------|
| `accommodates` | Capacidad | +26,16 € | +57,1 | Por cada persona adicional, el precio sube ~26 € |
| `bathrooms` | Nº baños | +54,41 € | +49,1 | Cada baño añade ~54 € (mayor impacto unitario) |
| `bedrooms` | Nº dormitorios | +13,87 € | +17,2 | Cada dormitorio añade ~14 € |
| `review_scores_rating` | Valoración media | +11,80 € | +4,7 | Efecto real pero pequeño |
| `number_of_reviews` | Nº reseñas | -0,11 € | -11,2 | Mayor rotación → alojamientos más baratos |
| `beds` | Nº camas | -5,58 € | -10,4 | Más camas sin más baños = menos exclusivo |
| `availability_365` | Disponibilidad | +0,03 € | +3,3 | Impacto prácticamente nulo |
| `calc_host_listings` | Anuncios del host | -0,004 € | -0,4 | Impacto mínimo |

A pesar de su capacidad explicativa, el modelo presenta limitaciones inherentes a su naturaleza lineal y a la ausencia de variables clave, por lo que sus resultados deben interpretarse como aproximaciones. Este comportamiento es consistente con la naturaleza del mercado, donde factores cualitativos no observados juegan un papel relevante.

---

## 9. Conclusión

El análisis confirma que el precio en Airbnb está determinado principalmente por factores estructurales del alojamiento, no por la reputación del host ni por la disponibilidad:

- **Mallorca** es el mercado más caro del conjunto analizado (mediana 239 €/noche, +137% sobre Valencia).
- **La capacidad** (`accommodates`, rho = 0,61) y **el número de baños** (coef. estandarizado +49,1) son las variables más asociadas al precio.
- **Las valoraciones** tienen efecto positivo real, pero débil (rho = 0,06); no discriminan bien el precio.
- **La disponibilidad** no explica el precio (rho = +0,001, p = 0,79).
- **El modelo lineal** (R² = 0,39, MAE = 76,39 €) confirma que los atributos físicos pesan más que los reputacionales.

> **En conjunto, el precio de un alojamiento Airbnb está explicado principalmente por sus características físicas — capacidad, número de baños y dormitorios — y por el mercado local (ciudad). Los factores reputacionales tienen un impacto secundario. Los resultados deben interpretarse como una aproximación basada en la información disponible.**
