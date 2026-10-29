# Estadística Computacional para la Toma de Decisiones

## Online Shoppers Purchasing Intention

Proyecto desarrollado para la asignatura **MCDI501 — Estadística Computacional para la Toma de Decisiones**, del **Magíster en Ciencia de Datos e Inteligencia Artificial** de la Universidad Andrés Bello (periodo 2026-82).

El proyecto utiliza el conjunto de datos **Online Shoppers Purchasing Intention**, del UCI Machine Learning Repository, para estudiar el comportamiento de navegación de usuarios de comercio electrónico y su relación con la finalización de una compra.

---

## 1. Pregunta de investigación

> **¿Qué características del comportamiento de navegación de los usuarios se relacionan con la probabilidad de que una sesión de comercio electrónico termine en una compra?**

El alcance es descriptivo, inferencial y predictivo. Las asociaciones identificadas no se interpretan como relaciones causales.

---

## 2. Conjunto de datos

**Online Shoppers Purchasing Intention** contiene **12.330 sesiones** y **18 variables**, sin valores faltantes. Cada sesión pertenece a un usuario distinto dentro de un periodo de un año.

- **Variable objetivo:** `Revenue`, que indica si la sesión terminó en compra. Está desbalanceada: **15,47 %** de las sesiones terminan en compra.
- **Predictores:** páginas visitadas y su duración (administrativas, informativas y de producto), tasas de rebote y salida, valor de página, cercanía a fechas especiales, mes, tipo de visitante, fin de semana y características técnicas (sistema operativo, navegador, región y tipo de tráfico).

**Fuente:** Sakar, C. O., & Kastro, Y. (2018). *Online Shoppers Purchasing Intention Dataset*. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q

---

## 3. Estructura del repositorio

```text
Estadistica_Computacional/
│
├── F1/
│   └── Formativa_1.ipynb                          # EDA e inferencia (formativa)
│
├── F2/
│   └── Formativa_2_modelamiento_predictivo.ipynb  # primer modelo logístico (formativa)
│
├── S1/
│   └── 01_exploracion_inicial.ipynb               # análisis exploratorio e inferencial
│
├── S2/
│   ├── 02_simulacion_remuestreo.ipynb             # validación, simulación y remuestreo
│   └── resultados/
│       └── resultados_validados.csv               # insumo trazable para S3
│
├── S3/
│   └── S3_modelamiento_final.ipynb                # notebook maestro: modelamiento integrado
│
├── data/
│   ├── raw/
│   │   └── online_shoppers_intention.csv          # datos originales, sin modificar
│   └── processed/
│
├── docs/                                          # informes PDF y Word de cada evaluación
│
├── .gitignore
├── README.md
└── requirements.txt
```

---

## 4. Desarrollo del proyecto

### F1 — Formativa 1: EDA e inferencia

Primera aproximación al problema: comprensión del contexto, clasificación de variables, definición de la variable objetivo, estadística descriptiva e inferencia inicial.

### S1 — Sumativa 1: análisis exploratorio e inferencial

- Estadística descriptiva, distribuciones y relaciones bivariadas.
- Tasa de conversión: **15,47 %** (IC 95 %: 14,84 %–16,11 %).
- IC 95 % para las medias de `ProductRelated_Duration`, `PageValues` y `ExitRates`.
- Pruebas de hipótesis: χ² para `VisitorType × Revenue` (V de Cramér = 0,105) y Mann-Whitney para `PageValues` según `Revenue` (efecto grande, r_rb = 0,727).
- Correlaciones altas entre `BounceRates`–`ExitRates` y `ProductRelated`–`ProductRelated_Duration`.

### S2 — Sumativa 2: simulación, remuestreo y robustez

- Bootstrap no paramétrico con IC percentil y BCa (10.000 remuestras).
- Pruebas de permutación para `PageValues` y `VisitorType` (10.000 permutaciones).
- Bootstrap de correlaciones, simulación Monte Carlo, convergencia, datos sintéticos y análisis de sensibilidad.
- Robustez frente a valores extremos: media recortada, cercas IQR y jackknife.

Los resultados validados se guardan en `S2/resultados/resultados_validados.csv` como insumo para S3.

### F2 — Formativa 2: modelamiento predictivo

Ensayo del flujo de modelamiento: 12 % de faltantes MCAR controlados, imputación por mediana, partición 70/30 estratificada y un modelo de regresión logística con cinco predictores justificados con S1/S2, evaluado con matriz de confusión, métricas y curva ROC.

### S3 — Sumativa 3: modelamiento predictivo integrado

Notebook maestro: `S3/S3_modelamiento_final.ipynb`.

- **Datos faltantes:** 12 % MCAR en `ProductRelated_Duration` y `ExitRates`; comparación de eliminación, mediana e **imputación por regresión lineal múltiple** (4 predictores por variable, elegidos desde S1/S2). La regresión reduce el RMSE a menos de la mitad y preserva las correlaciones de S1.
- **Decisiones tomadas a partir de la retroalimentación de S2:**
  - filtro VIF antes de modelar: se excluye `BounceRates`;
  - `PageValues` fuera de los modelos hasta confirmar que está disponible al momento de predecir;
  - ponderación de clases (peso 3,23 para compras).
