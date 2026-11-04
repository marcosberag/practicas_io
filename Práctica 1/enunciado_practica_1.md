# Práctica 1. Investigación Operativa

**Asignatura:** Investigación Operativa  
**Curso:** 2026-2027  
**Fuente:** Apuntes de *Investigación Operativa*, Carlos Quesada González, Tema 5: Prácticas, páginas 97-99 (páginas 100-102 del PDF).

## Indicaciones generales

Todas las prácticas se realizan en grupos de hasta 4 personas, conforme a la herramienta de elección de grupos de Moodle.

Esta práctica consta de dos partes. **Se recomienda encarecidamente entregar la práctica al menos una semana antes de la fecha límite.** De esa forma habrá posibilidad de que recibáis feedback para corregir lo que fuera necesario. En caso de entregarlo en la fecha límite, esa versión se considerará definitiva.

Se recuerda que el uso de herramientas de IA está permitido, pero **todo el código debe estar comentado en castellano, explicando qué hace**. Además, todos los grupos deberán defender esta práctica el día **[pendiente de acordar con vosotros]**. La nota de esta práctica saldrá de la evaluación conjunta de lo entregado y lo expuesto y podrá ser diferente para integrantes de un mismo grupo, si su desempeño en la exposición también lo es.

### Detalles sobre la exposición

- La presentación debe realizarse utilizando PowerPoint o un programa similar de presentación de diapositivas.
- En la presentación se expondrá **sólo la Parte 1**.
- La presentación debe constar de un **máximo de 7 diapositivas** (la portada y contraportada no cuentan).
- La presentación debe durar **exactamente 7 minutos** (en concreto, desfases de más de un minuto serán penalizados).
- Cada diapositiva debe contener, como mucho, **50 palabras**.
- Cada diapositiva debe contener un **máximo de dos líneas de código, o 5 líneas de pseudocódigo**.
- Cada mención que permita identificar que el trabajo se ha dividido penalizará, por ejemplo «en la parte de compañero1...», «el código de compañero3...», «en lo que hizo compañero2...». (El trabajo se puede dividir, pero yo no me puedo enterar: hay que llegar a la presentación como una unidad).
- No se permite leer la exposición.

## Parte 1 (50% de la nota de la Práctica 1)

Consiste en la programación de un script que resuelva un problema de programación lineal. Se puede introducir ya en forma matricial sin necesidad de ir capturando una por una las entradas, como si de un software comercial se tratase.

Se trata de programar el algoritmo **«Símplex completo»** visto en clase. Decidirá automáticamente si empezar con Símplex primal o dual y cambiará si fuera necesario. **No hace falta considerar casos degenerados.**

Además, genera un conjunto de datos que pertenezcan a **dos categorías linealmente separables**. Los datos deben estar en **dos dimensiones**. Plantea el problema de minimización del **L1-SVM**, formúlalo como problema dual y aplica el algoritmo que acabas de programar para resolverlo.

## Parte 2 (50% de la nota de la Práctica 1)

La segunda parte de esta práctica consiste en la realización de un **ataque adversario a una red neuronal**. Los cuatro primeros ítems son obligatorios y sólo con ellos se puede obtener un 10 en esta parte 2 de la práctica uno. Sin embargo, hay una serie de puntos opcionales para aquellos tengan interés en probar más cosas. Se recomienda usar **pytorch o tensorflow** para la realización de esta parte. El proceso es el siguiente:

1. Entrena una red neuronal que clasifique con al menos un **95% de acierto** el conjunto de datos de **MNIST**. Elige una arquitectura diferente a la de clase, y asegúrate de que no coincida con la de ningún otro grupo. Puedes utilizar para esto todas las librerías que desees. Si se usa tensorflow, se recomienda usar el dataset importado desde la propia librería con `from tensorflow.keras.datasets import mnist`. **Identifica la cantidad de parámetros** de la arquitectura de tu red neuronal.

2. Entrena una **SVM con núcleo Gaussiano** para MNIST. Puedes utilizar para esto todas las librerías que desees.

3. Genera una función que haga un **ataque de tipo FGSM** a la red neuronal. Si existe una librería de python específica para esto, no se puede usar, pero sí se puede usar (y es recomendable) usar funciones que te ayuden a para calcular los gradientes dentro de la función signo (por ejemplo la función `GradientTape` de tensorflow).

4. Genera unas cuantas imágenes adversarias y trata de predecirlas tanto con tu red neuronal como con la SVM. **Visualiza tanto las originales como las adversarias.**

5. **(Opcional)** Genera imágenes adversarias para todo el conjunto de train y/o test de MNIST y establece el error de cada uno de los dos modelos sobre este conjunto adversario.

6. **(Opcional)** Entrena adversariamente, es decir, entrena tus dos modelos con las **120.000 imágenes**: 60.000 originales y 60.000 adversarias. Calcula el error en el test conjunto (20.000 imágenes, originales y adversarias).

7. **(Opcional)** Ataca a las 60.000 imágenes adversarias, obteniendo 60.000 imágenes «doblemente adversarias». ¿Qué rendimiento obtiene el modelo entrenado adversariamente sobre las imágenes «doblemente adversarias»?

**Asegúrate de fijar las semillas necesarias para que los resultados sean completamente reproducibles.**
