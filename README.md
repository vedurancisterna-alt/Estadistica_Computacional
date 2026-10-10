# Online Shoppers Purchasing Intention

Proyecto desarrollado para la asignatura **Estadística Computacional para la Toma de Decisiones (MCDI501)** del Magíster en Ciencia de Datos e Inteligencia Artificial de la Universidad Andrés Bello.

## Descripción

El proyecto utiliza el dataset **Online Shoppers Purchasing Intention**, que contiene información sobre sesiones de usuarios de un sitio de comercio electrónico.

El objetivo general es aplicar técnicas de estadística computacional para explorar y analizar los factores asociados a la intención de compra de los usuarios.

La variable objetivo del dataset es **Revenue**, que indica si una sesión terminó o no en una compra.

## Estructura del repositorio

```text
Estadistica_Computacional/
├── data/
│   ├── raw/          # Datos originales (online_shoppers_intention.csv)
│   └── processed/    # Datos procesados
├── notebooks/
│   └── 01_exploracion_inicial.ipynb   # Sumativa 1: análisis exploratorio e inferencial
├── docs/
│   ├── informe_sumativa1_grupo2.pdf   # Informe entregable de la Sumativa 1
│   └── informe_sumativa1_grupo2.docx  # Versión editable del informe
├── README.md
├── requirements.txt
└── .gitignore
```

## Evaluaciones

| Evaluación | Notebook | Informe |
| --- | --- | --- |
| Sumativa 1: Análisis exploratorio e inferencial | `notebooks/01_exploracion_inicial.ipynb` | `docs/informe_sumativa1_grupo2.pdf` |

## Puesta en marcha

Requisitos: Python 3.10 o superior.

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

El notebook puede ejecutarse desde la raíz del repositorio o desde `notebooks/`, y usa una semilla fija (`RANDOM_STATE = 42`) para que los resultados sean reproducibles.

## Integrantes (Grupo 2)

Verónica Durán, Raúl Moya, Daniela Rojas, Manuel Sánchez.
