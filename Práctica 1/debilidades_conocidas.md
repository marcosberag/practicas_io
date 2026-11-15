# Debilidades conocidas · Análisis de IA

Observaciones pendientes de validación docente. Se conserva el código original, sin aplicar correcciones.

- **Símplex:** sin método de dos fases ni garantía general frente a degeneración. `no_resuelto` no implica infactibilidad.
- **Dual del L1-SVM:** la igualdad representada por dos desigualdades introduce una base inicial degenerada. ¿Es aceptable para el alcance de la práctica?
- **Interpretación del óptimo:** se utiliza la tabla del L1-SVM sin comprobar antes que el estado sea `optimo`.
- **Generación de datos:** una separación inviable puede dejar el bucle sin terminar.
- **Opcional 6:** `validation_split=0.1` deja **108.000 imágenes** para ajustar la red, frente a las **120.000** indicadas en el enunciado.
- **Validación del opcional 6:** el barajado puede repartir una imagen original y su adversaria entre entrenamiento y validación; ambas particiones dejan de ser independientes por imagen de origen.

**Alcance de la evidencia:** los opcionales 5–7 no tienen una ejecución completa verificada. Las salidas conservadas son las originales. También queda por confirmar la originalidad de la arquitectura respecto a clase y otros grupos.
