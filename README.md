# ProyectoEBAC_FINAL
Entrga Final del preoyecto con datos de empresa aliada para la certificación de Ciencia de datos
# Proyecto de Análisis de Ventas

Este proyecto tiene como objetivo analizar el comportamiento de ventas de una empresa a partir de distintas fuentes de datos relacionadas con productos, categorías, segmentos, calendario y ventas. El análisis integra procesos de limpieza, transformación, exploración, segmentación, consulta en SQL, visualización en Power BI y predicción de ventas mediante modelos de series de tiempo.

## Objetivo del proyecto

El propósito principal del proyecto es transformar datos comerciales dispersos en información útil para la toma de decisiones. A través del análisis se busca identificar patrones de ventas, regiones con mayor desempeño, productos clave, segmentos relevantes y posibles oportunidades de mejora dentro de la estrategia comercial.

## Fuentes de datos

El proyecto utiliza las siguientes tablas:

* `FACT_SALES`: tabla principal de ventas.
* `DIM_PRODUCT`: información de productos.
* `DIM_SEGMENT`: información de segmentos.
* `DIM_CATEGORY`: información de categorías.
* `DIM_CALENDAR`: información de fechas y semanas.

Estas tablas fueron cargadas desde archivos CSV y Excel, procesadas en Python y posteriormente utilizadas para análisis en SQL Server y Power BI.

## Herramientas utilizadas

* **Python**: limpieza, transformación, análisis exploratorio, clustering y modelado predictivo.
* **Pandas**: manipulación y consolidación de datos.
* **Matplotlib y Seaborn**: visualización de datos.
* **Scikit-learn**: aplicación de K-Means para segmentación de productos.
* **Statsmodels**: implementación del modelo ARIMA.
* **SQL Server**: creación de base de datos y consultas analíticas.
* **Power BI**: construcción de dashboard interactivo.

## Estructura general del proyecto

El proyecto se desarrolló en las siguientes etapas:

## 1. Limpieza y transformación de datos

En esta etapa se cargaron los archivos originales y se realizó una limpieza inicial de las tablas. Se revisaron valores nulos, duplicados, tipos de datos y consistencia en los nombres de columnas.

También se estandarizaron textos, fechas y variables numéricas. Para facilitar la unión entre las tablas de ventas y productos, se creó una clave homologada llamada `ITEM_KEY`, utilizada como identificador principal del producto.

## 2. Consolidación de datos

Las tablas fueron integradas para construir una base final enriquecida. La tabla de ventas fue relacionada con la información de calendario, productos, categorías y segmentos.

Durante esta etapa se identificó que la región `TOTAL AUTOS SCANNING MEXICO` funcionaba como un total nacional agregado. Por esta razón, fue separada del análisis regional para evitar duplicar ventas. El análisis principal se realizó con las áreas reales de venta.

## 3. Análisis exploratorio de datos

Se realizó un análisis exploratorio para comprender el comportamiento general de las ventas. Se analizaron ventas por región, segmento, formato, marca y producto.

Entre los principales hallazgos se observó que el conjunto de datos corresponde a la categoría general de tratamiento y sanitización de telas. También se detectaron diferencias importantes entre regiones, así como productos con mayor participación en el valor total de ventas.

Se utilizaron visualizaciones como:

* Gráficos de barras.
* Gráficos de líneas.
* Histogramas.
* Boxplots.
* Visualizaciones con escala logarítmica para interpretar valores atípicos.

## 4. Segmentación de productos con K-Means

Se aplicó el algoritmo K-Means para segmentar los productos de acuerdo con su comportamiento comercial. Las variables utilizadas incluyeron ventas totales, unidades vendidas, semanas activas y presencia regional.

Se identificaron cuatro grupos principales:

* Productos de volumen acumulado.
* Productos líder.
* Productos de presencia específica.
* Productos de baja contribución.

Esta segmentación permitió distinguir entre productos que generan ventas por amplitud de catálogo y productos que, aunque son pocos, tienen alto impacto comercial.

