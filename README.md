# Prácticas de Investigación Operativa

**Grado en Ciencia de Datos e Inteligencia Artificial · UPM · Curso 2026-2027**

Repositorio de trabajo para las prácticas de Investigación Operativa. Los enunciados proceden de los apuntes de la asignatura de Carlos Quesada González.

## Contenido

```text
Práctica 1/
├── enunciado_practica_1.md
├── Parte 1/
│   └── parte1.ipynb          # Símplex combinado y L1-SVM
├── Parte2/
│   ├── parte2.ipynb          # MNIST, FGSM y apartados opcionales 5–7
│   └── antecedentes/        # Fuentes originales y sus resultados históricos
└── REVISION.md              # Cambios, comprobaciones y pendientes
Práctica 2/
├── enunciado_practica_2.md
└── circuitos.png            # Imagen del enunciado
```

## Ejecución

Se necesita **Python 3** y un entorno compatible con notebooks de Jupyter, como JupyterLab o VS Code con la extensión Jupyter. Las dependencias están en `requirements.txt`; las versiones utilizadas en la revisión se registran en `requirements-verificacion.txt`.

1. Abrir `Práctica 1/Parte 1/parte1.ipynb`.
2. Seleccionar un entorno de Python con NumPy, SciPy y Matplotlib instalados.
3. Ejecutar las celdas en orden, desde el principio.

Para la Parte 2, abrir `Práctica 1/Parte2/parte2.ipynb` y ejecutar desde un entorno limpio con TensorFlow y scikit-learn. MNIST se descarga si no está en la caché de Keras. El cuaderno entrena la red y la SVM con los tamaños originales, y guarda `red_mnist.keras` en el directorio de ejecución. Los apartados opcionales 5–7 se activan con `EJECUTAR_OPCIONALES = True`; pueden exigir bastante tiempo y memoria, especialmente la SVM de 120.000 imágenes. Con el valor `False` sus salidas indican expresamente que no se han ejecutado.

Los notebooks de `antecedentes/` se conservan íntegros como trazabilidad del trabajo previo. Algunos contienen errores, resultados sin código o dependencias de otras sesiones: no son la ruta recomendada de ejecución. Para remitir al profesor, utilizar los dos notebooks principales, el enunciado y el informe de revisión.

## Símplex combinado

La función principal, `simplex_completo(opt, c, A, rest, b)`, recibe un problema de programación lineal con variables originales no negativas:

- `opt`: `"max"` o `"min"`.
- `c`: coeficientes del objetivo, vector de longitud `n`.
- `A`: matriz de restricciones, de dimensiones `m × n`.
- `rest`: lista de `m` signos, `"<="` o `">="`.
- `b`: términos independientes, vector de longitud `m`.

Devuelve `(x, z, estado, M_f)`: variables originales, valor objetivo, estado de terminación y última tabla calculada. Cuando no se acredita una solución óptima, `x` y `z` son `None`.

El método comienza con Símplex estándar si la base inicial es primal factible. En caso contrario, comprueba si puede comenzar con Símplex dual y, tras recuperar la factibilidad primal, pasa al estándar conservando la base.

**Alcance:** se implementa el procedimiento combinado estudiado en clase. No se admiten restricciones de igualdad directamente ni se garantiza tratamiento general de degeneración. El dual del L1-SVM representa una igualdad mediante dos desigualdades y tiene una base inicial degenerada: la instancia incluida se verifica, pero no hay garantía general de ausencia de ciclos. Si la tabla inicial no es primal ni dual factible, el programa puede devolver `"no_resuelto"`; esto no significa que el problema sea infactible. No se implementa el método de dos fases.

## Estado del trabajo

Versión consolidada para recibir feedback. La Parte 1 incluye el L1-SVM y comprobaciones independientes. La Parte 2 reúne los apartados obligatorios y opcionales en un único flujo. Consultar `Práctica 1/REVISION.md` para distinguir resultados comprobados, históricos y pendientes.
