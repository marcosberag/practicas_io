# Prácticas de Investigación Operativa

**Grado en Ciencia de Datos e Inteligencia Artificial · UPM · Curso 2026-2027**

## Práctica 1 · Versión para feedback

La práctica se presenta en **dos notebooks**, uno por cada parte del enunciado, con una estructura de explicación y títulos común. Esta versión conserva **íntegramente las celdas de código y las salidas originales**. El trabajo de integración se limita a reunir los apartados, ordenar los archivos y homogeneizar la presentación. Las observaciones sobre posibles problemas aparecen separadas al final de cada cuaderno, sin aplicar correcciones al código.

| Archivo | Contenido |
| --- | --- |
| [Parte 1](Pr%C3%A1ctica%201/parte1.ipynb) | Símplex combinado y aplicación al L1-SVM |
| [Parte 2](Pr%C3%A1ctica%201/parte2.ipynb) | MNIST, red neuronal, SVM gaussiana, FGSM y opcionales 5–7 |
| [Enunciado](Pr%C3%A1ctica%201/enunciado_practica_1.md) | Requisitos de la práctica y de la exposición |

### Resultados y alcance

Los notebooks se pueden leer directamente en GitHub. Las salidas guardadas son las de las versiones recibidas, **no una nueva ejecución de esta versión editorial**. Se conserva la batería original de pruebas del Símplex. Los experimentos opcionales 5–7 están implementados, pero no tienen resultados completos acreditados en las salidas recibidas.

Las validaciones y ampliaciones funcionales de la revisión anterior se han retirado de esta versión. Siguen accesibles en el [historial de la revisión anterior](https://github.com/marcosberag/practicas_io/tree/296832983ad313b75ccdd196537fea11b3a6e0d5), junto con los borradores originales y el informe detallado. Las celdas de código actuales se han comparado con sus fuentes y coinciden íntegramente, incluidos comentarios y salidas.

### Cuestiones para feedback

Se mantienen las observaciones sobre degeneración del dual del L1-SVM, originalidad de la arquitectura, interpretación de los ataques y validación del entrenamiento adversario opcional. Este último utiliza `validation_split=0.1`: la red ajusta sus pesos con 108.000 imágenes, mientras el apartado pide entrenar con 120.000. Estos puntos se señalan en los notebooks para su discusión; no se han corregido sus implementaciones.

Los apartados 1–4 de la Parte 2 son los obligatorios y permiten obtener la máxima nota de esa parte según el enunciado. La exposición de la Parte 1 se prepara por separado.

### Ejecución

Cada notebook es independiente del otro. Abrirlo en Jupyter o VS Code, seleccionar el entorno de Python y ejecutar las celdas en orden desde un kernel limpio. [requirements.txt](requirements.txt) recoge las versiones disponibles en el entorno de revisión; no acredita el entorno de las salidas históricas ni una nueva ejecución completa de los originales.

```bash
python -m pip install -r requirements.txt
```

La Parte 2 carga MNIST mediante Keras y lo descarga si no está en caché. Guarda `red_mnist.keras` en el directorio de ejecución. Para ejecutar únicamente los apartados obligatorios, detenerse al finalizar el apartado 4. **Ejecutar todas las celdas también inicia los opcionales 5–7**: se mantiene su código original sin interruptores añadidos. Estos experimentos pueden requerir bastante tiempo y memoria, especialmente la SVM con 120.000 imágenes.

## Práctica 2 de la asignatura

Se conservan su [enunciado](Pr%C3%A1ctica%202/enunciado_practica_2.md) y la imagen de los circuitos en la carpeta `Práctica 2`. Corresponde a la otra práctica de la asignatura, distinta de la Parte 2 de la Práctica 1.
