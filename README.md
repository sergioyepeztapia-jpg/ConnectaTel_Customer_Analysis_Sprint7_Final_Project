# 📊 ConnectaTel Customer Analysis

## 📌 Descripción del proyecto

Este proyecto presenta un análisis exploratorio de datos de **ConnectaTel**, una Empresa de Telecomunicaciones con operaciones en Latinoamérica.

El objetivo principal es analizar el comportamiento de los clientes, identificar patrones de uso, segmentar la base de usuarios según edad y nivel de actividad, detectar comportamientos atípicos y generar recomendaciones de negocio que puedan contribuir a mejorar la oferta comercial y la toma de decisiones basada en datos.

El análisis fue desarrollado como proyecto final del Sprint 7 del programa de **Data Analyst de TripleTen**.

---

## 🎯 Objetivos

- Evaluar la calidad de los datos e identificar valores faltantes, sentinels e inconsistencias.
- Analizar las características generales de los clientes y su comportamiento de uso.
- Estudiar las distribuciones de llamadas, mensajes y minutos de llamada.
- Detectar valores atípicos mediante análisis estadístico y visual.
- Segmentar a los clientes por edad y nivel de uso.
- Identificar grupos relevantes desde una perspectiva comercial.
- Traducir los resultados del análisis en recomendaciones accionables para stakeholders.

---

## 🗂️ Datasets utilizados

El análisis utiliza tres datasets:

### `plans.csv`
Contiene información sobre los planes comerciales disponibles, incluyendo:

- nombre del plan,
- mensajes incluidos,
- GB incluidos por mes,
- minutos incluidos,
- tarifa mensual,
- costos adicionales por GB, mensaje y minuto.

### `users_latam.csv`
Contiene información de los clientes:

- identificador del usuario,
- nombre y apellido,
- edad,
- ciudad,
- fecha de registro,
- plan contratado,
- fecha de baja.

### `usage.csv`
Contiene los registros de actividad de los usuarios:

- identificador del evento,
- identificador del usuario,
- tipo de actividad (`call` o `text`),
- fecha,
- duración de llamadas,
- longitud de mensajes.

---

## 🔎 Etapas del análisis

El proyecto se desarrolló siguiendo las siguientes etapas:

1. **Carga e inspección inicial de datos**
2. **Evaluación de estructura, tipos de datos y valores faltantes**
3. **Identificación de valores inválidos y sentinels**
4. **Conversión y validación de fechas**
5. **Limpieza y preparación de datos**
6. **Agregación de métricas de uso por cliente**
7. **Análisis exploratorio de datos (EDA)**
8. **Visualización mediante histogramas y boxplots**
9. **Detección de valores atípicos mediante IQR**
10. **Segmentación por edad y nivel de uso**
11. **Interpretación ejecutiva y recomendaciones de negocio**

---

## 🧹 Calidad y preparación de los datos

Durante la exploración se identificaron diferentes problemas de calidad.

- La columna `city` contenía **469 valores nulos (11.73%)** y **96 registros con `?` (2.40%)**. Después de unificar ambos casos, se identificaron **565 usuarios sin una ciudad válida (14.13%)**.
- En `age` se detectaron valores sentinel de **-999**, los cuales fueron reemplazados utilizando la mediana calculada a partir de las edades válidas.
- En `reg_date` se encontraron **40 registros correspondientes a 2026 (1.00%)**, fuera del periodo esperado de los datos, por lo que fueron tratados como valores faltantes.
- En `usage`, la columna `date` contenía **50 valores nulos (0.125%)**.
- `duration` presentó **22,076 valores nulos (55.19%)** y `length` **17,896 (44.74%)**. Se comprobó que estos valores faltantes están relacionados principalmente con el tipo de evento (`call` o `text`), por lo que no fueron imputados arbitrariamente.
- También se detectaron **16 registros de texto con duración** y **12 registros de llamada con longitud**, considerados pequeñas inconsistencias en los datos.
- `churn_date` presentó **3,534 valores nulos (88.35%)**. Debido a que la ausencia de esta fecha puede corresponder a clientes sin una baja registrada, no se imputaron valores artificiales.

---

## 👥 Segmentación de clientes

### Segmentación por edad

Los clientes fueron clasificados en tres grupos:

- **Joven:** menores de 30 años.
- **Adulto:** entre 30 y 59 años.
- **Adulto Mayor:** 60 años o más.

La distribución obtenida fue:

| Segmento | Usuarios | Porcentaje |
|---|---:|---:|
| Adulto | 2,018 | 50.45% |
| Adulto Mayor | 1,222 | 30.55% |
| Joven | 760 | 19.00% |

El **81% de los clientes tiene 30 años o más**, mostrando una concentración importante de la base en los segmentos Adulto y Adulto Mayor.

### Segmentación por nivel de uso

Los usuarios también fueron clasificados según su cantidad de llamadas y mensajes:

