# PREDICCIÓN DE CONTENIDO DE ALUMINIO Y NIVELES DE PH EN SUELO AGRÍCOLA
>Manuel Alejandro González, Santiago Alonso

Video para conocer más acerca del proyecto: https://youtu.be/t5haGGzXKgQ

En este proyecto, se utilizaron datos de **muestras de suelo** de cultivos en diferentes regiones de Colombia, junto con las mediciones de radiancia en diferentes espectros de luz, y su nivel de aluminio y pH del suelo medidos con técnicas convencionales. Utilizando estos datos, se implementaron modelos de regresión por **vectores de soporte** y **redes neuronales** para **predecir los niveles de pH y aluminio** de las muestras.

# Metodología
El dataset trabajado fue limpiado de valores no numéricos y desconocidos. Luego se utilizaron dos métodos para predecir tanto el nivel de pH como el de aluminio. El primer método fue el de redes neuronales (Multi-layer Perceptron regressor). El segundo método fue utilizando vectores de soporte (Epsilon-Support Vector Regression). Ambos modelos fueron hechos usando la librería SkLearn. Para lograr el mejor método, se evaluó el coeficiente de determinación de cross-validaciones para diferentes aspectos del modelo: como la normalización, la reducción dimensional (usando PCA) y los diferentes hiperparámetros de los métodos. Una vez se encontró el modelo con el mejor coeficiente de determinación, este se evaluó sobre un conjunto de prueba, el cual contenía el 10% de los datos iniciales.

## Limpieza de datos
El dataset inicialmente contaba con 6178 muestras. Sin embargo, muchas de estas tenían valores NA. Se decidió eliminar las muestras con alguno de estos NA porque obteníamos de todas formas una cantidad grande de datos. Para los datos de la regresión de aluminio, se trabajó con 1599 muestras finales. Para la regresión de pH, se trabajó con 3178 muestras finales. 

Para realizar esto se utilizó la función **dropna()** de la librería pandas.

## Red neuronal para predicción de pH

>**Efectos de la normalización**
Primero, se evaluó el efecto de la normalización de los datos, midiendo el coeficiente de determinació del modelo con *cross-validación* de 5 folds. Se encontró que sin normalizar los datos, el R2 fue de: **0.457** y con normalización fue de: **0.561**. Por eso **se decidió seguir trabajando con las características normalizadas.**

>**Efectos de la reducción dimensional**
Luego, se evaluaron los efectos de la reducción dimensional, ya que se contaba con 246 características. La reducción dimensional se hizo por PCA. Se probaron diferentes valores de varianza explicada, incluyendo una PCA conservando todos los componentes. Los resultados fueron los siguientes: 
Según estos resultados se decidió seguir trabajando sobre los **datos normalizados y con una PCA que conservara el 100% de los componentes.** con lo que se obtuvo ya un R2 de **0.787**

>**Iteración de hiperparámetros**
Se evaluó con que parámetros funcionaba mejor el modelo. Aquí se evaluó el efecto de la combinación de las diferentes funciones de activación de la red y de los diferentes optimizadores. Luego se evaluó el efecto del valor de la taza de aprendizaje.
Según lo anterior, se decidió que el **mejor modelo era normalizando los datos, realizando una PCA dejando el 100% de los componentes y con una red neuronal con función de activación ReLU, optimizador adam y taza de aprendizaje 0.0001**.

>**Evaluación final del modelo**
Al evaluar el modelo final con los datos de prueba (10% de los datos) se obtuvo un coeficiente de determinación de **0.7685. **

## Red neuronal para predicción de Aluminio
>**Efectos de la normalización**
Primero, se evaluó el efecto de la normalización de los datos, midiendo el coeficiente de determinació del modelo con *cross-validación* de 5 folds. Se encontró que sin normalizar los datos, el R2 fue de: **0.205** y con normalización fue de: **0.477**. Por eso **se decidió seguir trabajando con las características normalizadas.**

>**Efectos de la reducción dimensional**
Luego, se evaluaron los efectos de la reducción dimensional, ya que se contaba con 246 características. La reducción dimensional se hizo por PCA. Se probaron diferentes valores de varianza explicada, incluyendo una PCA conservando todos los componentes. Los resultados fueron los siguientes: 
Según estos resultados se decidió seguir trabajando sobre los **datos normalizados y con una PCA que conservara el 100% de los componentes.** con lo que se obtuvo ya un R2 de **0.720**

