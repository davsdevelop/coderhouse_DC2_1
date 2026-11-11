# 🐾 Modelado Predictivo y Enriquecimiento Biológico en Adopción de Mascotas

**Autor:** Diego Videla Silva

**Comisión:** 96160

**Curso:** Data Science II - Machine Learning para la Ciencia de Datos (Coderhouse)

**Entrega:** Primera Entrega (ETL, Enriquecimiento vía API y Análisis Exploratorio)

## 📌 Descripción del Proyecto

La sobrepoblación en refugios y centros de rescate animal es un desafío logístico y de bienestar crítico. Este proyecto busca identificar los predictores biológicos y visuales de la velocidad de adopción de mascotas para optimizar las estrategias de rescate, gestionar el inventario y enfocar el presupuesto de marketing de manera eficiente.

Para lograrlo, se toma un registro transaccional de un refugio (obtenido de Kaggle) y se enriquece consumiendo bases de datos genéticas internacionales (*The Dog API* & *The Cat API*).

## 🗂️ Estructura del Repositorio

El proyecto mantiene la siguiente estructura para facilitar su revisión:

```text
📁 coderhouse_DC2_1
│
├── 📁 .vscode/                              # Configuraciones del editor
├── 📁 dataset/                              # Datasets originales y caché (Kaggle y APIs)
├── 📁 Documentos/                           # Entregables formales
│   ├── Entrega1_Videla_AdopcionMascotas_Documentado.pdf                  # Informe Ejecutivo
│   └── Entrega1_Videla_AdopcionMascotas_Documentado_Presentacion.pdf     # Presentación de Slides
├── 📁 venv/                                 # Entorno virtual de Python
│
├── .env                                     # Credenciales locales (ignorado en el repo)
├── .env.template                            # Plantilla de referencia para las API Keys
├── .gitignore                               # Configuración de exclusiones de Git
├── Diccionario API.png                      # Respaldo visual del diccionario de la API
├── Diccionario Columnas.png                 # Respaldo visual del diccionario del dataset base
├── Entrega1_Videla_AdopcionMascotas.ipynb   # Jupyter Notebook con el código fuente (ETL y EDA)
└── README.md                                # Documentación principal del repositorio
```

## 🛠️ Tecnologías y Metodología Implementada

* **Lenguaje:** Python 3
* **Librerías:** `pandas`, `requests`, `matplotlib`, `seaborn`, `difflib`, `python-dotenv`.
* **Metodología:**
  1. **Ingesta y ETL:** Carga de datos locales y consumo de APIs REST.
  2. **Data Wrangling & IA:** Limpieza sintáctica y semántica usando *Fuzzy String Matching* (`difflib`) validado mediante inteligencia artificial (LLM) bajo criterios clínicos veterinarios.
  3. **Arquitectura:** Bifurcación en Data Marts (`df_final_full` y `df_final_razas`) para asegurar el rigor estadístico al separar animales mestizos de razas puras.
  4. **EDA (Exploratory Data Analysis):** Comprobación de 4 hipótesis de negocio orientadas a la logística del refugio.

## 🚀 Instrucciones para Evaluadores (Ejecución del Código)

Este Jupyter Notebook ha sido diseñado para ser **100% reproducible** sin necesidad de configurar variables de entorno (como se ve en el `.env.template`) ni gestionar credenciales privadas de la API.

**Mecanismo de Caché Local:**
Al ejecutar el bloque de *Conexión a API* en el Notebook (`Entrega1_Videla_AdopcionMascotas.ipynb`), el código detectará automáticamente la existencia del archivo de caché dentro de la carpeta `dataset/`. Al encontrarlo, omitirá la petición HTTP a las APIs de perros y gatos, y cargará la tabla maestra biológica directamente desde el disco local.

Para evaluar, simplemente abra el archivo `.ipynb` y ejecute todas las celdas en orden.