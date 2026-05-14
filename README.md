# Lead Scoring — Predicción y Segmentación de Leads Comerciales

Sistema de scoring comercial que combina segmentación no supervisada (KMeans) y clasificación supervisada (XGBoost) para predecir la probabilidad de compra de cada lead y priorizar la acción comercial.

## Tecnologías

Python · Pandas · Scikit-learn · XGBoost · Matplotlib · Jupyter Notebook

## Estructura del repositorio

```
├── 01_Documentos/
│   └── lead_scoring.yml                      # Configuración del entorno
│
├── 02_Datos/
│   ├── 01_Originales/
│   │   └── Leads.csv                         # Dataset original
│   ├── 02_Validacion/
│   │   └── validacion.csv
│   └── 03_Trabajo/
│       ├── cat_resultado_calidad.pickle
│       ├── cat_resultado_eda.pickle
│       ├── df_tablon.pickle
│       ├── muestra.csv
│       ├── num_resultado_calidad.pickle
│       ├── num_resultado_eda.pickle
│       ├── perfiles_df.pickle
│       ├── trabajo.csv
│       ├── trabajo_resultado_calidad.pickle
│       ├── x_preseleccionado.pickle
│       └── y_preseleccionado.pickle
│
├── 03_Notebooks/
│   └── 02_Desarrollo/
│       ├── 99_Imagenes/
│       │   ├── Excel_procesos.png
│       │   └── Proceso_pipeline.PNG
│       ├── 001_LEAD_SCORING_Procesos.xlsx
│       ├── 01_Set_Up.ipynb
│       ├── 02_Calidad_de_Datos.ipynb
│       ├── 03_EDA.ipynb
│       ├── 04_Transformacion_de_datos.ipynb
│       ├── 05_Modelizacion_para_No_Supervisado.ipynb
│       ├── 06_Preseleccion_de_variables.ipynb
│       ├── 07_Modelizacion_para_Clasificacion.ipynb
│       ├── 08_Preparacion_del_codigo_de_produccion.ipynb
│       ├── 09_Codigo_de_reentrenamiento.ipynb
│       ├── 10_Codigo_de_ejecucion.ipynb
│       └── PRO_Pipelines.ipynb
│
├── 04_Modelos/
│   ├── pipe_ejecucion.pickle
│   └── pipe_entrenamiento.pickle
│
├── 05_Resultados/
│   ├── variables_finales.pickle
│   └── Lead Scoring.pdf                      # Presentación del proyecto
│
└── README.md
```

## El problema

Un equipo comercial recibe cientos de leads. No todos tienen la misma probabilidad de comprar. El sistema asigna a cada lead una puntuación entre 0 y 1 que refleja su probabilidad de conversión, permitiendo priorizar los contactos con mayor potencial.

## Pipeline

### 1. Segmentación (No supervisado)
KMeans sobre el dataset completo para identificar perfiles de lead diferenciados.
- **Solución final: 5 clusters**
- Métricas evaluadas: Codo, Silueta, Calinski-Harabasz, Davies-Bouldin

### 2. Scoring (Supervisado)
Clasificación binaria para predecir probabilidad de compra.
- **Algoritmo:** XGBoost Classifier con GridSearchCV
- **AUC-ROC sobre validación: 0.901**
- **Variables más importantes:** score_actividad, tiempo_en_site_total, origen_Lead Add Form, ocupacion, visitas_total

## Producción

El sistema tiene dos modos:

- **Reentrenamiento** (`09_Codigo_de_reentrenamiento.ipynb`): aplica las mismas transformaciones y configuración del modelo sobre nuevos datos sin repetir el análisis completo.
- **Ejecución** (`10_Codigo_de_ejecucion.ipynb`): carga el pipeline serializado y genera el scoring sobre cualquier dataset nuevo en segundos.

## Cómo ejecutarlo

```bash
# Crear entorno desde el yml del proyecto
conda env create --file 01_Documentos/lead_scoring.yml --name lead_scoring

# Activar entorno
conda activate lead_scoring

# Ejecutar notebooks en orden numérico desde 03_Notebooks/02_Desarrollo/
# Empezar por: 01_Set_Up.ipynb
```

---

Proyecto académico desarrollado durante el Master en Data Science de Evolve.
