# 📘 Proyecto: Sistema de Análisis de Sentimiento para Reseñas en Español  
**Repositorio:** [sentiment-api](https://github.com/Valencia525/Analisis-de-Sentimientos-de-Feedback---H12-25-L-Equipo-37---)

---

## 👨‍💼 Equipo de trabajo

### Líder del proyecto
**Nombre:** Joel Valencia San Román  
**Contacto:** joelvalenciasanroman@gmail.com  
**Rol:** Data Scientist Lead  

### Equipo de Data Science

**Nombre:** Ana Mosquera Lozano  
**Contacto:** armosque99@gmail.com  
**Rol:** Data Scientist  

**Nombre:** Jetsael Villegas  
**Contacto:** jet7vm@hotmail.com  
**Rol:** Data Scientist  

**Nombre:** Enrique Hernández  
**Contacto:** enriketf@gmail.com  
**Rol:** Data Scientist  

**Nombre:** Paola Andrea Rubiano Ruiz  
**Contacto:** —  
**Rol:** Data Scientist  

---

## 📌 Descripción general

El presente proyecto tiene como objetivo el diseño, entrenamiento y documentación de un **sistema de análisis de sentimiento aplicado a reseñas en español**, capaz de clasificar textos en las categorías **positivo**, **negativo** y **neutral**.

El sistema combina **machine learning supervisado** con un **criterio de decisión basado en probabilidades**, lo que permite manejar la incertidumbre inherente al modelo y evitar decisiones forzadas en casos ambiguos.

Desde su concepción, el proyecto fue diseñado con una visión práctica y escalable, permitiendo la **migración del flujo completo desde un entorno de experimentación en Python hacia un entorno de inferencia en Java**, manteniendo consistencia lógica, interpretabilidad y reproducibilidad.

---

## 🎯 Objetivo del proyecto

Desarrollar un sistema de análisis de sentimiento que:
- Clasifique reseñas en español de manera confiable.
- Incorpore una categoría neutral basada en rangos de probabilidad.
- Sea interpretable, documentado y técnicamente defendible.
- Pueda integrarse en entornos productivos.

---

## 📊 Dataset y preparación de datos

El sistema de prueba se desarrolló a partir de un **dataset compuesto por aproximadamente 50,000 reseñas en español**.
El sistema final se desarrolló a partir de un **dataset compuesto por aproximadamente 200,000 reseñas en español de amazon,  de un entorno real, reducido a 80,000 reseñas para las metricas mostradas**.

El dataframe contiene:
- Texto de reseñas.
- Etiquetas de sentimiento asociadas.

Durante la preparación de los datos se realizaron las siguientes tareas:
- Identificación de columnas relevantes.
- Limpieza de valores nulos o inconsistentes.
- Análisis de la distribución de clases.

Para el entrenamiento del modelo se definió una **clasificación binaria (positivo / negativo)**.  
La categoría **neutral** no fue entrenada explícitamente, sino introducida posteriormente mediante reglas basadas en probabilidad durante la inferencia.

---

## 🧹 Preprocesamiento de texto

El preprocesamiento lingüístico fue diseñado para reducir ruido sin perder información semántica relevante:

- Conversión del texto a minúsculas.
- Eliminación de acentos.
- Limpieza de caracteres no informativos.
- Normalización de expresiones negativas compuestas (*“no funciona”*, *“no sirve”*).

Estas transformaciones se definieron tras pruebas iterativas y análisis de impacto en las métricas del modelo.

---

## 🧠 Diseño del pipeline de Machine Learning

El sistema se implementó mediante un **pipeline de machine learning**, integrando:

- Vectorización del texto.
- Clasificador supervisado.
- Inferencia probabilística (`predict_proba`).

Este enfoque garantiza coherencia entre entrenamiento e inferencia y facilita la portabilidad del modelo.

---

## 🔬 Fases del desarrollo del modelo

### Fase 1: Modelo de prueba (baseline)

Se entrenó un **modelo inicial de referencia**, cuyo objetivo fue:
- Validar el preprocesamiento.
- Evaluar la separabilidad del problema.
- Establecer métricas base.

La evaluación se realizó sobre un **conjunto de prueba de 10,000 reseñas**, balanceado (5,000 por clase).

#### Resultados del modelo de prueba

| Clase | Precisión | Recall | F1-score | Soporte |
|------:|----------:|-------:|---------:|--------:|
| 0 (Negativo) | 0.89 | 0.86 | 0.87 | 5,000 |
| 1 (Positivo) | 0.86 | 0.90 | 0.88 | 5,000 |
| **Accuracy global** | — | — | **0.88** | 10,000 |
| **Macro average** | 0.88 | 0.88 | 0.88 | 10,000 |
| **Weighted average** | 0.88 | 0.88 | 0.88 | 10,000 |

Este modelo se utilizó **exclusivamente como referencia inicial** y **no corresponde al modelo final entregado**.

---

### Fase 2: Modelo final optimizado con Optuna

El **modelo final** incorpora **Optimización Bayesiana mediante Optuna**, con el objetivo de encontrar automáticamente la mejor combinación de hiperparámetros.

#### Optimización Bayesiana (Optuna)

La optimización incluyó:
- Definición del espacio de búsqueda de hiperparámetros.
- Evaluación iterativa mediante funciones objetivo.
- Selección del modelo con mayor desempeño global.
- Prevención de overfitting mediante validación.

Este enfoque permitió mejorar la estabilidad, generalización y desempeño del sistema.

---

## 📈 Evaluación del modelo final

El modelo final fue evaluado sobre un **conjunto de prueba independiente de 12,000 reseñas**, balanceado (6,000 por clase).

### Resultados del modelo final (Optuna)

| Clase | Precisión | Recall | F1-score | Soporte |
|------:|----------:|-------:|---------:|--------:|
| Negativo | 0.94 | 0.93 | 0.93 | 6,000 |
| Positivo | 0.93 | 0.94 | 0.93 | 6,000 |
| **Accuracy global** | — | — | **0.93475** | 12,000 |
| **Macro average** | 0.93 | 0.93 | 0.93 | 12,000 |
| **Weighted average** | 0.93 | 0.93 | 0.93 | 12,000 |

Estos resultados corresponden **exclusivamente al modelo final**, optimizado mediante **Optimización Bayesiana con Optuna**.

---

## 🧠 Interpretación de resultados

El **accuracy de 93.47%** evidencia una mejora significativa respecto al modelo de prueba.  
Las métricas equilibradas entre clases indican **ausencia de sesgos relevantes**.  
El **F1-score estable (0.93)** confirma un balance sólido entre precisión y recall.

El modelo final es **robusto, generalizable y apto para despliegue productivo**.

---

## ⚖️ Uso de probabilidades y definición de la categoría neutral

La decisión final se basa en la **probabilidad asociada a la clase positiva**, no únicamente en la etiqueta:

- Alta probabilidad → clasificación confiable.
- Probabilidad intermedia → clasificación neutral.
- Baja probabilidad → clasificación negativa.

Esta capa de decisión probabilística es **independiente del clasificador** y mejora el desempeño del sistema en escenarios reales.

---

## 📊 Visualización de resultados

El análisis se complementa con visualizaciones generadas mediante **PyPlot**, que permiten:
- Analizar el comportamiento del modelo.
- Comparar desempeño entre fases.
- Validar estabilidad de predicciones.

Las gráficas asociadas corresponden al **modelo final optimizado**.


---





# 📘 README — Proyecto `sentiment-api`

Este documento explica cómo abrir y ejecutar el proyecto **sentiment-api** en tu entorno local.

---

## 🚀 Cómo abrir el proyecto en Eclipse

1. **Descargar** el archivo `sentiment-api.zip` desde Google Drive.  
2. **Descomprimir** el archivo en una carpeta local.  
3. **Abrir Eclipse**.  
4. En el menú principal, ir a:  
   **File → Import**  
5. Seleccionar:  
   **Existing Maven Projects**  
6. Hacer clic en **Next**.  
7. Seleccionar la carpeta raíz del proyecto:  
   ```
   sentiment-api
   ```
8. Hacer clic en **Finish**.  
9. Esperar a que **Maven descargue automáticamente las dependencias**.  
10. Ejecutar la clase:
    ```
    TestPredictor
    ```

📌 **Importante:**  
No crear el proyecto manualmente. El proyecto debe abrirse **únicamente** mediante la opción *Existing Maven Projects*.

---

## 🧠 Archivo del modelo ONNX (muy importante)

- ❗ **NO mover** el archivo `pipeline.onnx` de la carpeta:
  ```
  models/
  ```
- ❗ Si por alguna razón se cambia su ubicación, es obligatorio actualizar la ruta en el código:

```java
new SentimentPredictor("models/pipeline.onnx");
```

---

## 💻 ¿Y si no usas Eclipse?

No hay problema. El proyecto es un **proyecto Maven estándar**, por lo que puede abrirse y ejecutarse desde otros entornos:

- **IntelliJ IDEA**
- **Visual Studio Code**
- **Línea de comandos**, ejecutando:
  ```bash
  mvn clean install
  ```

Esta portabilidad es una de las ventajas de haber estructurado el proyecto con Maven.

---

## ✅ Notas finales

- El modelo ONNX ya está integrado en el proyecto.
- `TestPredictor` sirve como punto de prueba para validar la inferencia.
- La clase que se usa para meter texto y obtener una respuesta es SentimentPredictor.
- No es necesario configurar nada adicional más allá de importar el proyecto correctamente.
