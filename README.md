# Análisis de Perfil de Transporte

## Descripción del proyecto

Este proyecto corresponde a una prueba técnica de análisis de datos sobre un dataset de transporte.

El objetivo fue analizar la información disponible para obtener una visión general del perfil de envíos, identificando carriers principales, tiempos de entrega, lanes con mayor volumen, tendencias semanales y distribución de shipments por peso facturable.

El análisis fue realizado utilizando SQL Server para las consultas y Power BI Desktop para la visualización de resultados.

---

## Herramientas utilizadas

- SQL Server
- Power BI Desktop
- Excel / CSV
- GitHub
  
---

## Objetivos del análisis

Se desarrollaron consultas SQL para responder las siguientes consignas:

1. Obtener la cantidad total de shipments por trimestre, agrupados por carrier y ordenados por peso.
2. Calcular el promedio de días transcurridos entre la fecha de recogida y la fecha de entrega.
3. Identificar los lanes con mayor volumen.
4. Analizar la frecuencia de shipments y su tendencia semanal.
5. Clasificar los shipments por rangos de peso facturable.

---

## Consultas SQL

Las consultas utilizadas se encuentran en el archivo:

```text
sql/queries.sql
```

El dataset fue cargado en SQL Server en una tabla llamada:

```sql
dbo.Details
```

---

## Resultados SQL

### 1. Shipments por trimestre, carrier y peso total

Esta consulta agrupa los shipments por carrier, año y trimestre. Luego ordena el resultado según el peso total transportado.

![Consigna 1](images/01.png)

---

### 2. Promedio de días entre recogida y entrega

Esta consulta calcula el promedio de días entre la fecha de recogida y la fecha de entrega.

![Consigna 2](images/02.png)

---

### 3. Lanes con mayor volumen

Esta consulta identifica los lanes principales, definidos como combinación entre código postal de origen y código postal de destino.

![Consigna 3](images/03.png)

Durante el análisis se observaron algunos valores de volumen inusualmente altos (los tres primeros registros), por lo que sería recomendable validarlos con la fuente original antes de tomar decisiones finales. Ademas, se identificaron valores negativos muy grandes que pueden identificarse como outliers. 

---

### 4. Tendencia semanal de shipments

Esta consulta agrupa la cantidad de shipments por año y semana para observar la frecuencia de envíos a lo largo del tiempo.

![Consigna 4](images/04.png)

La evolución completa se presenta visualmente en la página Weekly Trends del reporte de Power BI.

---

### 5. Distribución por peso facturable

Esta consulta clasifica los shipments según los rangos de peso facturable definidos en la consigna.

![Consigna 5](images/05.png)
---

## Reporte en Power BI

El archivo de Power BI se encuentra en:

```text
powerbi/transport_profile_analysis.pbix
```

El reporte fue organizado en diferentes páginas para presentar cada parte del análisis de forma clara:

1. Overview
2. Carrier Analysis
3. Lane Analysis
4. Weekly Trends
5. Chargeable Weight Profile

---

## Vista general del dashboard

### 1. Overview

![Overview](images/01_overview.png)

Esta página resume los principales indicadores del dataset, como cantidad total de shipments, peso total, volumen total y promedio de días entre recogida y entrega.

---

### 2. Carrier Analysis

![Carrier Analysis](images/02_carrier_analysis.png)

Esta sección muestra el comportamiento de los shipments por carrier y trimestre.

El objetivo es identificar qué carriers concentran mayor cantidad de envíos y mayor peso transportado.

---

### 3. Lane Analysis

![Lane Analysis](images/03_lane_analysis.png)

Esta página permite analizar los lanes principales, definidos como combinaciones de código postal de origen y código postal de destino.

El objetivo es identificar las rutas con mayor volumen transportado.

---

### 4. Weekly Trends

![Weekly Trends](images/04_weekly_trends.png)

Esta sección muestra la evolución semanal de los shipments.

El objetivo es observar tendencias, variaciones y posibles picos de actividad a lo largo del período analizado.

---

### 5. Chargeable Weight Profile

![Chargeable Weight Profile](images/05_weight_brackets.png)

Esta página clasifica los shipments según los rangos de peso facturable definidos en la consigna.

---

## Principales resultados

A partir del análisis realizado, se pueden destacar los siguientes puntos:

- La actividad de transporte se concentra principalmente en determinados carriers.
- CARRIER 002 y CARRIER 001 concentran una parte importante del peso transportado.
- El promedio de días entre recogida y entrega es de aproximadamente 5.33 días.
- Existen lanes con volúmenes significativamente superiores al resto.
- La frecuencia semanal muestra variaciones en la actividad a lo largo del período analizado.
- La mayor parte de los shipments se concentra en los rangos de 50-500 Kg y 1000-5000 Kg de peso facturable.

---

## Observaciones sobre calidad de datos

Durante el análisis se identificaron algunos puntos a tener en cuenta:

- Algunas columnas numéricas fueron importadas como texto.
- Existen valores vacíos o faltantes en algunos campos.
- Se detectaron algunos valores de volumen negativos o inusualmente altos.
- Algunos Shipment ID aparecen en más de una fila, por lo que se utilizó `COUNT(DISTINCT SHIPMENT_ID)` cuando correspondía.
- Sería recomendable revisar los outliers antes de tomar decisiones finales basadas en volumen o coste.

---

## Desafíos encontrados

El principal desafío fue trabajar con un dataset que contenía diferentes formatos de datos.

Para evitar errores durante la carga, los datos fueron importados inicialmente como texto en SQL Server. Luego, dentro de las consultas, se realizaron conversiones básicas para calcular fechas, pesos, volúmenes y rangos.

Este enfoque permitió mantener el archivo original sin modificar y realizar el análisis de forma controlada.

---

## Información faltante para un análisis más completo

Para obtener una visión más completa del perfil de transporte, sería útil contar con información adicional como:

- Tipo de servicio o modo de transporte.
- SLA o tiempo objetivo de entrega.
- Estado del shipment.
- Cliente o unidad de negocio.
- Región o zona geográfica.
- Moneda del coste.
- Fechas planificadas vs fechas reales.
- Motivo de retrasos, si existieran.
- Tipo de producto transportado.

---

## Conclusión

El análisis permite obtener una primera visión del perfil de transporte del dataset, identificando carriers principales, lanes con mayor volumen, tiempos promedio de entrega, tendencias semanales y distribución por peso facturable.

Además, se identificaron algunos aspectos de calidad de datos que deberían revisarse para mejorar la precisión del análisis y permitir una toma de decisiones más completa.