- **Bajo uso:** menos de 5 llamadas y menos de 5 mensajes.
- **Uso medio:** menos de 10 llamadas y menos de 10 mensajes, excluyendo previamente a los usuarios clasificados como Bajo uso.
- **Alto uso:** usuarios restantes con niveles superiores de actividad según los criterios definidos.

| Segmento | Usuarios | Porcentaje |
|---|---:|---:|
| Uso medio | 2,943 | 73.58% |
| Bajo uso | 778 | 19.45% |
| Alto uso | 279 | 6.98% |

El segmento de **Uso medio representa aproximadamente tres de cada cuatro clientes**, convirtiéndose en el grupo de mayor volumen dentro de la base analizada.

---

## 📈 Principales hallazgos

- El plan **Básico representa 64.875%** de los clientes, mientras que el plan **Premium representa 35.125%**.
- La distribución de edades se encuentra entre **18 y 79 años**, sin un sesgo marcado después del tratamiento de valores inválidos.
- La cantidad de mensajes se concentra principalmente alrededor de **4 a 7 mensajes**, con una ligera asimetría hacia valores superiores.
- La cantidad de llamadas se concentra principalmente alrededor de **3 a 6 llamadas**.
- Los minutos de llamada presentan una distribución claramente sesgada hacia la derecha, con una cola de usuarios de consumo elevado.
- Las visualizaciones no muestran por sí solas diferencias suficientemente marcadas entre los planes Básico y Premium como para concluir que uno presenta mayor propensión de uso.

---

## ⚠️ Valores atípicos

Mediante el método del rango intercuartílico (**IQR**) se obtuvieron los siguientes límites superiores:

| Métrica | Límite superior IQR | Máximo observado |
|---|---:|---:|
| Mensajes | 11.5 | 17 |
| Llamadas | 10.5 | 15 |
| Minutos de llamada | 61.8575 | 155.69 |

Los valores atípicos fueron conservados porque representan comportamientos de uso plausibles y no existe evidencia suficiente para considerarlos errores.

Estos usuarios pueden ser especialmente relevantes desde una perspectiva comercial, ya que podrían representar clientes con necesidades de consumo diferentes a las del usuario promedio.

---

## 💡 Recomendaciones de negocio

1. **Evaluar una oferta orientada al segmento de Uso medio**, que representa el 73.58% de la base de clientes.

2. **Analizar con mayor profundidad a los usuarios de Alto uso y a los clientes con consumos extremos**, especialmente aquellos con una cantidad elevada de minutos de llamada, para identificar oportunidades de migración, paquetes adicionales o beneficios específicos.

3. **Investigar el segmento de Bajo uso** para determinar si su menor actividad responde a necesidades naturalmente reducidas o a una baja utilización del servicio, evitando asumir automáticamente que bajo uso significa insatisfacción.

4. **Profundizar el análisis cruzando edad, nivel de uso y plan contratado** antes de diseñar campañas dirigidas a segmentos etarios específicos.

5. **Fortalecer los controles de calidad de datos**, especialmente en ciudad, fechas y variables asociadas al tipo de evento, para reducir sentinels, fechas fuera de rango e inconsistencias.

---

## 🛠️ Tecnologías utilizadas

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Jupyter Notebook**
- **Git / GitHub**

---

## ▶️ Cómo ejecutar el proyecto

1. Descarga o clona este repositorio.
2. Abre el archivo:

   `ConnectaTel_Customer_Analysis_Sprint7_Final_Project.ipynb`

3. Ejecuta el notebook utilizando **Jupyter Notebook**, **JupyterLab** o un entorno compatible.
4. Asegúrate de contar con las librerías necesarias:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

5. Los archivos de datos utilizados por el notebook deben estar disponibles en las rutas correspondientes antes de ejecutar las celdas de carga.

> **Nota:** Los datasets originales utilizados durante el proyecto pueden depender del entorno educativo de TripleTen. Si se ejecuta el notebook fuera de dicho entorno, puede ser necesario actualizar las rutas utilizadas en `pd.read_csv()`.

---

## 🔁 Reproducción del análisis

Para reproducir correctamente los resultados:

1. Carga los tres datasets.
2. Ejecuta las celdas del notebook en orden.
3. Realiza la limpieza y transformación de los datos.
4. Construye el perfil agregado por usuario.
5. Ejecuta el análisis exploratorio y las visualizaciones.
6. Genera las segmentaciones de edad y nivel de uso.
7. Revisa los resultados y conclusiones ejecutivas.

El notebook fue validado mediante una **ejecución completa desde un kernel reiniciado**, comprobando que todas las celdas se ejecutan correctamente en orden.

---

## 👤 Autor

**Sergio Yépez Tapia**

Ingeniero en Telecomunicaciones y Electrónica | Data Analytics

Proyecto desarrollado como parte del programa de **Data Analyst de TripleTen**.