>**Iteración de hiperparámetros**
Se evaluó con que parámetros funcionaba mejor el modelo. Aquí se evaluó el efecto de la combinación de las diferentes funciones de activación de la red y de los diferentes optimizadores. Luego se evaluó el efecto del valor de la taza de aprendizaje.
Según lo anterior, se decidió que el  **mejor modelo era normalizando los datos, realizando una PCA dejando el 100% de los componentes y con una red neuronal con función de activación ReLU, optimizador adam y taza de aprendizaje 0.0001**.

>**Evaluación final del modelo**  
> Al evaluar el modelo final con los datos de prueba (10% de los datos) se obtuvo un coeficiente de determinación de **0.6568. **

## SVM para predicción de pH

>**Efectos de la normalización**
Primero, se evaluó el efecto de la normalización de los datos, midiendo el coeficiente de determinació del modelo con *cross-validación* de 5 folds. Se encontró que sin normalizar los datos, el R2 fue de: **0.532** y con normalización fue de: **0.576**. Por eso **se decidió seguir trabajando con las características normalizadas.**

>**Efectos de la reducción dimensional**
Luego, se evaluaron los efectos de la reducción dimensional, ya que se contaba con 246 características. La reducción dimensional se hizo por PCA. Se probaron diferentes valores de varianza explicada, incluyendo una PCA conservando todos los componentes. Los resultados fueron los siguientes: 
Según estos resultados se decidió seguir trabajando sobre los **datos normalizados y con una PCA que conservara el 100% de la varianza explicada.** con lo que se obtuvo ya un R2 de **0.576**

>**Iteración de hiperparámetros**
Se evaluó con que parámetros funcionaba mejor el modelo. Aquí se evaluó el efecto de la combinación de las diferentes funciones de activación de la red y de los diferentes optimizadores. Luego se evaluó el efecto del valor de la taza de aprendizaje.
j
Según los resultados anteriores, el modelo final se terminó ajustando con los **datos normalizados, transformados con una PCA al 100% de componentes, y se usó el SVR con un tipo de “kernel: linear” y un valor de “gamma” de 0.1.**
Una vez se evaluó el modelo final con los datos de prueba (10% de los datos) se logró obtener un Coeficiente de determinación de **0.572**. Esto es inferior a lo logrado mediante las redes neuronales.

## SVM para predicción de Aluminio
>**Efectos de la normalización**
Primero, se evaluó el efecto de la normalización de los datos, midiendo el coeficiente de determinació del modelo con *cross-validación* de 5 folds. Se encontró que sin normalizar los datos, el R2 fue de: **0.168** y con normalización fue de: **0.213**. Por eso **se decidió seguir trabajando con las características normalizadas.**

>**Efectos de la reducción dimensional**
Luego, se evaluaron los efectos de la reducción dimensional, ya que se contaba con 246 características. La reducción dimensional se hizo por PCA. Se probaron diferentes valores de varianza explicada, incluyendo una PCA conservando todos los componentes. Los resultados fueron los siguientes: 
.
Según estos resultados se decidió seguir trabajando sobre los **datos normalizados y con una PCA que conservara el 100% de los componentes.** con lo que se obtuvo ya un R2 de **0.213**

>**Iteración de hiperparámetros**
Se evaluó con que parámetros funcionaba mejor el modelo. Aquí se evaluó el efecto de la combinación de las diferentes funciones de activación de la red y de los diferentes optimizadores. Luego se evaluó el efecto del valor de la taza de aprendizaje.
.
Según los resultados anteriores, el modelo final se terminó ajustando con los datos normalizados, transformados con una PCA al 100% de componentes, y se usó el SVR con un tipo de “kernel: linear”, un C (parámetro que controla el equilibrio entre el ajuste de los datos de entrenamiento y la suavidad de la función de regresión.) estándar de 100 y un valor de “gamma” de “auto”.
Una vez se evaluó el modelo final con los datos de prueba (10% de los datos) se logró obtener un Coeficiente de determinación de 0.454. Esto es inferior a lo logrado mediante las redes neuronales.

# Conclusiones
A partir de los resultados, se encontró que los mejores modelos para predecir tanto el aluminio como el nivel de pH, son los de redes neuronales (MLP regressor), obteniendo coeficientes de determinación de 0.77 para la predicción del pH y de 0.66 para predecir aluminio. Así que para el pH, se obtuvo con las redes neuronales un modelo que logra comportarse bien y a partir de la espectrometría predecir bien esta variable, sin embargo no es perfecto y requiere de más trabajo. Para predecir aluminio, el modelo logrado no se comporta tan bien pero es un primer acercamiento para predecir este factor del suelo.
