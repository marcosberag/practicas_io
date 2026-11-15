# Prácticas de Investigación Operativa

**Grado en Ciencia de Datos e Inteligencia Artificial · UPM · Curso 2026-2027**

## Práctica 1 · Versión para feedback

La práctica se presenta en **dos notebooks**, uno por cada parte del enunciado. Ambos incluyen el planteamiento, la explicación de la solución, el código comentado en castellano, las comprobaciones y las salidas guardadas. Se pueden revisar directamente en GitHub sin ejecutar el entrenamiento.

| Archivo | Contenido |
| --- | --- |
| [Parte 1](Pr%C3%A1ctica%201/parte1.ipynb) | Símplex combinado, datos separables en dos dimensiones y formulación y resolución dual del L1-SVM |
| [Parte 2](Pr%C3%A1ctica%201/parte2.ipynb) | MNIST con red neuronal y SVM gaussiana, FGSM, predicción y visualización de imágenes adversarias; opcionales 5–7 |
| [Enunciado](Pr%C3%A1ctica%201/enunciado_practica_1.md) | Requisitos de la práctica y de la exposición |

### Resultados comprobados

Ejecución del 15 de noviembre de 2026, desde entornos limpios:

- **Parte 1:** 28/28 pruebas del Símplex superadas; objetivo del L1-SVM coincidente entre primal, dual y HiGHS: **0,610824756**, con comprobación de factibilidad y complementariedad.
- **Parte 2:** **98,82 %** de acierto de la red neuronal en test, **41.074 parámetros** y **98,33 %** de acierto de la SVM. Se verifican las propiedades numéricas del ataque FGSM y se muestran originales y adversarias con las predicciones de ambos modelos.
- **Opcionales 5–7:** implementados, pero sin ejecutar en la versión guardada. Sus celdas indican expresamente ese estado.

### Cuestiones para feedback

Los cuadernos señalan sus limitaciones junto a las explicaciones correspondientes. El dual del L1-SVM introduce degeneración estructural, aunque la instancia incluida se resuelve y contrasta correctamente. En el entrenamiento adversario opcional queda pendiente decidir cómo separar la validación para evitar que una imagen original y su adversaria se repartan entre ambos conjuntos, y cómo ajustar el entrenamiento al requisito de 120.000 imágenes. También falta confirmar que la arquitectura de la red difiere de la de clase y de la de otros grupos.

Los puntos 1–4 de la Parte 2 son los obligatorios y permiten obtener la máxima nota de esa parte según el enunciado; no es necesario ejecutar los opcionales para solicitar feedback sobre el trabajo obligatorio. La exposición de la Parte 1 se prepara por separado.

### Ejecución

El entorno verificado utiliza **Python 3.13.0, Windows y CPU**. Las versiones de las dependencias se recogen en [requirements.txt](requirements.txt).

```bash
python -m pip install -r requirements.txt
```

Abrir el notebook deseado en Jupyter o VS Code, seleccionar el entorno de Python y ejecutar las celdas en orden desde un kernel limpio. Cada notebook es independiente del otro.

La Parte 2 carga MNIST mediante Keras y lo descarga si no está en caché. Guarda `red_mnist.keras` en el directorio de ejecución. La ejecución comprobada de los apartados obligatorios tarda aproximadamente siete minutos en el equipo utilizado; el tiempo depende del dispositivo. Los opcionales se activan con `EJECUTAR_OPCIONALES = True` y pueden requerir bastante más tiempo y memoria, especialmente la SVM con 120.000 imágenes.

Los borradores, cuadernos duplicados, resultados anteriores e informe detallado de revisión se conservan en el [historial de la versión consolidada](https://github.com/marcosberag/practicas_io/tree/296832983ad313b75ccdd196537fea11b3a6e0d5). Se han retirado de la versión actual para mantener una única ruta de lectura y ejecución.

## Práctica 2 de la asignatura

Se conservan su [enunciado](Pr%C3%A1ctica%202/enunciado_practica_2.md) y la imagen de los circuitos en la carpeta `Práctica 2`. Esta carpeta corresponde a la otra práctica de la asignatura; es distinta de la Parte 2 de la Práctica 1.
