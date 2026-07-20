# Hotel Booking Cancellation Predictor

## Descripción del Proyecto
Este proyecto es una solución integral de Machine Learning diseñada para predecir la probabilidad de que un cliente cancele su reserva de hotel. A través de un pipeline automatizado, el sistema ingiere datos históricos, limpia variables, realiza ingeniería de características (*Feature Engineering*) y despliega un algoritmo de ensamble optimizado.

El objetivo de negocio es reducir la fuga de capital por habitaciones vacías (Falsos Negativos) permitiendo al hotel tomar decisiones proactivas de retención de clientes.

## Arquitectura y Stack Tecnológico
* **Lenguaje:** Python 3
* **Procesamiento de Datos:** Pandas, NumPy
* **Visualización (EDA):** Matplotlib, Seaborn
* **Machine Learning:** Scikit-Learn (Pipelines, RandomForest, GridSearchCV)
* **Serialización:** Joblib
* **Despliegue Planificado:** Próximamente integración como microservicio con **FastAPI**.

## Pipeline de Datos (Feature Engineering)
Durante la fase de análisis y preprocesamiento (`01_hotel_eda.ipynb`), se implementaron estrategias críticas de limpieza:
1. **Prevención de Data Leakage:** Eliminación de variables futuras (`reservation_status`, `reservation_status_date`).
2. **Creación de Señales de Negocio:** Generación de la variable booleana `is_corporate`, aislando el comportamiento de alta fidelidad de los viajeros de negocios.
3. **Reducción de Cardinalidad:** Agrupación dinámica (Frequency Capping) en la variable `country`, conservando el Top 10 de tráfico internacional y mitigando el ruido estadístico.

## Rendimiento del Modelo
Se estableció un modelo de Regresión Logística como *Baseline* y, tras una búsqueda exhaustiva de hiperparámetros (GridSearchCV), se implementó un **Random Forest Classifier** con los siguientes resultados clave en la clase minoritaria (Cancelaciones):

* **Accuracy Global:** 88%
* **Recall (Cancelaciones):** 85% (El modelo atrapa casi 9 de cada 10 cancelaciones reales antes de que ocurran).
* **Mejores Hiperparámetros:** `max_depth: 20`, `min_samples_split: 2`, `n_estimators: 100`.

## Estructura del Repositorio
```text
├── data/
│   ├── raw/                 #  Dataset original
│   └── processed/           #  hotel_bookings_clean.csv
├── notebooks/
│   ├── 01_hotel_eda.ipynb         # Limpieza, EDA y Feature Engineering
│   └── 02_predictive_model.ipynb  # Baseline, GridSearchCV y Serialización
│   └── sandobox.ipynb             # Investigacion de variables y conclusiones generales de procedimientos
├── requirements.txt         # Dependencias del núcleo del proyecto
├── .gitignore               # Exclusión de binarios, caché, etc. 
└── README.md                # Documentación del proyecto