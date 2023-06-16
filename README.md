# Métodos de aprendizaje automático para la detección de factores de riesgo en el consumo de sustancias




## Julián Camilo Velandia
### Universidad Nacional de Colombia jvelandiag@unal.edu.co

## William Giovanni Quevedo
### Universidad Nacional de Colombia wgquevedob@unal.edu.co 



# Abstract

En el presente trabajo, se compararon tres métodos de aprendizaje automático (redes neuronales, árboles de decisión y random forest) para detectar factores de riesgo en el consumo de sustancias en la población universitaria a partir del estudio epidemiológico andino sobre consumo de drogas en la población universitaria de Colombia. Se identificaron variables predictoras relevantes, como la edad, el género, el entorno social y los antecedentes familiares de consumo. Estos hallazgos respaldan el uso de métodos de aprendizaje automático en la prevención del consumo de sustancias en la población universitaria.


 # Metodología

 ## Descripción del dataset

Se dispone de un extenso conjunto de datos recopilados en el marco del III Estudio Epidemiológico Andino sobre Consumo de Drogas en la Población Universitaria de Colombia, correspondiente al año 2016. Este estudio aborda diversas dimensiones relacionadas con el consumo de sustancias psicoactivas en el entorno universitario, con un enfoque particular en el tabaco, el alcohol, la marihuana y la cocaína, consideradas de gran relevancia debido a su prevalencia y potenciales riesgos asociados.

El objetivo general de esta investigación radica en estimar la magnitud del consumo de drogas lícitas e ilícitas entre la población universitaria, así como en identificar los principales factores de riesgo y protección asociados a dicho consumo. Específicamente, se busca comprender la percepción de riesgo que tienen los estudiantes en relación con estas sustancias, evaluar la existencia de un uso de riesgo o perjudicial, analizar el entorno en el que se lleva a cabo el consumo, así como examinar la facilidad de acceso y oferta de las sustancias psicoactivas en el contexto universitario.

Para llevar a cabo esta investigación, se implementó una rigurosa metodología de recolección de datos. En primer lugar, se realizaron selecciones al azar de universidades representativas en el país, asegurando una adecuada representatividad geográfica y demográfica. A continuación, se capacitó a coordinadores que supervisaron el desarrollo del estudio en cada institución seleccionada. Posteriormente, se procedió a la elección de los estudiantes participantes, siguiendo criterios de muestreo aleatorio y procurando alcanzar una muestra representativa de la población universitaria en su conjunto.

La recopilación de los datos se llevó a cabo mediante la aplicación de encuestas estructuradas por cuestionarios en línea, garantizando así la confidencialidad y privacidad de los participantes. Esta metodología permitió obtener información detallada y precisa sobre el consumo de drogas en el ámbito universitario, así como sobre los factores de riesgo y protección asociados. Cabe mencionar que, debido a la cantidad de datos recabados y a la importancia de las sustancias antes mencionadas, el presente análisis se centrará específicamente en el tabaco, el alcohol, la marihuana y la cocaína.

El dataset en cuestión, contiene información sensible y privada sobre el consumo de sustancias entre estudiantes universitarios. Por razones de privacidad y ética, es fundamental asegurar la confidencialidad y protección de los datos personales de los participantes involucrados en la investigación.

Para garantizar la confidencialidad de los participantes y cumplir con los principios éticos y legales de la investigación, hemos decidido no subir el dataset a repositorios públicos. Si otros investigadores están interesados en acceder al dataset para fines de replicación o colaboración, les pedimos que se pongan en contacto con nosotros directamente.

 ## Preprocesamiento de datos

El dataset en cuestión consta de una serie de preguntas agrupadas por temática. En la primera parte se tiene las preguntas que conforman el perfil base del estudiante (104 preguntas útiles o que fueron respondidas por la mayoría de usuarios), algunas de estas preguntas son las siguientes: 

¿En qué año ingresó usted a la carrera que estudia actualmente?
¿Cuál es el estrato al que pertenece su vivienda?
¿Cómo calificaría su situación económica?

Luego se separan en datos de entrenamiento y validación en una proporción 80/20, para ser utilizados en los métodos de aprendizaje automático.

La tarea a resolver por los métodos de aprendizaje automático será la de predecir la pregunta sobre el consumo de cada sustancia a partir del perfil base de cada estudiante, las preguntas son las siguientes:

 Tabaco: ¿Ha fumado usted cigarrillos u otro tipo de tabaco alguna vez en la vida?
