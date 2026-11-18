# 🐾 Modelado Predictivo y Enriquecimiento Biológico en Adopción de Mascotas

**Autor:** Diego Videla Silva  
**Comisión:** 96160  
**Curso:** Data Science II - Machine Learning para la Ciencia de Datos (Coderhouse)  
**Entrega:** Entrega Final (ETL, Enriquecimiento vía API, EDA, Machine Learning y SHAP)

**📄 Informe Final:** [EntregaFinal_Videla_AdopcionMascotas_Documentado.pdf](Documentos/EntregaFinal/EntregaFinal_Videla_AdopcionMascotas_Documentado.pdf)

## 📌 Descripción del Proyecto

La sobrepoblación en refugios y centros de rescate animal es un desafío logístico y de bienestar crítico. Este proyecto combina un registro transaccional de mascotas en adopción (Kaggle, 14.993 registros) con datos biológicos reales obtenidos mediante APIs externas (*The Dog API* & *The Cat API*).

El objetivo principal es resolver un problema de **Clasificación Binaria**: predecir al momento del ingreso qué mascotas corren **riesgo de estancamiento** (más de 100 días en el refugio o no adoptadas) para que la organización pueda asignar presupuesto de marketing y fotografía de forma proactiva.

## 🗂️ Estructura del Repositorio

```text
📁 coderhouse_DC2_1
│
├── 📁 dataset/                              # Datasets originales y caché local de las APIs
│   ├── AdopcionMascotas.csv
│   ├── BreedLabels.csv
│   └── biologia_api_cache.csv
├── 📁 Documentos/                           # Entregables formales
│   ├── 📁 EntregaFinal/                     # Informe de la entrega final
│   │   └── EntregaFinal_Videla_AdopcionMascotas_Documentado.pdf
│   └── 📁 PrimeraEntrega/                   # Entregables de la primera entrega
│       ├── Entrega1_Videla_AdopcionMascotas_Documentado.pdf
│       └── Entrega1_Videla_AdopcionMascotas_Documentado_Presentacion.pdf
│
├── .env.template                            # Plantilla de referencia para API Keys
├── .gitignore                               # Exclusiones de Git (ignora .env y entorno virtual)
├── Diccionario API.png                      # Respaldo visual del diccionario de la API
├── Diccionario Columnas.png                 # Respaldo visual del diccionario del dataset base
├── Entrega1_Videla_AdopcionMascotas.ipynb   # Notebook principal (ETL, EDA, ML y SHAP)
├── requirements.txt                         # Dependencias del proyecto
└── README.md                                # Documentación principal del repositorio
```

## 🛠️ Tecnologías y Metodología Implementada

- **Lenguaje:** Python 3
- **Librerías:** `pandas`, `numpy`, `requests`, `python-dotenv`, `matplotlib`, `seaborn`, `plotly`, `scikit-learn`, `xgboost`, `shap`, `difflib`.
- **Pipeline de Datos y Machine Learning:**
  1. **Ingesta y ETL:** Carga de datos transaccionales y consumo de APIs REST con mecanismo de caché local.
  2. **Limpieza Semántica con IA:** Resolución de discrepancias de razas mediante *Fuzzy String Matching* (`difflib`) auditado con un LLM bajo criterios clínicos veterinarios.
  3. **EDA y Visualización Interactiva:** Validación de 4 hipótesis de negocio, incluyendo segmentación por especie (perro vs. gato) con gráficos interactivos en `Plotly`.
  4. **Ingeniería de Atributos:** Creación de variables de negocio (`es_ventana_dorada`, `es_raza_pura`, `desc_len`, `salud_completa`, `es_gratis`), imputación biológica por especie y preprocesamiento encapsulado en `ColumnTransformer` + `Pipeline`.
  5. **Modelado y Validación Cruzada:** Comparación de 3 arquitecturas (Regresión Logística, Random Forest y XGBoost) con `StratifiedKFold` (5-Fold) y balanceo de clases.
  6. **Optimización y Explicabilidad:** Ajuste de hiperparámetros con `RandomizedSearchCV` e interpretabilidad global del modelo ganador mediante valores **SHAP**.

## 🏆 Resultados del Modelo Final

El modelo seleccionado fue **Random Forest Optimizado**, evaluado sobre el conjunto de testeo (`20%` no visto):
- **ROC-AUC:** `0.7617`
- **Accuracy:** `72.76%`
- **F1-Score (Clase Riesgo):** `0.5469` | **Recall (Clase Riesgo):** `58.69%`

El análisis **SHAP** confirmó que la edad al ingreso (`Age`, `es_ventana_dorada`), la pureza racial enriquecida vía API (`es_raza_pura`), la calidad del perfil (`PhotoAmt`, `desc_len`) y las publicaciones grupales (`Quantity`) son los principales impulsores del riesgo de estancamiento.

## 🚀 Instrucciones para Evaluadores (Ejecución del Código)

Este Notebook ha sido diseñado para ser **100% reproducible** sin necesidad de configurar credenciales privadas de API.

**Mecanismo de Caché Local:**  
Al ejecutar el bloque de *Conexión a API*, el código detectará automáticamente `dataset/biologia_api_cache.csv`, omitirá las peticiones HTTP a *The Dog/Cat API* y cargará los datos biológicos directamente desde el disco local.

**Instalación de dependencias:**

```bash
python -m venv venv
source venv/bin/activate      # En Windows: venv\Scripts\activate
pip install -r requirements.txt
```

> **Nota macOS:** `xgboost` requiere OpenMP. Si al importarlo aparece un error de `libomp.dylib`, instalar el runtime con `brew install libomp`.

Para evaluar, abra el archivo `.ipynb` y ejecute todas las celdas en orden.

> **Tiempo de ejecución:** la ejecución completa tarda aproximadamente **5 minutos**, debido a la validación cruzada y a la búsqueda de hiperparámetros (`RandomizedSearchCV`) de los modelos de Machine Learning.