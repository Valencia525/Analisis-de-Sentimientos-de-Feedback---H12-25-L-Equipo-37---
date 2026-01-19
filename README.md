# 📘 Proyecto: Sistema de Análisis de Sentimiento para Reseñas en Español  
**Repositorio:** `sentiment-api`

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

El modelo fue desarrollado a partir de un **dataset compuesto por aproximadamente 50,000 reseñas en español**, seleccionadas por su relevancia para el problema de análisis de sentimiento.

El dataframe contiene:
- Texto de reseñas.
- Etiquetas de sentimiento asociadas.

Durante la preparación de los datos se realizaron las siguientes tareas:
- Identificación de columnas relevantes.
- Limpieza de valores nulos o inconsistentes.
- Análisis de la distribución de clases.

Para el entrenamiento del modelo se definió una **clasificación binaria (positivo / negativo)**.  
La categoría **neutral** no fue entrenada de forma explícita, sino introducida posteriormente mediante reglas basadas en probabilidad durante la inferencia.

---

## 🧹 Preprocesamiento de texto

El preprocesamiento lingüístico fue diseñado para reducir ruido sin perder información semántica relevante.  
Las transformaciones aplicadas incluyen:

- Conversión sistemática del texto a minúsculas.
- Eliminación de acentos para unificar variantes ortográficas.
- Limpieza de caracteres no relevantes.
- Normalización de expresiones compuestas frecuentes con carga negativa  
  (por ejemplo: *“no funciona”*, *“no sirve”*).

Estas transformaciones fueron definidas a partir de pruebas iterativas, observando mejoras en la estabilidad del modelo y la coherencia de las predicciones.

---

## 🧠 Diseño del pipeline de Machine Learning

El sistema se implementó mediante un **pipeline de machine learning**, integrando en una sola estructura:

- Transformación del texto a una representación numérica.
- Clasificador entrenado.
- Métodos de inferencia y obtención de probabilidades.

Este enfoque garantiza que el mismo flujo de procesamiento se aplique tanto en entrenamiento como en inferencia, reduciendo inconsistencias y facilitando la portabilidad del modelo.

---

## 📈 Entrenamiento y evaluación del modelo

Aunque el dataset original consta de **50,000 reseñas**, la evaluación final se realizó sobre un **conjunto de prueba de 10,000 reseñas**, balanceado entre ambas clases (5,000 por clase).

Las métricas utilizadas para evaluar el desempeño del modelo fueron:
- Accuracy
- Precision
- Recall
- F1-score

### Resultados de clasificación

| Clase | Precisión | Recall | F1-score | Soporte |
|------:|----------:|-------:|---------:|--------:|
| 0 (Negativo) | 0.89 | 0.86 | 0.87 | 5,000 |
| 1 (Positivo) | 0.86 | 0.90 | 0.88 | 5,000 |
| **Accuracy global** | — | — | **0.88** | 10,000 |
| **Macro average** | 0.88 | 0.88 | 0.88 | 10,000 |
| **Weighted average** | 0.88 | 0.88 | 0.88 | 10,000 |

---

## 🧠 Interpretación de resultados

El **accuracy de 87.66%** indica un desempeño sólido y consistente.  
Las métricas balanceadas entre clases reflejan que el modelo no presenta sesgos significativos.  
El valor del **F1-score cercano a 0.88** confirma un equilibrio adecuado entre precisión y recall.

Estos resultados validan el uso del modelo como **núcleo de inferencia confiable**, sobre el cual se implementa una capa adicional de lógica basada en probabilidades para manejar casos de baja certeza mediante la categoría **neutral**.

---

## ⚖️ Uso de probabilidades y definición de la categoría neutral

La decisión final no se basa únicamente en la etiqueta predicha por el clasificador, sino en la **probabilidad asociada a la clase positiva (`predict_proba`)**, interpretada como una medida de confianza:

- Probabilidades altas → clasificación confiable.
- Probabilidades intermedias → clasificación como neutral.
- Probabilidades bajas → clasificación negativa.

Este enfoque introduce una **regla de decisión independiente del modelo**, mejorando la utilidad del sistema en escenarios reales.

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
