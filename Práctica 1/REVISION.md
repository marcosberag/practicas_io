# Revisión de la versión consolidada

**Fecha:** 15 de noviembre de 2026. **Finalidad:** solicitar feedback del profesor antes de la entrega definitiva.

## Fuentes revisadas

Se ha partido de `main` en `c80c86d861df111fb0f295e57c4cb6ce7596df8f` (14 de noviembre). El historial contiene la implementación y las pruebas del Símplex en `98c77a3`, la incorporación del L1-SVM mediante «Add files via upload» en `676317e` y los cinco cuadernos de la Parte 2 en `c80c86d`. Solo existe la rama remota `main` en el momento de la revisión.

El adjunto `parte2.ipynb` del chat anterior corresponde a los opcionales 5–7. Se ha recuperado el archivo adjunto original, puesto que `/mnt/data/parte2.ipynb` no existe en este entorno de Windows. Su SHA-256 es `7876a3b5c5e7d6196450f61378fe5fbd1d9c959c20de5d99995cad7de075e47a`.

## Cambios realizados

- Se mantienen los dos bloques principales: `Parte 1/parte1.ipynb` y `Parte2/parte2.ipynb`. Los apartados 1–7 de MNIST forman ahora un único flujo, con datos y modelos compartidos. Los opcionales se activan de forma explícita para evitar iniciar por accidente el entrenamiento de la SVM con 120.000 imágenes.
- Se conserva el contenido de los cinco notebooks de la Parte 2 en `Parte2/antecedentes/`, con sus salidas históricas. Se añade allí el adjunto original completo. Los errores de kernel, variables sin definir y salidas sin código de esos antecedentes no se eliminan ni se presentan como resultados nuevos.
- Se unifican portada, objetivos, explicación de entradas y salidas, comentarios en castellano, tablas y notación. Se corrigen afirmaciones que confundían resultados de los apuntes con los de esta arquitectura, y se elimina la afirmación no verificada de originalidad de la red.
- Se corrige la explicación de FGSM: maximiza la aproximación lineal de la pérdida y no garantiza una clasificación errónea. Se distingue ataque de caja blanca a la red de transferencia a la SVM, y se evita inferir robustez general a partir de seis imágenes.
- Se conserva la arquitectura convolucional de 41.074 parámetros, SGD con tasa 0,1, 15 épocas, la SVM RBF con `C=10`, `gamma=0.01` y `EPSILON=0.2`. Se añaden comprobaciones explícitas del 95 % exigido y del número de parámetros.
- Se mantiene el procedimiento de FGSM. Se valida que `epsilon` sea finito y no negativo y se añade procesado por lotes de 256 al ataque del test completo. Se prueban rango, finitud, cota, perturbación nula y equivalencia por lotes. Se extiende la evaluación doblemente adversaria a la SVM robusta, que faltaba en el adjunto.
- En el L1-SVM se retiran impresiones de depuración, se comprueba el estado antes de interpretar el óptimo y se usa tolerancia para identificar multiplicadores positivos. Se distingue margen blando de la solución sin violaciones observada en la muestra.
- Se añade validación primal-dual, complementariedad y contraste con HiGHS. El generador de datos rechaza separaciones no finitas o inviables: antes podía entrar en un bucle sin salida. El límite se deduce del cuadrado `[-4,4]^2` y la recta usada, conservando exactamente los datos con la semilla y separación originales.
- No se modifican las funciones `actualizar_matriz`, `preprocesar`, `simplex_estandar`, `simplex_dual` ni `simplex_completo`: su estructura sintáctica se ha comparado con el original. No se cambia la regla de pivote ni se añade el método de dos fases.
- Se actualizan el README, las dependencias y la selección de kernel portátil `python3`. Los modelos generados quedan excluidos del control de versiones.

## Comprobaciones nuevas

La revisión ejecuta los notebooks principales desde kernels limpios. Las versiones se registran en `requirements-verificacion.txt`; el equipo usa Windows y CPU con Python 3.13.0. Las salidas originales se guardan aparte y las nuevas salidas corresponden al código consolidado.

### Parte 1

- **28/28** pruebas del Símplex superadas, incluidas condiciones de terminación, último pivote, tolerancias, entradas y bases inválidas y conservación de datos.
- La muestra contiene **40 puntos**, 20 por clase, y se reproduce exactamente con la semilla 0.
- **Primal = dual = HiGHS: 0,610824756**. Brecha primal-dual calculada: **0** en la precisión de la ejecución.
- Se verifican no negatividad, restricciones de ambos problemas y los dos productos de complementariedad con tolerancia `1e-7`.
- El primal se resuelve también con el Símplex combinado y coincide en objetivo. Se comprueban margen y ausencia de violaciones para esta muestra.
- Se comprueba el rechazo de separaciones 0, negativas, NaN, infinito y 5.

### Parte 2

