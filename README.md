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
