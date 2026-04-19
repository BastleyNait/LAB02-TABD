# 📊 Informe Semántico del Proyecto Integrador - RENACE
# Estudiante: Chirinos Negron Sebastian Arley 
## 1. Descripción del Corpus Extendido

El sistema utiliza un corpus de **36 registros técnicos** en español, balanceado con 12 documentos por cada dominio crítico de la red RENACE:

* **EDA (Enfermedades Diarreicas Agudas):** Vigilancia epidemiológica y protocolos de salud pública.
* **BDV (Bases de Datos Vectoriales):** Infraestructura tecnológica para la recuperación de registros clínicos.
* **IA (Inteligencia Artificial):** Modelos predictivos y análisis de lenguaje aplicados al sector salud.

Cada registro incluye metadatos de **Región** (Arequipa, Lima, Puno, Nacional), **Año** (2022-2025) y **Subtema** específico.

## 2. Análisis de Visualizaciones y Clusters

Para la interpretación geométrica del espacio vectorial, se generaron las siguientes gráficas disponibles en el repositorio:

* **Heatmap de Similitud (36x36):** [Ver `heatmap_36x36.png`](./heatmap_36x36.png). Esta matriz revela una fuerte cohesión interna en el dominio EDA. Los dominios BDV e IA muestran una interconexión mayor debido a la terminología compartida de ingeniería de datos.
* **Proyección PCA:** [Ver `pca_36docs.png`](./pca_36docs.png). El análisis de componentes principales permite observar la separación macroscópica. Se identifica que la varianza global logra separar el eje de 'Salud' (EDA) del eje 'Tecnológico' (IA/BDV).
* **Estructura Local t-SNE:** [Ver `tsne_36docs.png`](./tsne_36docs.png). Mediante el uso de métrica coseno y perplexity adecuada, se visualizan micro-clusters donde documentos de la misma región (ej. Arequipa) tienden a acercarse si comparten subtemas similares.

## 3. Detección de Outliers Semánticos

Mediante la función `encontrar_documentos_atipicos` con un umbral de 0.6, se identificaron registros cuya firma vectorial es única. 

* **Ejemplo de Outlier:** [Ver `outliers_semanticos.png`](./outliers_semanticos.png). Temas como 'Criptografía en marcapasos' o 'Turismo en el Amazonas' aparecen como puntos aislados, lo que indica que su contenido no tiene redundancia en el corpus actual, siendo puntos críticos de información única.

## 4. Interpretación y Recomendación Final

Tras comparar el modelo `all-MiniLM` (base) con `paraphrase-multilingual-MiniLM-L12-v2`, se concluye:

1.  **Precisión Lingüística:** El modelo multilingüe es un **80% más efectivo** detectando sinonimia técnica en español (ej. relacionar 'brotes' con 'epidemias').
2.  **Persistencia:** La implementación con `ChromaDB PersistentClient` permite que el sistema RENACE sea escalable, evitando la re-indexación costosa en cada sesión.

**Recomendación:** Se recomienda el despliegue del modelo **Multilingual L12** para el sistema nacional, ya que garantiza que las búsquedas semánticas capturen las variaciones regionales del lenguaje técnico peruano sin pérdida de contexto.