## 5. Análisis con SQL Server

Las tablas limpias fueron exportadas desde Python en formato CSV y cargadas en SQL Server. Posteriormente, se ejecutaron consultas para validar los datos y analizar ventas desde diferentes dimensiones.

Algunas consultas realizadas incluyeron:

* Ventas por región.
* Ventas por segmento.
* Ventas por marca.
* Top de productos por ventas.
* Resumen de productos por cluster.

Esta etapa permitió validar los resultados obtenidos en Python y reforzar el análisis mediante consultas SQL.

## 6. Dashboard en Power BI

Se construyó un dashboard interactivo en Power BI con distintas páginas de análisis:

* Resumen de ventas.
* Ventas por región.
* Análisis de productos líderes.
* Análisis de clusters.

El dashboard incluye visualizaciones como tarjetas de indicadores, gráficos de líneas, barras, dona y matrices dinámicas.

También se integraron filtros interactivos por año, trimestre, fecha, formato, segmento, marca y fabricante. Además, se agregaron botones de navegación y bookmarks para facilitar la exploración del reporte.

## 7. Predicción de ventas con ARIMA

Para la predicción de ventas se utilizó la mayor granularidad temporal disponible en el dataset: ventas semanales.

Antes de entrenar el modelo, se aplicó la prueba Dickey-Fuller para evaluar la estacionariedad de la serie. La serie original no fue estacionaria y la primera diferenciación no fue suficiente, por lo que se utilizó una segunda diferenciación.

Se probaron distintas configuraciones de ARIMA y se compararon mediante métricas como:

* MAE.
* MSE.
* RMSE.

El mejor modelo probado fue ARIMA(2,2,2). El modelo logró capturar la tendencia general de las ventas, aunque presentó limitaciones para anticipar picos o caídas abruptas. Por esta razón, la predicción se interpreta como una referencia de tendencia y no como una estimación exacta.

## Principales hallazgos

* `TOTAL AUTOS SCANNING MEXICO` representa un total nacional agregado y no debe tratarse como una región independiente.
* Las ventas regionales presentan diferencias relevantes entre áreas.
* Algunos productos concentran una parte importante del valor total de ventas.
* Los productos líder tienen alto impacto comercial aunque representan pocos artículos.
* El clustering permitió clasificar los productos en grupos con comportamientos comerciales distintos.
* El modelo ARIMA tiene desempeño moderado y resulta útil para observar tendencias generales.

## Recomendaciones

* Mantener separado el análisis regional del total nacional agregado para evitar duplicidad de ventas.
* Dar seguimiento especial a los productos líder por su alto impacto comercial.
* Revisar los productos de baja contribución para evaluar oportunidades de ajuste, promoción o depuración.
* Utilizar el dashboard de Power BI como herramienta de monitoreo comercial.
* Ampliar el histórico de ventas para mejorar la estabilidad de los modelos predictivos.
* Incorporar variables externas como promociones, inventario, campañas o estacionalidad para mejorar la predicción.

## Futuras mejoras

Como mejoras futuras, se recomienda incorporar más periodos históricos y variables adicionales que ayuden a explicar mejor los cambios en la demanda. También sería útil probar modelos más avanzados como SARIMA, Random Forest, XGBoost o modelos híbridos que combinen variables temporales y comerciales.

El dashboard también podría ampliarse con páginas enfocadas en rentabilidad, desempeño por fabricante, análisis por marca y seguimiento de productos estratégicos.

## Archivos generados

Durante el desarrollo del proyecto se generaron archivos limpios y preparados para SQL Server y Power BI, entre ellos:

* `FACT_SALES_CLEAN_AREAS.csv`
* `FACT_SALES_CLEAN_MEXICO.csv`
* `PRODUCT_CLUSTER.csv`
* `RESUMEN_REGION.csv`
* `RESUMEN_SEGMENTO.csv`
* `RESUMEN_MARCA.csv`
* `RESUMEN_CLUSTERS.csv`
* `BASE_POWERBI_VENTAS.csv`

## Autor
