# DeepL_Farmacia

Combinaré una red convolucional para extraer características de los datos temporales seguido por una red recurrente para modelar las secuencias temporales.


Paso 1: Preparar los datos

Primero, necesitamos asegurarnos de que tus datos estén en el formato adecuado para el modelado de series de tiempo.

1. **Limpieza y preprocesamiento**:
   - Convertir la columna `AñoSem` en una marca de tiempo si aún no lo es.
   - Ordenar los datos por esta marca de tiempo para asegurar que la secuencia temporal sea correcta.
   - Comprobar si hay valores faltantes en los datos y decidir cómo manejarlos (eliminarlos, imputarlos, etc.).

2. **Normalización**:
   - Normalizar los datos numéricos como `Piezas` e `ImporteFarmacia` para que el entrenamiento del modelo sea más estable.

3. **Estructuración para series de tiempo**:
   - Dependiendo de la granularidad de las predicciones y el tamaño de la ventana temporal que quieres utilizar, transforma los datos en un formato de secuencia (por ejemplo, utilizar las ventas de las últimas 4 semanas para predecir la siguiente semana).

### Paso 2: Crear conjuntos de datos de entrenamiento, validación y prueba

- Dividir los datos en conjuntos de entrenamiento, validación y prueba.
- Asegurarse de que no hay solapamiento temporal entre estos conjuntos para evitar el riesgo de fuga de datos.

### Paso 3: Definir el modelo híbrido

Para el modelo híbrido, utilizaremos una combinación de CNN y RNN (como LSTM).

1. **Capa CNN**:
   - Utiliza capas convolucionales para extraer características de los datos de entrada. Puedes usar varias capas convolucionales seguidas de capas de pooling para reducir la dimensionalidad.

2. **Capa LSTM**:
   - Las características extraídas por la CNN se alimentarán a una o varias capas LSTM para capturar las dependencias temporales.

3. **Capas Densas**:
   - Después de la LSTM, una o más capas densas pueden ser usadas para la predicción final.

4. **Salida**:
   - La capa de salida dependerá del tipo de predicción que estés haciendo (por ejemplo, regresión para predecir valores continuos).

### Paso 4: Entrenamiento del modelo

- Compilar el modelo con una función de pérdida adecuada y un optimizador.
- Entrenar el modelo en el conjunto de datos de entrenamiento y validar su rendimiento en el conjunto de validación.
- Ajustar los hiperparámetros según sea necesario basado en el rendimiento del modelo.

### Paso 5: Evaluación y ajustes

- Evaluar el modelo en el conjunto de datos de prueba para ver cómo generaliza en datos no vistos.
- Hacer ajustes si es necesario (ajustar la arquitectura del modelo, cambiar hiperparámetros, etc.).