- **Tres regresiones logísticas:** variables validadas en S1/S2, stepwise por AIC y modelo reducido por BIC. Selección por validación cruzada en entrenamiento.
- **Modelo final:** AUC en prueba = 0,708; recall = 73,6 %.
- **Bootstrap** de coeficientes y odds ratios (2.000 réplicas): todos conservan su signo en ≥ 99,8 % de las réplicas.
- **Impacto de la imputación:** el modelo final ajustado con las tres estrategias llega a las mismas conclusiones.
- **Escenario de decisión:** en una campaña simulada de 1.000 sesiones, el modelo concentra 1,55 veces más compradores que una selección al azar.

**Entregables de S3:**

- Informe final integrado: [`docs/informe_sumativa3_grupo2.pdf`](docs/informe_sumativa3_grupo2.pdf)
- Notebook maestro: [`S3/S3_modelamiento_final.ipynb`](S3/S3_modelamiento_final.ipynb)
- Video de presentación (10 minutos, participan los cuatro integrantes): https://youtu.be/KRPnkCK2GlI

---

## 5. Trazabilidad del análisis

```text
S1  Explorar     descriptiva, IC, pruebas de hipótesis
 ↓
S2  Validar      bootstrap, permutación, Monte Carlo, jackknife
 ↓
S3  Modelar      imputación por regresión, regresión logística, bootstrap del modelo
 ↓
Informe final integrado + video de presentación
```

Cada fase usa los resultados de la anterior como fundamento de sus decisiones metodológicas.

---

## 6. Reproducibilidad

Los análisis se desarrollaron en **Python 3.10 o superior** con notebooks de Jupyter. Todos los procedimientos aleatorios usan la semilla:

```python
RANDOM_STATE = 42
```

Bibliotecas principales: pandas, NumPy, SciPy, statsmodels, scikit-learn, Matplotlib, Seaborn y Jupyter.

Para instalar el entorno:

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

---

## 7. Ejecución

Ejecutar los notebooks en orden metodológico. Cada uno busca los datos en `data/raw/online_shoppers_intention.csv` y puede ejecutarse desde la raíz del repositorio o desde su propia carpeta.

| Orden | Notebook |
|---|---|
| 1 | `F1/Formativa_1.ipynb` |
| 2 | `S1/01_exploracion_inicial.ipynb` |
| 3 | `S2/02_simulacion_remuestreo.ipynb` (genera `S2/resultados/resultados_validados.csv`) |
| 4 | `F2/Formativa_2_modelamiento_predictivo.ipynb` |
| 5 | `S3/S3_modelamiento_final.ipynb` |

Antes de entregar, ejecutar cada notebook con **Kernel → Restart & Run All**.

---

## 8. Principales criterios metodológicos

- Separación entre variables cuantitativas y cualitativas según su significado.
- Distinción entre asociación y causalidad.
- Análisis explícito de distribuciones asimétricas y uso de medidas robustas.
- Conservación de observaciones extremas cuando no hay evidencia de error (respaldado por el jackknife de S2).
- Evaluación de la incertidumbre con intervalos de confianza clásicos y bootstrap.
- Prevención de fuga de información: imputación y estandarización ajustadas solo con entrenamiento; exclusión de `PageValues` hasta confirmar su disponibilidad.
- Evaluación con métricas adecuadas al desbalance (recall, F1, AUC), no solo accuracy.
- Reproducibilidad mediante semillas y documentación del código.

---

## 9. Integrantes — Grupo 2

- **Verónica Durán Cisterna**
- **Raúl Moya Arriagada**
- **Daniela Rojas Vilches**
- **Manuel Sánchez Cárcamo**

**Docentes:** PhD. Jean Paul Maidana González · PhD. David Reute Zúñiga

---

## 10. Estado del proyecto

| Etapa | Estado | Notebook | Informe |
|---|---|---|---|
| F1 | Completada | `F1/Formativa_1.ipynb` | `docs/informe_formativa1_grupo2.pdf` |
| S1 | Completada | `S1/01_exploracion_inicial.ipynb` | `docs/informe_sumativa1_grupo2.pdf` |
| S2 | Completada | `S2/02_simulacion_remuestreo.ipynb` | `docs/informe_sumativa2_grupo2.pdf` |
| F2 | Completada | `F2/Formativa_2_modelamiento_predictivo.ipynb` | — (se entrega el notebook) |
| S3 | Completada | `S3/S3_modelamiento_final.ipynb` | `docs/informe_sumativa3_grupo2.pdf` · [video](https://youtu.be/KRPnkCK2GlI) |

---

**Magíster en Ciencia de Datos e Inteligencia Artificial**
**Estadística Computacional para la Toma de Decisiones**
