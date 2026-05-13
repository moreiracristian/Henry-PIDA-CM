# Guía de mejoras Power BI — PIDA

## Fuentes de datos a conectar (en orden)

| Archivo | Tabla sugerida en Power BI |
|---|---|
| `datasets/procesado/acctec_hogares_mediabajada_ingresos.csv` | `AccesoIngresos` |
| `datasets/procesado/velocidad_promedio_zonas_similares.csv` | `VelocidadClusters` |
| `datasets/procesado/acceso_velocidad_y_tecnologia_con_mapa.csv` | `TecnologiaMapa` |
| `datasets/procesado/mapa_conectividad.csv` | `MapaConectividad` |

---

## Medidas DAX — copiar y pegar en Power BI

> Ir a **Inicio → Nueva medida** y pegar cada bloque.

---

### Tabla: AccesoIngresos

```dax
// Acceso al último trimestre disponible (2024 Q1 = 78,89)
Acceso Ultimo Periodo =
CALCULATE(
    MAX(AccesoIngresos[Accesos por cada 100 hogares]),
    FILTER(
        ALL(AccesoIngresos),
        AccesoIngresos[Año] = MAXX(ALL(AccesoIngresos), AccesoIngresos[Año])
    )
)

// Objetivo: +2% sobre el acceso actual
Acceso Objetivo 2pct =
[Acceso Ultimo Periodo] * 1.02

// KPI 1: variación real entre el último y penúltimo trimestre (en %)
KPI1 Variacion Real =
VAR UltimoAno = MAXX(ALL(AccesoIngresos), AccesoIngresos[Año])
VAR UltimoTrim = CALCULATE(
    MAX(AccesoIngresos[Trimestre]),
    AccesoIngresos[Año] = UltimoAno
)
VAR AccesoActual = CALCULATE(
    MAX(AccesoIngresos[Accesos por cada 100 hogares]),
    AccesoIngresos[Año] = UltimoAno,
    AccesoIngresos[Trimestre] = UltimoTrim
)
VAR AnoAnterior = IF(UltimoTrim = 1, UltimoAno - 1, UltimoAno)
VAR TrimAnterior = IF(UltimoTrim = 1, 4, UltimoTrim - 1)
VAR AccesoAnterior = CALCULATE(
    MAX(AccesoIngresos[Accesos por cada 100 hogares]),
    AccesoIngresos[Año] = AnoAnterior,
    AccesoIngresos[Trimestre] = TrimAnterior
)
RETURN
ROUND(DIVIDE(AccesoActual - AccesoAnterior, AccesoAnterior) * 100, 2)

// Ingresos totales (SUMA — usar en el gráfico de línea, NO el campo directo)
Total Ingresos Miles =
SUM(AccesoIngresos[Ingresos (miles de pesos)])

// Velocidad media de bajada promedio
Velocidad Promedio Nacional =
AVERAGE(AccesoIngresos[Mbps (Media de bajada)])
```

---

### Tabla: VelocidadClusters

```dax
// Velocidad promedio por cluster (usar en tarjeta con filtro de cluster)
Velocidad Promedio Cluster =
AVERAGE(VelocidadClusters[velocidad_promedio])

// Desvío estándar entre clusters (KPI 2 — variabilidad)
KPI2 Variabilidad =
STDEV.P(VelocidadClusters[velocidad_promedio])

// Objetivo: reducir variabilidad 10%
KPI2 Objetivo Reduccion =
[KPI2 Variabilidad] * 0.90
```

---

### Tabla: TecnologiaMapa

```dax
// % localidades con Fibra Óptica
Pct Fibra Optica =
DIVIDE(
    CALCULATE(COUNTROWS(TecnologiaMapa), TecnologiaMapa[fibra_optica_y] = "SI"),
    COUNTROWS(TecnologiaMapa)
) * 100

// % localidades con Cablemodem
Pct Cablemodem =
DIVIDE(
    CALCULATE(COUNTROWS(TecnologiaMapa), TecnologiaMapa[cablemodem_y] = "SI"),
    COUNTROWS(TecnologiaMapa)
) * 100

// % localidades con ADSL
Pct ADSL =
DIVIDE(
    CALCULATE(COUNTROWS(TecnologiaMapa), TecnologiaMapa[adsl_y] = "SI"),
    COUNTROWS(TecnologiaMapa)
) * 100

// % localidades con tecnología moderna (Fibra o Cablemodem)
Pct Tecnologia Moderna =
DIVIDE(
    CALCULATE(
        COUNTROWS(TecnologiaMapa),
        TecnologiaMapa[fibra_optica_y] = "SI" || TecnologiaMapa[cablemodem_y] = "SI"
    ),
    COUNTROWS(TecnologiaMapa)
) * 100
```

