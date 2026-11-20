# TP4 — Clasificación de lesiones cutáneas con CNN

Trabajo práctico de aprendizaje profundo enfocado en la clasificación de **9 clases de lesiones dermatológicas** usando redes neuronales convolucionales (CNN) en PyTorch, comparando su rendimiento, eficiencia paramétrica y robustez frente a perceptrones multicapa (MLP).

## Estructura del repositorio

* `04_CNN_Skin_ISIC.ipynb`: Notebook completo y ejecutado con el análisis exploratorio (EDA), limpieza de duplicados, comparación MLP vs. CNN, ablación de arquitectura, experimentos de *data augmentation*, evaluación final en test e interpretabilidad (filtros y mapas de activación).
* `requirements.txt`: Librerías necesarias para ejecutar el entorno.
* `README.md`: Descripción general e instrucciones de ejecución.

## Resumen del flujo y resultados

1. **Limpieza y partición:** A partir de las 878 imágenes originales se detectaron y eliminaron 34 duplicados exactos (33 filtrados entre `train` y `val`), quedando **844 imágenes únicas** divididas de forma estratificada en `60% train` (506), `20% val` (169) y `20% test` (169).
2. **MLP vs. CNN:** Las CNN superan por más de 11–13 puntos porcentuales a las MLP en validación utilizando más de 10 veces menos parámetros y mostrando mayor estabilidad ante traslaciones.
3. **Arquitectura y *Data Augmentation*:** El análisis de un factor a la vez mostró que aumentar la profundidad a **4 bloques** (campo receptivo de 38 px) y aplicar rotaciones/reflexiones (**`flips + rot90`**) mejora la generalización sin distorsionar la información clínica de color.
4. **Evaluación en test (5 semillas):**

| Modelo | Parámetros | Test Accuracy | Test F1-macro |
| :--- | :---: | :---: | :---: |
| **CNN final (4 bloques + `flips+rot90`)** | 361.113 | **0,6722 ± 0,0312** | **0,6616 ± 0,0432** |
| **MLP (64 px)** | 6.358.793 | 0,5041 ± 0,0534 | 0,4872 ± 0,0572 |

## Cómo ejecutar el proyecto

1. Clonar el repositorio e instalar las dependencias:
   ```bash
   pip install -r requirements.txt
