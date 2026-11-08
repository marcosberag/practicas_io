# Prácticas de Investigación Operativa

**Grado en Ciencia de Datos e Inteligencia Artificial · UPM · Curso 2026-2027**

Repositorio de trabajo para las prácticas de Investigación Operativa. Los enunciados proceden de los apuntes de la asignatura de Carlos Quesada González.

## Contenido

```text
Práctica 1/
├── enunciado_practica_1.md
└── Parte 1/
    └── parte1.ipynb          # Símplex combinado (en desarrollo)
Práctica 2/
├── enunciado_practica_2.md
└── circuitos.png            # Imagen del enunciado
```

## Ejecución

Se necesita **Python 3**, **NumPy** y un entorno compatible con notebooks de Jupyter, como JupyterLab o VS Code con la extensión Jupyter.

1. Abrir `Práctica 1/Parte 1/parte1.ipynb`.
2. Seleccionar un entorno de Python con NumPy instalado.
3. Ejecutar las celdas en orden, desde el principio.

## Símplex combinado

La función principal, `simplex_completo(opt, c, A, rest, b)`, recibe un problema de programación lineal con variables originales no negativas:

- `opt`: `"max"` o `"min"`.
- `c`: coeficientes del objetivo, vector de longitud `n`.
- `A`: matriz de restricciones, de dimensiones `m × n`.
- `rest`: lista de `m` signos, `"<="` o `">="`.
- `b`: términos independientes, vector de longitud `m`.

Devuelve `(x, z, estado, M_f)`: variables originales, valor objetivo, estado de terminación y última tabla calculada. Cuando no se acredita una solución óptima, `x` y `z` son `None`.

El método comienza con Símplex estándar si la base inicial es primal factible. En caso contrario, comprueba si puede comenzar con Símplex dual y, tras recuperar la factibilidad primal, pasa al estándar conservando la base.

**Alcance:** se implementa el procedimiento combinado estudiado en clase. No se tratan restricciones de igualdad ni casos degenerados. Si la tabla inicial no es primal ni dual factible, el programa puede devolver `"no_resuelto"`; esto no significa que el problema sea infactible. Tampoco se implementa un método general de Fase I.

## Estado del trabajo

La implementación del Símplex y su documentación están en revisión. La aplicación al L1-SVM de la Práctica 1 se integrará en el mismo flujo de resolución.