---

## Correcciones por página

### Página "KPI's" y "Reporte de análisis"
**Problema:** muestran Markdown crudo (`##`, `**`).
**Fix:** Seleccionar el cuadro de texto → eliminar `##` y `**` manualmente. Son decoradores de Markdown que Power BI no interpreta.

---

### Página "KPI Henry" (renombrar a "KPI 1 — Acceso por Hogar")

| Elemento | Problema | Fix |
|---|---|---|
| Tarjeta "KPI Incremento del 2%" | Muestra ~240803 (suma de campo numérico erróneo) | Reemplazar el campo por la medida `KPI1 Variacion Real` → mostrará el % real |
| Tarjeta "Aumento del 2%" | Valor incorrecto | Usar la medida `Acceso Objetivo 2pct` |
| Gráfico "Recuento de Trimestre por ADSL" | Usa COUNT en lugar de SUM | Click en el campo ADSL en el panel → cambiar agregación de **Recuento** a **Suma** |
| Gráfico de líneas (accesos cruzados) | Demasiadas series sin filtro | Eliminar la leyenda por Año → mostrar una sola línea promedio nacional |
| Sección "Geolocalización" vacía | Sin datos conectados | Agregar mapa: campo `Accesos por cada 100 hogares` sobre provincias |

---

### Página "KPI Reducción de variabilidad" (renombrar a "KPI 2 — Velocidad")

| Elemento | Problema | Fix |
|---|---|---|
| Slicer de provincias | Nombres en minúscula con guión bajo | En Power Query: columna `provincia` → Transformar → Capitalizar cada palabra |
| Slicer "Segmentación 0 / 2" | No se entiende | Renombrar el título del slicer a "Cluster" |
| Partidos cortados en gráfico de barras | Etiquetas truncadas | Aumentar el margen izquierdo del gráfico o activar etiquetas dentro de la barra |
| Tarjeta "Reducción de la Variabilidad = -5" | Sin unidad ni contexto | Agregar subtítulo: "Mbps menos que el cluster anterior" |

---

### Página "KPI Acceso equitativo" (renombrar a "KPI 3 — Tecnología")

| Elemento | Problema | Fix |
|---|---|---|
| Gráfico de línea "Ingresos" con caída brusca | Y-axis usa **Recuento** en lugar de **Suma** | Click en el campo → cambiar a **Suma** → usar medida `Total Ingresos Miles` |
| Mapa muestra el mundo entero | Sin zoom a Argentina | Formatear visual → Mapa → Auto-zoom: **Activado**. Si no alcanza: agregar filtro de página por país = Argentina |
| Torta con 24 porciones (provincias) | Ilegible | Reemplazar por **Gráfico de barras apiladas**: Eje X = provincia, Valores = `adsl_x`, `cablemodem_x`, `fibra_optica_x`, `wireless_x` |

---

### Página "Conclusión"
**Problema:** `## Conclusión` se ve como texto literal.
**Fix:** Borrar el `##` del cuadro de texto y reemplazar el párrafo genérico por:

> **Hallazgos clave:**
> - El acceso por hogar creció de 40 a 78,9 cada 100 hogares entre 2014 y 2024 (+97%).
> - La variabilidad de velocidad entre clusters es alta: desvío estándar de 80 Mbps entre localidades.
> - Solo el X% de las localidades tienen Fibra Óptica, concentrada en el AMBA y capitales provinciales.
> - El objetivo de 2% trimestral se cumple en la mayoría de los períodos analizados.

---

## Mejoras de diseño rápidas (10 minutos)

1. **Tema unificado:** Vista → Temas → elegir "Innovación" o "Ejecutivo" (oscuro)
2. **Renombrar tabs:**
   - `KPI's` → `Resumen`
   - `Reporte de analisis` → `Contexto`
   - `KPI Reducción de la variabilidad entre seg...` → `KPI 2 — Velocidad`
   - `KPI Henry` → `KPI 1 — Acceso`
   - `KPI Acceso equitativo` → `KPI 3 — Tecnología`
3. **Fuente de datos en pie:** insertar cuadro de texto en cada página → `Fuente: ENACOM — indicadores.enacom.gob.ar`
