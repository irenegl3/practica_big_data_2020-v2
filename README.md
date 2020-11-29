# Predicción de retraso de vuelos

Proyecto inicial obtenido del repositorio https://github.com/ging/practica_big_data_2019, basado en https://github.com/rjurney/Agile_Data_Code_2 .

Se trata de la implementación de un sistema completo que usa un modelo predictivo, también creado por el sistema, para realizar predicciones en tiempo real de nuevos vuelos.

## Tecnologías empleadas
- Mongo versión 4.4.2
- Flask
- Kafka versión 2.12-2.3.0
- Zookeper versión 3.5.5
- Spark versión 2.4.4
- SBT
- Python3
- PIP
- Docker-compose 
- Google Cloud

## Arquitectura
[<img src="images/video_course_cover.png">](http://datasyndrome.com/video)

## Proceso

1. Descargar el dataset con la información de vuelos y sus retrasos, con el fin de entrenar el modelo de Machine Learning. Este paso se ha realizado previamente, y los datos obtenidos se encuentran en la carpeta **data**. Se han almacenado dichos datos en la base de datos mongo.

2. Crear el flujo de comunicación que permitirá el envío de datos desde el job de Spark con el servidor web de Flask. Para ello se ha empleado Zookeeper y Kafka, y se ha creado un topic al que se suscribirá el job de Spark.

2. Entrenar el modelo predictivo empleando el algoritmo RandomForest con los datos obtenidos. Para ello se ha empleado PySpark.

3. Ejecutar el job de Spark que predice el retraso del vuelo indicado por el usuario. Para ello se ha empleado spark-submit, que ejecuta el fichero jar que contiene la clase de Scala que realiza las funciones necesarias, entre las que se encuentra generar un *stream* de comunicación subscribiéndose al topic de Kafka (paso 2) para consumir sus datos, y conectarse a la base de datos mongo para insertar las predicciones hechas.

4. Servidor web de Flask donde el usuario podrá seleccionar que vuelo quiere predecir y podrá ver el resultado de la predicción. Este componente envía, mediante Kafka, la información solicitada por el usuario, para que el job de Spark la consuma y genere la predicción correspondiente. Gracias al continuo *polling* que flask hace a Mongo, puede consultar los resultados de la predicción y mostrarlos en la interfaz web.

## Implementación
En este proyecto se han realizado las siguientes implementaciones a parte del funcionamiento básico (4 puntos):
- Spark-submit para ejecutar el job de predicción, en lugar de usar IntelliJ como que se propone inicialmente en el enunciado (1 punto)
- Dockerizar cada servicio por separado, generando contenedores distintos para Zookeeper, Kafka, Mongo, Spark y WebServer (1 punto)
- Despliegue de los servicios dockerizados mediante docker-compose, haciendo uso del docker-compose.yml añadido en el repositorio (1 punto)
- Despliegue de todo el sistema en la plataforma Google Cloud (1 punto)

## Instrucciones de despliegue