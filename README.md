# Analisis-de-Sentimientos-de-Feedback---H12-25-L-Equipo-37---
Modelo de análisis de sentimiento en español que combina machine learning y reglas basadas en probabilidad para clasificar reseñas como positivas, negativas o neutrales, priorizando interpretabilidad, documentación y escalabilidad entre Python y Java.

# Modelo de Análisis de Sentimiento para Reseñas en Español

## 📌 Descripción general
Este proyecto consiste en el diseño, entrenamiento y documentación de un modelo de análisis de sentimiento aplicado a reseñas en español. El sistema clasifica textos en tres categorías: **positivo**, **negativo** y **neutral**, incorporando un enfoque basado en **probabilidades** para evitar decisiones forzadas en casos de baja certeza.

El proyecto fue desarrollado con una visión práctica y escalable, permitiendo la migración conceptual desde un entorno de experimentación en **Python** hacia un entorno de inferencia en **Java**, manteniendo consistencia lógica y reproducibilidad.

---

## 🎯 Objetivo
Desarrollar un sistema de análisis de sentimiento que:
- Clasifique reseñas en español de forma confiable.
- Utilice probabilidades para definir una categoría neutral.
- Sea interpretable, documentado y defendible.
- Pueda adaptarse a entornos productivos más allá del prototipo.

---

## 📊 Dataset
El modelo fue entrenado utilizando un dataframe estructurado compuesto por:
- Textos de reseñas en español.
- Etiquetas de sentimiento asociadas.

Durante la preparación de datos se realizaron:
- Revisión de valores nulos e inconsistencias.
- Análisis de distribución de clases.
- Definición de una clasificación binaria (positivo / negativo) para el entrenamiento directo.

La clase **neutral** se introduce posteriormente mediante reglas basadas en probabilidad.

---

## 🧹 Preprocesamiento de texto
Se implementó un preprocesamiento lingüístico cuidadoso para reducir ruido sin perder información semántica:

- Conversión del texto a minúsculas.
- Eliminación de acentos.
- Limpieza de caracteres no relevantes.
- Normalización de frases compuestas frecuentes con carga semántica negativa (ej. *“no funciona”*, *“no sirve”*).

Estas decisiones fueron validadas mediante pruebas iterativas.

---

## 🧠 Pipeline de Machine Learning
El modelo se implementó mediante un **pipeline**, integrando:
- Vectorización del texto.
- Clasificador entrenado.
- Métodos de inferencia y obtención de probabilidades.

Este enfoque garantiza que el mismo flujo se utilice tanto en entrenamiento como en inferencia, reduciendo errores e inconsistencias.

---

## 📈 Entrenamiento y Evaluación
El desempeño del modelo fue evaluado utilizando métricas estándar de clasificación:

- Accuracy
- Precision
- Recall
- F1-score

El análisis incluyó la interpretación de falsos positivos y falsos negativos, considerando su impacto en escenarios reales.

---

## ⚖️ Uso de probabilidades y clase neutral
En lugar de basarse únicamente en la etiqueta predicha, el sistema utiliza la probabilidad de la clase positiva (`predict_proba`) para definir rangos de decisión:

- Probabilidades altas → clasificación confiable.
- Probabilidades intermedias → **neutral**.
- Probabilidades bajas → **negativo**.

Esta capa de lógica actúa como una regla de negocio independiente del modelo.

---

## 🔧 Función final de predicción
Se desarrolló una función que encapsula todo el flujo:
- Entrada de texto crudo.
- Aplicación automática del pipeline.
- Obtención de probabilidades.
- Asignación de la etiqueta final según los umbrales definidos.

Esta función está pensada como interfaz principal para producción o integración.

---

## ☕ Adaptación conceptual a Java
La lógica del sistema fue reconstruida conceptualmente en Java, separando responsabilidades en:
- Preprocesamiento.
- Inferencia.
- Decisión final basada en probabilidades.

Esto asegura consistencia entre lenguajes y facilita su uso en entornos productivos.

---

## 📄 Licencia
Este proyecto se distribuye bajo la licencia **MIT**.
