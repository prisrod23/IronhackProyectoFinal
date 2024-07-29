# Predicción de la enfermedad de Alzheimer: un enfoque desde la Ciencia de Datos

## Table of Contents
- [Introduction](#introduction)
- [Problem Statement](#problem-statement)
- [Data Collection](#data-collection)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Feature Engineering](#feature-engineering)
- [Model Building and Evaluation](#model-building-and-evaluation)
- [Results and Discussion](#results-and-discussion)
- [Conclusion](#conclusion)
- [Future Work](#future-work)
- [Contributing](#contributing)
- [License](#license)

## Introduction
El Alzheimer es una de las principales causas de demencia, afectando sobre todo a las personas mayores y causando un deterioro cognitivo progresivo. Detectarla a tiempo y con precisión es clave para tratarla y obtener mejores resultados para los pacientes.
Los métodos tradicionales de diagnóstico, como las neuroimágenes y el análisis del líquido cefalorraquídeo, suelen ser invasivos, prolongados y caros. Pero gracias a los avances en inteligencia artificial y aprendizaje automático, ahora tenemos alternativas prometedoras que son menos invasivas, más rápidas y económicas.
A medida que evolucionan las herramientas de modelado de datos será cada vez más fácil hacer un diagnóstico prematuro para la detección de la enfermedad.

## Problem Statement
El objetivo del proyecto es construir un modelo predictivo que permita identificar la enfermedad de Alzheimer con alta precisión poniendo énfasis en minimizar los falsos-negativos (FN). Número de casos que la prueba declara negativos y que en realidad son positivos. Por ejemplo, decirle a un paciente que no tiene Alzheimer cuando realmente si lo tiene. Tiene unas consecuencias negativas al no tratar al paciente lo antes posible.
Para ello nos centraremos en optimizar nuestros modelos para conseguir tener un Recall y F1-Score cercanos a 1.


## Data Collection
El conjunto de datos utilizado para esta investigación se obtuvo de la plataforma de código abierto Kaggle. https://www.kaggle.com/datasets/rabieelkharoua/alzheimers-disease-dataset


@misc{rabie_el_kharoua_2024,
title={Alzheimer's Disease Dataset},
url={https://www.kaggle.com/dsv/8668279},
DOI={10.34740/KAGGLE/DSV/8668279},
publisher={Kaggle},
author={Rabie El Kharoua},
year={2024}}

El conjunto de datos incluye 35 variables que proporcionan información relacionada con la enfermedad tales como: detalles demográficos, factores del estilo de vida, historial médico, mediciones clínicas, evaluaciones cognitivas y funcionales, síntomas y un diagnóstico de la enfermedad de Alzheimer.


## Data Cleaning and Preparation

No se encontraron duplicados en el dataset.

No se detectaron valores faltantes.

Graficando los datos con boxplots no se detectaron outliers significativos.

Ampliamos el cálculo basado en la desviación estándar respecto a la media y el análisis a partir de los cuantiles.

Se descartaron dos variables sin valor predictivo en una fase temprana:
'PatientID' 
'DoctorInCharge'

Concluimos que el dataset no requiere de ninguna limpieza específica más.


## Exploratory Data Analysis

La variable objetivo identificada es Diagnosis, que representa si un paciente ha sido diagnosticado con Alzheimer (1 para sí, 0 para no).

La distribución muestra un desbalance entre clases, con más pacientes no diagnosticados que diagnosticados. Para determinar la magnitud del desequilibrio calculamos los siguientes Índices:
Índice de Desequilibrio : 1.83.
Índice de Gini : 0.46. 
Nos planteamos reajustar el desequilibrio en el dataset en pasos posteriores.

Los histogramas mostraron las distribuciones de variables con bastante uniformidad, aunque la variable Age no tenía una distribución normal, no se ajustó ya que una distribución asimétrica negativa es esperable en ese tipo de pacientes.

La matriz de correlación ayudó a identificar la relación entre variables numéricas, destacando algunas correlaciones fuertes.
Las áreas más claras y más oscuras fuera de la diagonal indican correlaciones fuertes entre variables específicas. 

Algunos detalles significativos:

Parece que hay una correlación significativa entre diferentes tipos de colesterol (Total, LDL, HDL, Triglycerides), lo cual es lógico debido a la naturaleza de estas mediciones.

La variable ‘Diagnosis’ parece tener una relación interesante con algunas variables como ‘MemoryComplaints’, ‘Confusion’, ‘Disorientation’, ‘PersonalityChanges’, ‘DifficultyCompletingTasks’, y ‘Forgetfulness’. Esto sugiere que estos síntomas pueden ser predictores importantes para el diagnóstico de la enfermedad de Alzheimer.

‘MMSE’ y ‘FunctionalAssessment’ podrían estar correlacionados con la variable ‘Diagnosis’, indicando que estas evaluaciones son cruciales para identificar la presencia de la enfermedad.

Identificamos las variables con mayor correlación como las mejores predictoras:
‘Functional Assessment’
‘Memory Complaints’
‘ADL’
‘Behavioral Problems’
‘MMSE’

## Feature Engineering

Las variables categóricas Ethnicity y EducationLevel se transformaron en binarias utilizando get_dummies.

El resultado final se persistió como clean_dataset.

Para poder compensar el desbalanceo en la variable principal, probamos dos estrategias : 
- Undersampling del dataset usando resample
- Oversampling del dataset usando SMOTE

El resultado final se persistió como Balanced_dataset y Smote_dataset respectivamente.

## Model Building and Evaluation
Se probaron varios modelos, incluyendo KNN, SVM y árboles de decisión, para determinar el mejor rendimiento con los distintos datasets.
Para cada uno de nuestros tres dataset seleccionamos un 80% de las muestras para entrenamiento (Train) y un 20% para prueba (Test), y escalamos con StandardScaler.

XGBoost y Random Forest fueron los modelos más consistentes y con mejor rendimiento, especialmente en el dataset Balanceado. 
Por ello, profundizamos en estos dos modelos para intentar mejorar su rendimiento a través de la selección de variables y el ajuste de sus hiperparámetros.

- Optimización Modelo Random Forest

Se identificaron las variables más importantes usando el algoritmo Random Forest.
Se realizó un Grid Search para optimizar los hiperparámetros del modelo.
El modelo optimizado alcanzó una precisión del 91%, un Recall del 88%, y un F1-Score del 89%.

- Optimización Modelo XGBoost

Se identificaron las variables más importantes usando el algoritmo XGBoost.
Se realizó un Grid Search para optimizar los hiperparámetros del modelo.
El modelo optimizado alcanzó una precisión del 93%, un Recall del 90%, y un F1-Score del 91%.

Se compararon los resultados de los modelos optimizados de Random Forest y XGBoost.

Se realizó una validación cruzada de 10 fold para asegurar la robustez de los modelos.

## Results and Discussion
Se seleccionó el modelo Random Forest optimizado por su mejor rendimiento en Recall, la métrica objetivo.

## Conclusion
Recap the project's achievements and lessons learned.

## Future Work
1. Implementación del modelo en un entorno de producción.
2. Monitoreo continuo del rendimiento del modelo.
3. Actualización del modelo con nuevos datos para mantener su precisión.

## Contributing
Feel free!

## License

El contenido de este repositorio está licenciado bajo la Licencia Creative Commons Atribución-NoComercial 4.0 Internacional (CC BY-NC 4.0).
Para más detalles, puede consultar la [Licencia completa](https://creativecommons.org/licenses/by-nc/4.0/deed.es).

