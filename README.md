# Proyecto de Análisis de Datos 'PIDA' Cristian Moreira para Henry.

![Imagen del Proyecto](imagenes/ElitianTelec.png)

## Descripción del Proyecto

Este proyecto fue realizado en mi rol como **Data Analyst**. Mi tarea principal fue analizar datos relacionados con el acceso a internet en diferentes localidades, utilizando varias métricas y KPIs para evaluar la cobertura y la equidad en la distribución de servicios de internet. Mi análisis se centró en identificar áreas de mejora en la infraestructura y proponer estrategias para optimizar el acceso a internet en distintas regiones.

## Contexto del Proyecto

El objetivo principal del proyecto es analizar el acceso a internet en diversas localidades y medir la efectividad de la compañía sobre las políticas actuales mediante indicadores clave de rendimiento (KPIs). Los KPIs que se definió fueron los siguientes:

1. **Incrementar el Acceso a Internet por 2% por cada 100 Hogares**:
   - Este KPI mide el aumento en el acceso a internet por cada 100 hogares en cada provincia. Se calcula con la fórmula:
     \[
     \text{KPI} = \left(\frac{\text{Nuevo Acceso} - \text{Acceso Actual}}{\text{Acceso Actual}}\right) \times 100
     \]
   - **Objetivo**: Incrementar el acceso a internet en un 2% por cada 100 hogares para el próximo trimestre.

2. **Reducción de la Variabilidad de Velocidad entre Clusters**:
   - Este KPI se enfoca en reducir la variabilidad de la velocidad promedio de internet entre diferentes clusters dentro de una provincia o partido. Se pretende identificar y minimizar las diferencias significativas en la calidad del acceso a internet dentro de las áreas agrupadas.
   - **Objetivo**: Identificar y reducir áreas con alta variabilidad en la velocidad de internet para mejorar la consistencia de la infraestructura.

3. **Acceso Equitativo a Internet por Tecnología**:
   - Este KPI mide la distribución del acceso a diferentes tecnologías de internet (ADSL, Cablemodem, Fibra Óptica, Wireless, etc.) en relación con la población y la ubicación geográfica. El objetivo es identificar desigualdades en la distribución tecnológica y proponer mejoras en la infraestructura.
   - **Objetivo**: Asegurar que todas las localidades tengan acceso equitativo a tecnologías avanzadas de internet.

## Estructura del Proyecto

La estructura del proyecto en GitHub está organizado en las siguientes carpetas y archivos:

- **`/dashboards`**: Archivos de los dashboards utilizados para visualizar los KPIs y el análisis.
  - `PresentacionPIDA-Henry-CM.pbix`: Archivo de PowerBI con las visualizaciones y KPIs.
- **`/datasets`**: Contiene los archivos de datos utilizados para el análisis.
  - `/datasets/procesado`
  - `acceso_velocidad_y_tecnologia_con_mapa.csv, acctec_hogares_mediabajada_ingresos.csv, mapa_conectividad.csv, velocidad_promedio_zonas_similares.csv`: Archivos principales que importe y exporte para mis analisis.
- **`/notebooks`**: Incluye los cuadernos de Jupyter con el análisis de datos.
  - `eda_mapa.ipynb`: Análisis exploratorio de datos.
  - `etleda_hoja1.csv`: Archivo csv que creo desde el analisis 'etleda_hoja1.ipynb'
  - `etleda_hoja1.ipynb`: Análisis exploratorio de datos y cálculo de KPI 2 y visualización.
  - `etleda_hoja2.ipynb`: Análisis exploratorio de datos y cálculo de KPI 3 y visualización.
  - `etleda_kpi_henry.ipynb`: Análisis exploratorio de datos y cálculo de KPI 1 y visualización.
- **`/pilabs2`**: Contiene los archivos del entorno virtual.
- **`/reports`**: Carpeta vacia
- **`/src`**: Contiene el requirements.txt


## Reporte de Análisis

El informe de análisis se basa en los dashboards creados en PowerBI y los cuadernos de Jupyter. El análisis incluye:

- **Tendencias de Crecimiento**: Gráficos de líneas o áreas que muestran la evolución de los ingresos y el acceso a internet a lo largo del tiempo.
- **Variabilidad de Velocidad**: Visualización de la variabilidad en la velocidad de internet entre clusters y provincias.
- **Acceso por Tecnología**: Distribución del acceso a diferentes tecnologías de internet y su relación con la población y la ubicación geográfica.

## Funcionalidad de los KPIs

Cada KPI se visualiza y mide a través de gráficos específicos en PowerBI y Jupyter:

1. **Incremento del Acceso a Internet**: Muestra el porcentaje de aumento esperado en el acceso a internet.
2. **Reducción de Variabilidad de Velocidad**: Mide la consistencia de la velocidad de internet entre diferentes áreas.
3. **Acceso Equitativo por Tecnología**: Evalúa la distribución de tecnologías de internet y propone mejoras para equilibrar el acceso.

## Conclusión

Este proyecto intenta proporcionar una visión integral del acceso a internet en diferentes localidades y ayuda a identificar áreas críticas que requieren atención para mejorar la infraestructura y asegurar un acceso equitativo a todas las tecnologías de internet.

Gracias por tu tiempo de lectura.