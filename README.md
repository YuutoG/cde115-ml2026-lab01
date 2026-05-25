# 🏆 El Oráculo del Balón - Predicción Mundial FIFA 2026 - Pulpo Pawl 2026 🐙🐙🐙

Este repositorio contiene el desarrollo integral de un pipeline predictivo de Machine Learning diseñado para proyectar las probabilidades de victoria en la Copa del Mundo de la FIFA 2026. Abordando el desafío del nuevo formato de 48 selecciones, el proyecto evita la predicción determinista de un campeón y emplea simulaciones estocásticas basadas en inferencia a nivel de partido.

## ⚙️ Arquitectura y Metodología

El sistema está construido bajo las mejores prácticas de ingeniería de datos, constando de cuatro pilares metodológicos:

1. **Ingesta y Procesamiento:** Extracción dinámica de datos estructurados (Scraping de EloRatings) y limpieza de un dataset masivo de resultados internacionales desde 1872.
2. **Ingeniería de Características (Feature Engineering):** Construcción de un motor iterativo para calcular el Rating ELO histórico, implementación de decaimiento temporal exponencial (*Time Decay*) para priorizar rendimientos recientes, y cuantificación matemática de la ventaja de localía.
3. **Modelado Predictivo:** Entrenamiento, calibración y optimización de hiperparámetros de un ensamble **XGBoost**. El modelo fue validado rigurosamente utilizando el Mundial de Qatar 2022 como conjunto de prueba, evaluado mediante métricas de probabilidad continua (*Log-Loss* y *Brier Score*).
4. **Simulación Monte Carlo:** Ejecución de 10,000 iteraciones del torneo completo, mapeando la estructura oficial de grupos y llaves eliminatorias, resultando en un Top 5 de favoritos con sus respectivos intervalos de confianza (95%).

## 📂 Estructura del Repositorio

La arquitectura del proyecto está modularizada para garantizar su reproducibilidad:

\`\`\`text
CDE115-ML2026-LAB01/
│
├── data/
│   ├── processed/                # Datasets preprocesados y listos para modelado
│   │   ├── elo_current_2026.csv
│   │   └── historical_matches_elo.csv
│   └── raw/                      # Datos crudos originales
│       └── results.csv
│
├── docs/
│   └── figuras/                  # Visualizaciones del Análisis Exploratorio (EDA)
│       ├── elo_diferencia_boxplot.png
│       └── time_decay_curve.png
│
├── models/                       # Modelos predictivos exportados (joblib/pickle)
│   └── xgb_best_model.pkl
│
├── notebooks/                    # Flujo de trabajo analítico paso a paso
│   ├── 00_fetch_data.ipynb
│   ├── 01_data_cleaning_feature_engineering.ipynb
│   ├── 02_model_training_pawl.ipynb
│   └── 03_montecarlo_simulation.ipynb
│
├── .gitignore                    # Archivos y directorios excluidos del control de versiones
├── .python-version               # Versión específica de Python utilizada
└── README.md                     # Documentación principal del proyecto
\`\`\`

## 🚀 Requisitos y Reproducibilidad

El entorno de desarrollo fue configurado para ser replicable de manera sencilla.

### Instalación de dependencias
Se recomienda la creación de un entorno virtual (`.venv`). Una vez activado, asegúrese de contar con las siguientes librerías principales instaladas:
* `pandas`
* `numpy`
* `scikit-learn`
* `xgboost`
* `matplotlib` & `seaborn`
* `tqdm`
* `selenium` & `beautifulsoup4` (Para el script de scraping)

Para instarlo en el entorno puede seguir los siguientes pasos:

1. Una vez instalado Python (recomendado Python 3.14), ejecute:
En Linux:
```python -m venv .venv```

2. Activar el entorno
```bash
source .venv/bin/activate
```

```powershell
.venv/Scripts/activate
```

3. Instalar las dependencias
```bash
pip install -r requirements.txt
```


### Ejecución
El flujo de trabajo está numerado lógicamente en la carpeta `/notebooks`. Se deben ejecutar en orden ascendente (desde el `00` hasta el `03`) para asegurar que los datos procesados y los modelos entrenados se pasen correctamente de un cuaderno a otro.

El flujo va desde la obtención de los datos, hasta la
ejecución de la simulación.

## 📊 Resultados de la Simulación (El Oráculo 2026)

Tras ejecutar **10,000 iteraciones** del torneo completo utilizando el motor de Monte Carlo y el modelo XGBoost calibrado, se obtuvieron las siguientes probabilidades de campeonato. 

Se incluye el Intervalo de Confianza (IC) del 95% para dotar de rigor estadístico a las proyecciones:

| Posición | Selección Nacional | Probabilidad | IC 95% (Margen de Error) |
| :---: | :--- | :---: | :---: |
| 🥇 | **España** | 15.44% | [14.73% - 16.15%] |
| 🥈 | **Argentina** | 10.70% | [10.09% - 11.31%] |
| 🥉 | **Inglaterra** | 9.01% | [8.45% - 9.57%] |
| 4 | **Portugal** | 6.88% | [6.38% - 7.38%] |
| 5 | **Brasil** | 6.80% | [6.31% - 7.29%] |

> **Nota Analítica:** Las probabilidades absolutas son bajas (ningún equipo supera el 20%) debido a la alta varianza que introduce el nuevo formato de 48 equipos y la ronda adicional de dieciseisavos de final. El modelo confirma matemáticamente que, en torneos de eliminación directa con esta densidad, el componente estocástico es altamente significativo.

## 👨‍💻 Autores
**Carlos David Ascencio Abarca - AA15009**
*Ingeniería en Sistemas Informáticos - Universidad de El Salvador*
**Eduardo David Rodríguez Ventura - RV15001**
*Ingeniería en Sistemas Informáticos - Universidad de El Salvador*