# Análisis de Acceso a Internet en Argentina — PIDA

![Banner del proyecto](imagenes/ElitianTelec.png)

**Proyecto Individual de Análisis de Datos** desarrollado en el bootcamp [Henry](https://www.soyhenry.com/) en el rol de Data Analyst.

---

## Descripción

Este proyecto analiza el estado del acceso a internet en Argentina utilizando datos oficiales del **ENACOM** (Ente Nacional de Comunicaciones). El objetivo es medir la cobertura, calidad y equidad en la distribución de servicios de internet a través de KPIs accionables, e identificar oportunidades de mejora en la infraestructura por provincia y localidad.

---

## Stack tecnológico

| Herramienta | Uso |
|---|---|
| Python 3.11 | ETL, EDA y cálculo de KPIs |
| Pandas / NumPy | Manipulación de datos |
| Matplotlib / Seaborn | Visualizaciones exploratorias |
| Scikit-learn | Clustering K-Means |
| GeoPandas / Folium | Análisis y visualización geoespacial |
| Power BI | Dashboard interactivo |
| Jupyter Notebooks | Documentación del análisis |

---

## KPIs definidos

### KPI 1 — Incremento del acceso a internet por hogar
Mide el aumento trimestral en el acceso a internet por cada 100 hogares, por provincia.

```
KPI = ((Nuevo Acceso - Acceso Actual) / Acceso Actual) * 100
```

**Objetivo:** crecer un 2% cada trimestre.

### KPI 2 — Reducción de variabilidad de velocidad entre clusters
Identifica zonas con alta dispersión en la velocidad media de bajada, agrupando localidades por similitud mediante K-Means.

**Objetivo:** reducir la brecha de velocidad entre clusters dentro de cada provincia.

### KPI 3 — Equidad en el acceso por tecnología
Mide la distribución de tecnologías (ADSL, Cablemodem, Fibra Óptica, Wireless) en relación con la población y la ubicación geográfica.

**Objetivo:** detectar provincias con escasa penetración de tecnologías modernas y proponer mejoras de infraestructura.

---

## Estructura del proyecto

```
Henry-PIDA-CM/
├── datasets/
│   ├── Internet.xlsx
│   ├── Telefonia_movil.xlsx
│   ├── telefonia_fija.xlsx
│   ├── Television.xlsx
│   ├── Portabilidad.xlsx
│   ├── servicios_postales.xlsx
│   ├── mapa_conectividad.xlsx
│   └── procesado/              ← CSVs generados por los notebooks
├── notebooks/
│   ├── etleda_kpi_henry.ipynb  ← ETL + EDA + KPI 1
│   ├── etleda_hoja1.ipynb      ← ETL + EDA + KPI 2
│   ├── etleda_hoja2.ipynb      ← ETL + EDA + KPI 3
│   └── eda_mapa.ipynb          ← Análisis geoespacial
├── dashboard/
│   └── PresentacionPIDA-Henry-CM.pbix
├── imagenes/
├── src/
│   └── requirements.txt
└── README.md
```

---

## Cómo ejecutar el proyecto

**1. Clonar el repositorio**
```bash
git clone https://github.com/moreiracristian/Henry-PIDA-CM.git
cd Henry-PIDA-CM
```

**2. Crear y activar un entorno virtual**
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate
```

**3. Instalar dependencias**
```bash
pip install -r requirements.txt
```

**4. Ejecutar los notebooks en este orden**
```
1. notebooks/etleda_kpi_henry.ipynb   → genera acctec_hogares_mediabajada_ingresos.csv
2. notebooks/etleda_hoja1.ipynb       → genera velocidad_promedio_zonas_similares.csv
3. notebooks/etleda_hoja2.ipynb       → genera acceso_velocidad_y_tecnologia_con_mapa.csv
4. notebooks/eda_mapa.ipynb           → análisis geoespacial (requiere mapa_conectividad.csv)
```

**5. Dashboard**
Abrir `dashboard/PresentacionPIDA-Henry-CM.pbix` con Power BI Desktop.

---

## Fuente de datos

Todos los datasets provienen del portal de datos abiertos del **ENACOM**:
[https://indicadores.enacom.gob.ar/datos-abiertos](https://indicadores.enacom.gob.ar/datos-abiertos)

---

## Hallazgos principales

- El acceso a internet por hogar creció de forma sostenida entre 2014 y 2024, con una aceleración marcada a partir de 2020 (pandemia).
- Existe una alta variabilidad en la velocidad media de bajada entre provincias del interior y el área metropolitana de Buenos Aires.
- La tecnología ADSL muestra una tendencia decreciente, mientras que Cablemodem y Fibra Óptica ganan participación. Sin embargo, muchas provincias aún dependen mayoritariamente de tecnologías legacy.
- Las localidades con menor densidad poblacional presentan las mayores brechas de conectividad y acceso a tecnologías modernas.

---

## Autor

**Cristian Moreira**
[GitHub](https://github.com/moreiracristian) · [LinkedIn](https://www.linkedin.com/in/moreiracristian)