- Se completa la ejecución de todos los apartados obligatorios desde un kernel limpio, sin errores, en aproximadamente **446 segundos** (incluye 15 épocas de la red y el entrenamiento de la SVM).
- **Red neuronal: 98,82 %** en las 10.000 imágenes de test (`0.9882000088691711`). Se supera el mínimo del 95 % y se verifican **41.074 parámetros**.
- **SVM gaussiana: 98,33 %** en test, con **10.867 vectores de soporte**.
- **FGSM:** se verifican forma, finitud, rango `[0,1]`, cota `EPSILON + 1e-6`, identidad con perturbación cero, rechazo de parámetros inválidos y equivalencia directa/por lotes con tolerancia `1e-6`.
- En las seis muestras ilustradas, los dos modelos aciertan las seis originales. Tras el ataque, la red acierta **3/6** y la SVM **4/6**. Son resultados descriptivos de esa muestra, no del test adversario completo. El cambio máximo observado por píxel es `0.20000002`, compatible con la tolerancia de float32.
- Se inspeccionan las dos figuras generadas: frontera y márgenes del L1-SVM e imágenes originales/adversarias con ambas predicciones. Las salidas se conservan en los cuadernos principales.
- Se compacta la salida de entrenamiento conservando las métricas finales de las **15 épocas**, la evaluación y el acierto final; se retiran las actualizaciones intermedias de la barra de progreso y los caracteres de control. Para futuras ejecuciones se establece `verbose=2`, sin cambiar el entrenamiento. TensorFlow emite avisos del entorno que no impiden completar las comprobaciones.
- Los opcionales **5–7 no se ejecutan** en esta comprobación; sus salidas lo indican expresamente. No se consideran acreditadas métricas de test adversario completo, entrenamiento adversario ni ataque doble.

## Problemas sustantivos y pendientes para el feedback

1. **Degeneración del dual L1-SVM.** La igualdad de balance se expresa mediante dos desigualdades con término independiente cero. La base inicial es degenerada, aunque el enunciado permite omitir casos degenerados. La instancia incluida funciona, pero el método no garantiza ausencia de ciclos en general. Conviene consultar al profesor si acepta esta representación o prefiere otra formulación. No se ha sustituido la regla de pivote.
2. **Alcance del Símplex.** No se implementa el método de dos fases. `no_resuelto` no demuestra infactibilidad. Los métodos de bajo nivel requieren la factibilidad de entrada documentada; no son interfaces generales para tablas arbitrarias. Se mantiene el uso de inversas y tolerancia absoluta, con sus límites de estabilidad y escalado.
3. **Validación del entrenamiento adversario opcional.** El barajado individual puede separar la imagen original y su adversaria entre entrenamiento y validación. `validation_split=0.1` implica 108.000 imágenes para ajustar la red y 12.000 para validar, mientras la SVM utiliza las 120.000. Se conserva y documenta el protocolo recibido. Antes de una entrega definitiva hay que decidir entre separar por imagen de origen o entrenar con las 120.000 sin validación interna; no se presenta esta validación como independiente.
4. **Interpretación de robustez.** El entrenamiento adversario es estático: las adversarias se generan contra la red original, no se recalculan en cada actualización. La evaluación mixta usa ese ataque fijo. El segundo ataque se calcula contra la nueva red y tiene cota acumulada de hasta `2*EPSILON` respecto al original, sin proyección a la bola original. Una buena precisión de la SVM ante transferencia no garantiza resistencia frente a un ataque específico.
5. **Resultados opcionales y recursos.** Los apartados 5–7 están integrados pero no ejecutados en la comprobación por defecto. No hay métricas nuevas de entrenamiento adversario ni de ataque doble. Ejecutarlos con los tamaños completos y conservar sus resultados antes de afirmar conclusiones sobre esos experimentos.
6. **Originalidad de arquitectura.** Confirmar con el profesor la diferencia respecto a la red de clase y la no coincidencia con otros grupos. Esa información no se puede acreditar con este repositorio.
7. **Reproducibilidad.** Las semillas y las operaciones deterministas no sustituyen el registro del entorno. No se ha repetido todo el entrenamiento dos veces para acreditar igualdad bit a bit. Los resultados de los antecedentes no se atribuyen a esta ejecución.

## Material para remitir

Los dos notebooks principales, el enunciado y este informe forman la versión para feedback. Los antecedentes y el historial permanecen disponibles en el repositorio para conservar todo el trabajo y sus resultados. La presentación de un máximo de siete diapositivas de contenido y siete minutos, exigida por el enunciado, no forma parte de esta consolidación.

## Referencias de comprobación

- [TensorFlow: ejemplo de FGSM](https://www.tensorflow.org/tutorials/generative/adversarial_fgsm), para contrastar el cálculo del gradiente respecto a la entrada y la perturbación por su signo.
- [Keras: API de entrenamiento](https://keras.io/api/models/model_training_apis/), para verificar que `validation_split` separa las últimas muestras antes del barajado de cada época.
- [scikit-learn: SVC](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html), para el esquema multiclase uno contra uno y las limitaciones de coste del entrenamiento.
