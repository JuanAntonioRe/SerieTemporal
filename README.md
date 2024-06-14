# Serie Temporal
Entrenamiento de varios modelos para una serie temporal.

## Descripción del proyecto
Una compañía de Taxi llamada Sweet Lift, ha recopilado datos históricos sobre pedidos de taxis en los aeropuertos. Para atraer a más conductores durante las horas pico, se necesita predecir la cantidad de pedidos de taxis para la próxima hora.

La métrica RECM en el conjunto de prueba no debe ser superior a 48.

Los datos se deben remuestrear de tal forma que cada punto de datos de los datos originales caigan dentro de intervalos de una hora.

## Objetivo
La tarea es una tarea de regresión, ya que nuestro objetivo es determinar las horas en los que son más solicitados los taxis.

## Desarrollo del proyecto
Para este caso de serie temporal nuestro dataset contiene sólo dos columnas: una con la fecha y hora de la solicitud del taxi y la otra con l cantidad de solicitudes de taxi.

### Preparación de los datos
Se tiene que convertir el dataset en una serie temporal. Esto significa, convertir el tipo de datos de la columna con las fechas al tipo `datetime`. Una vez realizado esto, la convertimos en el índice del DataFrame y lo ordenamos de manera ascendente.

El remuestreo que se solicita el cual dice que los datos originales caigan dentro de intervalos de una hora también se realiza en esta sección del proyecto.

### Análisis exploratorio de datos
Se realiza un análisis para saber los horarios en los que se realizan más pedidos de taxis. 

El análiis muestra que en los aeropuertos, los taxis son más solicitados durante las madrugadas de los veranos.

También se realiza un estudio de **tendencia y estacionalidad** el cuál afirma lo que ya se había dicho antes. Además se encuentra que la estacionalidad es la misma sin importar el mes.

### Formación de características
Al tener sólo una columna es necesario que se creen nuevas características para poder entrenar un modelo. Para esto se desarrolla una función que crea características de calendario, características de desfase y caracaterísticas de media móvil. De esta forma ya se puede entrenar un modelo.

### Entrenamiento de modelos
Después de crear los conjuntos de entrenamiento y prueba, se entrenan 3 modelos de los cuales se selecciona al que tenga mejor RECM. Dichos modelos son: Bosque aleatorio de regresión, CatBoost y LightGBM.

Se concluye que LightGBM es el mejor modelo, ya que su RECM es de 3.07.

## Conclusiones
Al evaluar el modelo seleccionado con el conjunto de prueba obtenemos un RECM de 14.63. Este es un valor alto en comparación con el conjunto de entrenamiento, pero sigue siendo mucho menor que el valor solicitado. Con esto se concluye que nuestro modelo funciona.

## Tecnologías usadas
* Pandas
* Matplotlib
* statsmodels.tsa.seasonal
    + seasonal_decompose
* sklearn: 
    + train_test_split
    + mean_squared_error
    + RandomForestRegressor
* CatBoost
* LightGBM