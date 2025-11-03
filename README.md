# TPF - Predicción de Consumo Energético Industrial

Este repositorio contiene el Trabajo Práctico Final para la materia "Laboratorio de Datos II", enfocado en crear un pipeline de MLOps completo para predecir el consumo energético de una planta cervecera.

## 🎯 Objetivo del Proyecto

El objetivo es desarrollar un pipeline de machine learning reproducible para predecir el consumo energético diario (kW) del sistema de refrigeración (`Frio (kW)`) del día siguiente. El proyecto se enfoca en buenas prácticas de MLOps, control de versiones (Git), versionado de datos (LFS, checksums) y seguimiento de experimentos.

## 📂 Estructura del Repositorio

El proyecto sigue una estructura estándar para proyectos de Machine Learning:

tp_final/
├── .git/
├── .gitattributes         # Configuración de Git LFS
├── .gitignore             # Archivos ignorados por Git
├── data/                  # Datos brutos, procesados e intermedios
│   ├── Totalizadores*.xlsx  # Datos brutos (manejados por Git LFS)
│   ├── dataset_unificado.csv
│   ├── dataset_preprocesamiento.csv
│   └── checksums.json     # Checksums para versionado de datos
├── models/                # Modelos entrenados y serializados
│   ├── modelo_v1.0.0.pkl  # (Manejado por Git LFS)
│   └── model_registry.json
├── notebooks/             # Notebooks de exploración, prototipado y borradores
│   ├── eda.ipynb
│   ├── preprocesamiento.ipynb
│   └── modelado.ipynb
├── results/               # Resultados finales
│   ├── predicciones.csv
│   └── experiment_logs.csv
├── src/                   # Scripts de código fuente (Python)
│   ├── __init__.py
│   ├── preprocessing_pipeline.py
│   ├── train_model.py
│   ├── predict.py
│   └── tools.py           # Funciones auxiliares
└── requirements.txt       # Lista de dependencias del proyecto

---

## 🚀 Guía de Instalación y Ejecución

Sigue estos pasos para clonar y ejecutar el proyecto en tu máquina local.

### Paso 1: Clonar el Repositorio

**¡IMPORTANTE!** Este proyecto usa **Git LFS** (Large File Storage) para manejar los archivos pesados (como los `.xlsx` y `.pkl`).

1.  **Instala Git LFS** en tu computadora (si no lo tienes). Puedes descargarlo desde [git-lfs.github.com](https://git-lfs.github.com).
2.  Clona el repositorio. El comando `git clone` descargará automáticamente los archivos de LFS.

    ```bash
    git clone [https://github.com/Angiii12/TPF_Consumo_Energetico.git](https://github.com/Angiii12/TPF_Consumo_Energetico.git)
    ```
3.  Entra a la carpeta del proyecto:
    ```bash
    cd TPF_Consumo_Energetico
    ```

### Paso 2: Configurar el Entorno Virtual (Conda)

Para asegurar la reproducibilidad, el proyecto usa un entorno de Conda específico (`cervecera_env`) y un archivo `requirements.txt`[cite: 26, 40].

1.  **Crea el entorno de Conda** (asegúrate de tener Anaconda o Miniconda instalado)[cite: 29]:
    ```bash
    conda create -n cervecera_env python=3.12
    ```
2.  **Activa el entorno:** [cite: 30]
    ```bash
    conda activate cervecera_env
    ```
3.  **Instala todas las dependencias** listadas en `requirements.txt`[cite: 224]:
    ```bash
    pip install -r requirements.txt
    ```

¡Listo! Ya tienes el entorno configurado con las mismas librerías y versiones usadas en el proyecto.

### Paso 3: Ejecutar los Scripts Principales

El pipeline se ejecuta secuencialmente. Debes ejecutar los scripts desde la carpeta raíz del proyecto (`TPF_Consumo_Energetico/`).

1.  **(Opcional) Ejecutar Preprocesamiento:**
    (Este script se usa para generar los datos limpios que usará el entrenamiento) [cite: 120].
    ```bash
    python src/preprocessing_pipeline.py
    ```

2.  **(Opcional) Entrenar el Modelo:**
    (Este script entrena el modelo usando los datos procesados y lo guarda en la carpeta `models/`) [cite: 146].
    ```bash
    python src/train_model.py
    ```

3.  **Ejecutar Predicciones (Script Principal):**
    Este es el script final[cite: 153]. Carga el último modelo entrenado desde `models/` y genera predicciones sobre un archivo de datos nuevos[cite: 212, 213].

    Debes pasarle como argumento la ruta al archivo Excel con los datos nuevos (usando uno de los de prueba como ejemplo):

    ```bash
    python src/predict.py "data/Totalizadores Planta de Cerveza 2021 2022.xlsx"
    ```

    Tras ejecutarse, verás un mensaje de éxito y encontrarás el archivo `predicciones.csv` en la carpeta `results/`[cite: 209, 210].