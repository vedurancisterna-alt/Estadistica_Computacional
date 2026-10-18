# Estadística Computacional para la Toma de Decisiones

## Online Shoppers Purchasing Intention

Proyecto desarrollado para la asignatura **Estadística Computacional para la Toma de Decisiones**, del **Magíster en Ciencia de Datos e Inteligencia Artificial**.

El proyecto utiliza el conjunto de datos **Online Shoppers Purchasing Intention**, disponible en el UCI Machine Learning Repository, para estudiar el comportamiento de navegación de usuarios de comercio electrónico y su relación con la finalización de una compra.

---

## 1. Pregunta de investigación

> **¿Qué características del comportamiento de navegación de los usuarios se relacionan con la probabilidad de que una sesión de comercio electrónico termine en una compra?**

El análisis tiene un alcance principalmente descriptivo e inferencial. Las asociaciones identificadas no se interpretan como relaciones causales.

---

## 2. Conjunto de datos

El conjunto de datos **Online Shoppers Purchasing Intention** contiene información de **12.330 sesiones** de navegación en un sitio de comercio electrónico.

La variable objetivo es:

- **Revenue**: indica si la sesión terminó o no en una compra.

El conjunto incluye variables asociadas a:

- cantidad de páginas visitadas;
- duración de las visitas;
- métricas de navegación;
- tasas de rebote y salida;
- valor de las páginas;
- características temporales de la sesión;
- tipo de visitante;
- sistema operativo, navegador y región;
- tráfico y comportamiento durante fines de semana.

Fuente:

**UCI Machine Learning Repository — Online Shoppers Purchasing Intention Dataset**

---

## 3. Estructura del repositorio

```text
Estadistica_Computacional/
│
├── F1/
│   └── Formativa_1.ipynb
│
├── F2/
│   └── 01_exploracion_inicial.ipynb
│
├── S1/
│   ├── 01_exploracion_inicial.ipynb
│   ├── informe_sumativa1_grupo2.docx
│   └── informe_sumativa1_grupo2.pdf
│
├── S2/
│   ├── 02_simulacion_remuestreo.ipynb
│   └── resultados/
│       └── resultados_validados.csv
│
├── data/
│   ├── raw/
│   │   └── online_shoppers_intention.csv
│   └── processed/
│
├── docs/
│
├── .gitignore
├── README.md
└── requirements.txt
```

---

## 4. Desarrollo del proyecto

### F1 — Definición y comprensión

Primera aproximación al problema de investigación y al conjunto de datos.

Se aborda:

- comprensión del problema;
- identificación del contexto;
- clasificación de variables;
- definición de la variable objetivo;
- formulación inicial de la pregunta de investigación.

### F2 — Estadística descriptiva

Exploración inicial del conjunto de datos mediante herramientas de estadística descriptiva.

Incluye:

- revisión de estructura y calidad de los datos;
- análisis de variables numéricas y categóricas;
- medidas de tendencia central y dispersión;
- distribuciones;
- visualizaciones;
- relaciones bivariadas;
- correlaciones.

### S1 — Estadística descriptiva e inferencial

La **Sumativa 1** profundiza el análisis mediante procedimientos descriptivos e inferenciales.

Incluye:

- análisis exploratorio de datos;
- estimación puntual;
- intervalos de confianza;
- análisis de correlaciones;
- pruebas de hipótesis;
- interpretación estadística contextualizada.

Entre los análisis realizados se consideran variables como:

- `ProductRelated_Duration`;
- `PageValues`;
- `ExitRates`;
- `VisitorType`;
- `Revenue`.

Los resultados obtenidos en esta etapa constituyen la base empírica para las simulaciones y procedimientos de remuestreo desarrollados posteriormente.

### S2 — Simulación y remuestreo

La **Sumativa 2** utiliza herramientas de estadística computacional para evaluar la estabilidad y robustez de los resultados obtenidos en S1.

Se implementan:

- **Bootstrap no paramétrico**;
- intervalos de confianza percentiles y **BCa**;
- **pruebas de permutación**;
- bootstrap de correlaciones;
- simulación **Monte Carlo**;
- evaluación de convergencia;
- generación de datos sintéticos;
- análisis de sensibilidad;
- análisis de robustez;
- **jackknife**.

Las simulaciones utilizan al menos **10.000 iteraciones o remuestras**, según corresponda.

Los principales resultados validados se almacenan en:

```text
S2/resultados/resultados_validados.csv
```

Este archivo permite conservar la trazabilidad de los resultados que servirán como insumo para las siguientes etapas del proyecto.

---

## 5. Trazabilidad del análisis

El proyecto mantiene una secuencia metodológica acumulativa:

```text
F1
Definición y comprensión
        ↓
F2
Estadística descriptiva
        ↓
S1
Estimación e inferencia
        ↓
S2
Simulación, remuestreo y robustez
        ↓
S3
Etapa posterior del proyecto
```

S2 no reemplaza los resultados obtenidos en S1, sino que los utiliza como punto de partida para evaluar su estabilidad mediante herramientas computacionales.

---

## 6. Reproducibilidad

Los análisis fueron desarrollados en **Python** mediante notebooks de Jupyter.

Se utiliza una semilla global para favorecer la reproducibilidad de los procedimientos aleatorios:

```python
SEED = 42
```

Las principales bibliotecas utilizadas son:

- pandas
- NumPy
- SciPy
- Matplotlib
- Seaborn
- Jupyter

Las dependencias del proyecto se encuentran documentadas en:

```text
requirements.txt
```

Para instalar el entorno:

```bash
pip install -r requirements.txt
```

---

## 7. Ejecución

Los notebooks principales del proyecto se encuentran en:

```text
F1/
F2/
S1/
S2/
```

Para reproducir los análisis se recomienda ejecutar los notebooks siguiendo el orden metodológico del proyecto.

El conjunto de datos original se encuentra en:

```text
data/raw/online_shoppers_intention.csv
```

---

## 8. Principales criterios metodológicos

Durante el desarrollo se mantienen los siguientes criterios:

- separación entre variables cuantitativas y cualitativas;
- interpretación contextual de los resultados;
- distinción entre asociación y causalidad;
- análisis explícito de distribuciones asimétricas;
- conservación de observaciones extremas cuando no existe evidencia suficiente para considerarlas errores;
- evaluación de incertidumbre mediante intervalos de confianza;
- validación computacional mediante remuestreo y simulación;
- evaluación de estabilidad y sensibilidad de los resultados;
- reproducibilidad mediante semillas aleatorias y documentación del código.

---

## 9. Integrantes — Grupo 2

- **Verónica Durán Cisterna**
- **Raúl Moya Arriagada**
- **Daniela Rojas Vilches**
- **Manuel Sánchez Cárcamo**

---

## 10. Estado del proyecto

| Etapa | Estado | Principal entregable |
|---|---|---|
| F1 | Completada | `F1/Formativa_1.ipynb` |
| F2 | Completada | `F2/01_exploracion_inicial.ipynb` |
| S1 | Completada | `S1/01_exploracion_inicial.ipynb` |
| S2 | En desarrollo | `S2/02_simulacion_remuestreo.ipynb` |

---

**Magíster en Ciencia de Datos e Inteligencia Artificial**  
**Estadística Computacional para la Toma de Decisiones**