Alcohol: ¿Ha consumido alcohol alguna vez en su vida? (bebidas alcohólicas como cerveza, vino, aguardiente, champaña, brandy, whisky u otros licores con alta graduación alcohólica o combinados, o bien de uso inyectado)
Marihuana: ¿Ha consumido marihuana alguna vez en su vida?
Cocaína:  ¿Ha consumido cocaína alguna vez en su vida?

Donde todas son de respuesta si o no (Binarias).

También se tiene información sobre el resultado de la encuesta AUDIT sobre consumo de alcohol, por lo que también se realizarán los métodos de aprendizaje automático con está variable

 ## Métodos de aprendizaje automático

La tarea a resolver por los métodos de aprendizaje automático será la de predecir la pregunta sobre el consumo de cada sustancia a partir del perfil base de cada estudiante

### 2.3.1	Redes neuronales 

Primero se realiza un primer acercamiento con redes neuronales, se plantea la siguiente arquitectura, ya que se cuentan con cerca de 104 características y con cerca de 1190 datos de entrenamiento:

![Frame 2](https://github.com/julianVelandia/CICAD_UNAL_2016/assets/52173621/d4abbc93-bb04-4fcc-b682-23ff48a415b3)

Figura 1: Arquitectura de redes neuronales utilizada

Se plantea una distribución de la capa de entrada con el número de entradas, 3 capas ocultas, de 4, 2 y 2 neuronas respectivamente, una capa de salida, Para todas las capas se usa la función de activación Relu, excepto para la última, ya que es binaria y se usa Sigmoide.

Para la capa de 4 neuronas se utiliza la técnica de Dropout, la cual ayuda a prevenir el sobreajuste al apagar aleatoriamente neuronas durante el entrenamiento, lo que obliga a las demás a tomar decisiones por sí mismas. Esto fomenta la generalización y mejora el rendimiento en datos nuevos.

También se utilizó EarlyStopping el cual es una estrategia en el entrenamiento de redes neuronales que detiene el proceso cuando el rendimiento en un conjunto de validación deja de mejorar, evitando así el sobreajuste. Esto ayuda a seleccionar el mejor modelo y a ahorrar tiempo y recursos computacionales.


### 2.3.1	Árboles binarios

Se utilizó un árbol de decisión para clasificar un conjunto de datos con DecisionTreeClassifier de la biblioteca sklearn. Después de entrenar el clasificador de árbol de decisión con los datos de entrenamiento, se realizó una predicción en el conjunto de validación, luego, se calculó la precisión de la predicción comparando las etiquetas verdaderas con las etiquetas predichas.

Se generó una representación textual del árbol de decisión, la cual muestra las condiciones utilizadas en cada nodo del árbol para tomar decisiones y las clases finales en las hojas.

Se generó una visualización gráfica del árbol de decisión, donde cada nodo representa una división en las características y las hojas representan las clases finales. 

Se calculó la importancia de las características, esta propiedad del clasificador de árbol de decisión proporciona una medida de la importancia relativa de cada característica en la clasificación. 

### 2.3.1	Random Forest

Se usa RandomForestClassifier de la librería sklearn, la que permite construir y entrenar el clasificador de bosque aleatorio con los siguientes parámetros: 

n_estimators: el número de árboles en el bosque, establecido en 100. Cuanto mayor sea este valor, más complejo será el modelo.
max_depth: la profundidad máxima de cada árbol en el bosque, establecida en 5. Limitar la profundidad ayuda a evitar el sobreajuste.
random_state: un número entero que se utiliza como semilla para garantizar la reproducibilidad de los resultados.

Luego, se ajusta el clasificador al conjunto de datos de entrenamiento y se entrena el clasificador utilizando el algoritmo de bosque aleatorio y los datos proporcionados. Luego se calcula la precisión del clasificador.
Por último, se imprimirá la información relevante de cada árbol en el bosque, como la profundidad, la cantidad de nodos y la importancia de las características. 

# Referencias

1.	ONUDC. Informe Mundial Sobre las Drogas 2022 [Internet]. Viena; 2022 jun [citado el 9 de junio de 2023]. Disponible en: https://www.unodc.org/res/wdr2022/MS/WDR22_Booklet_2_spanish.pdf
2.	ONUDC, Ministerio de Justicia y del Derecho. III Estudio epidemiológico andino sobre consumo de drogas en la población universitaria de Colombia. Bogotá D.C.; 2017. 
3.	Sistema de Alertas Tempranas de Colombia. Aparición de Nuevas Sustancias Psicoactivas en Colombia [Internet]. Bogotá D.C.; 2017 ene [citado el 9 de junio de 2023]. Disponible en: https://www.minjusticia.gov.co/programas-co/ODC/Documents/SAT/Boletines/2017%2001%20Boletin_sat.pdf
 
