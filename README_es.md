# 🔬 Análisis Estadístico Avanzado de Datos Oncológicos

[![R](https://img.shields.io/badge/Lenguaje-R-276DC3?logo=r&logoColor=white)](https://www.r-project.org/)
[![Estado](https://img.shields.io/badge/Estado-Completado-success)]()
[![Asignatura](https://img.shields.io/badge/Asignatura-Estad%C3%ADstica%20Avanzada-blueviolet)]()
[![Universidad](https://img.shields.io/badge/Universidad-Universidad%20de%20Deusto-red)]()

> **Selección de Idioma / Language Selection:**  
> 🇪🇸 **Castellano** | [🇬🇧 Read in English (English Version)](README.md)

---

## 📌 Tabla de Contenidos
- [Descripción General y Objetivos](#-descripción-general-y-objetivos)
- [Autores y Contexto Académico](#-autores-y-contexto-académico)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Descripción de los Conjuntos de Datos](#-descripción-de-los-conjuntos-de-datos)
- [Módulos Metodológicos](#-módulos-metodológicos)
  - [1. Análisis Exploratorio y Estadística Descriptiva](#1-análisis-exploratorio-y-estadística-descriptiva)
  - [2. Regresión Lineal Múltiple](#2-regresión-lineal-múltiple)
  - [3. Regresión Logística Binaria](#3-regresión-logística-binaria)
  - [4. Análisis de Componentes Principales (PCA)](#4-análisis-de-componentes-principales-pca)
  - [5. Análisis de Correspondencias (CA)](#5-análisis-de-correspondencias-ca)
  - [6. Agrupamiento No Supervisado: K-Means](#6-agrupamiento-no-supervisado-k-means)
  - [7. Agrupamiento Jerárquico Aglomerativo (HAA)](#7-agrupamiento-jerárquico-aglomerativo-haa)
  - [8. Discusión Comparativa de Métodos de Clustering](#8-discusión-comparativa-de-métodos-de-clustering)
- [Principales Hallazgos e Implicaciones Clínicas](#-principales-hallazgos-e-implicaciones-clínicas)
- [Tecnologías y Librerías de R](#-tecnologías-y-librerías-de-r)
- [Guía de Reproducibilidad y Ejecución](#-guía-de-reproducibilidad-y-ejecución)

---

## 🔬 Descripción General y Objetivos

Este repositorio alberga un proyecto integral de investigación estadística centrado en el análisis multivariante y el modelado predictivo de datos oncológicos. Desarrollado en el marco de la asignatura de **Estadística Avanzada** en la **Universidad de Deusto**, el propósito central de este estudio es aplicar rigurosas técnicas estadísticas (paramétricas y no paramétricas) a conjuntos de datos biomédicos reales y sintéticos—principalmente **Cáncer de Mama** (*Breast Cancer*) y **Cáncer de Próstata** (*Prostate Cancer*), complementados por el análisis exploratorio de un dataset clínico de **Cáncer de Pulmón** (*Lung Cancer*).

El trabajo responde a las siguientes preguntas fundamentales de investigación:
1. **Caracterización Morfológica:** ¿Cómo difieren las características geométricas y texturales de los núcleos celulares (radio, perímetro, área, concavidad, compacidad, textura) entre lesiones benignas y malignas?
2. **Modelado Predictivo:**
   - ¿Es posible formular modelos de regresión lineal robustos para predecir dimensiones tumorales controlando la multicolinealidad severa?
   - ¿Con qué precisión y sensibilidad puede un modelo logístico clasificar la malignidad de un tumor basándose en variables citológicas?
3. **Reducción de Dimensionalidad:** ¿Se puede comprimir un espacio de alta dimensión (ej. 30 variables procedentes de biopsia por aspiración con aguja fina) mediante Análisis de Componentes Principales (PCA) reteniendo la mayor parte de la varianza diagnóstica?
4. **Asociación Categórica:** ¿Qué dependencias no lineales existen entre atributos morfológicos discretizados mediante Análisis de Correspondencias (CA)?
5. **Agrupamiento Fenotípico:** ¿Son capaces los algoritmos de clustering no supervisado (K-Means y Agrupamiento Jerárquico Aglomerativo) de descubrir subgrupos latentes de tumores tanto en el espacio original como en el espacio reducido por PCA?

---

## 👥 Autores y Contexto Académico

- **Iker Ibarrola**
- **Enetz Quindimil**
- **Carlos Firvida**
- **Iñigo Infante**

*Institución:* **Universidad de Deusto**  
*Grado:* Ingeniería Informática / Ciencia de Datos  
*Asignatura:* Estadística Avanzada (2.º Curso, 2.º Semestre)

---

## 📁 Estructura del Repositorio

```plaintext
cancerResearch/
│
├── README.md                                    # Documentación principal del proyecto (Inglés)
├── README_es.md                                 # Documentación completa del proyecto (Castellano)
│
├── breast_cancer_data.csv                       # Dataset Wisconsin Diagnostic Breast Cancer (WDBC)
├── Prostate_Cancer.csv                          # Dataset clínico de cáncer de próstata
├── lung_cancer_data.csv                         # Dataset clínico-sintético de cáncer de pulmón
│
├── DiscussionOfClusteringResults_breast_cancer.R   # Comparación y síntesis K-Means vs HCA (Mama)
├── DiscussionOfClusteringResults_prostate_cancer.R # Comparación y síntesis K-Means vs HCA (Próstata)
│
├── DESCRIPTIVE_ANALYSIS/                         # Análisis Exploratorio de Datos (EDA)
│   ├── descriptive_analysis_breast_cancer.R      # Distribución, correlaciones y gráficos (Mama)
│   ├── descriptive_analysis_prostate_cancer.R    # Estadísticos y correlaciones (Próstata)
│   └── descriptive_analysis_lung_cancer.R        # Demografía, clínica y laboratorio (Pulmón)
│
├── LINEAR_REGRESSION/                            # Regresión Lineal Múltiple
│   ├── linear_regression_breast_cancer.R         # Modelo de Radio Medio, eliminación hacia atrás y diagnóstico
│   ├── linear_regression_prostate_cancer.r       # Modelo de Compacidad, ANOVA e intervalos de predicción
│   └── other_LRmodels_breast_cancer.R            # Modelos de Perímetro/Área y comparativa con 21 variables
│
├── LOGISTIC_REGRESSION/                          # Modelado de Clasificación Binaria
│   ├── logistic_regression_breast_cancer.R       # Clasificación del diagnóstico, matriz Caret y ROC/AUC
│   └── logistic_regression_prostate_cancer.R     # Selección de predictores, curvas sigmoides y umbral óptimo
│
├── PCA/                                          # Análisis de Componentes Principales
│   ├── PCA_breast_cancer.R                       # Comparativa dual (30 variables vs 10 medias), biplots
│   └── PCA_prostate_cancer.R                     # PCA escalado, dualidad y vectores paciente-variable
│
├── CA/                                           # Análisis de Correspondencias
│   ├── CA_breast_cancer.R                        # Discretización por cuartiles, test Chi-cuadrado y mapa 2D
│   ├── CA_prostate_cancer.R                      # Discretización por desviación típica y perfiles fila/columna
│   └── TEST_CA_Multiple_variable_combination.R   # Experimento de discretización con 3 variables
│
├── K-MEANS/                                      # Clustering No Supervisado con K-Means
│   ├── K-means_breast_cancer.R                   # Codo/Silueta, K=15, PCA vs Original, mapas de calor
│   └── K-Means_prostate_cancer.R                 # K=3 clusters, correlación variable-cluster
│
└── HAA/                                          # Agrupamiento Jerárquico Aglomerativo
    ├── HAA_Breast_Cancer.R                       # Enlace completo, dendrogramas y perfiles de clúster
    └── HAA_prostate_cancer.r                     # Enlace completo, cortes en altura/k y mapas de calor
```

---

## 📊 Descripción de los Conjuntos de Datos

### 1. Cáncer de Mama de Wisconsin (WDBC) (`breast_cancer_data.csv`)
- **Observaciones:** 569 pacientes (357 Benignos, 212 Malignos).
- **Atributos:** 32 variables:
  - `id`: Identificador numérico del paciente (descartado durante el preprocesamiento).
  - `diagnosis`: Diagnóstico anatomopatológico (`B` = Benigno, `M` = Maligno).
  - 30 variables continuas calculadas a partir de imágenes digitalizadas de biopsias por aspiración con aguja fina (FNA), que describen 10 propiedades morfológicas de los núcleos celulares, cada una registrada en tres estadísticas:
    - **Media** (`_mean`): Tendencia central de las mediciones nucleares.
    - **Error Estándar** (`_se`): Variabilidad e incertidumbre de la medida.
    - **Peor / Mayor** (`_worst`): Media de los tres valores más grandes por imagen.
  - **Propiedades Morfológicas:** Radio (`radius`), Textura (`texture`), Perímetro (`perimeter`), Área (`area`), Suavidad (`smoothness`), Compacidad (`compactness`), Concavidad (`concavity`), Puntos Cóncavos (`concave points`), Simetría (`symmetry`) y Dimensión Fractal (`fractal dimension`).
- **Calidad de los Datos:** Sin valores faltantes (`NA`). Se constató que un ~2% de las muestras presentan `concavity_mean = 0`, lo cual corresponde a células benignas sin invaginaciones medibles.

### 2. Cáncer de Próstata (`Prostate_Cancer.csv`)
- **Observaciones:** 100 registros clínicos (62 Malignos, 38 Benignos).
- **Atributos:** 10 columnas:
  - `id`: Identificador del paciente.
  - `diagnosis_result`: Diagnóstico clínico (`M` / `B`).
  - 8 métricas nucleares cuantitativas: `radius`, `texture`, `perimeter`, `area`, `smoothness`, `compactness`, `symmetry` y `fractal_dimension`.
- **Calidad:** Mediciones numéricas limpias, sin valores ausentes.

### 3. Cáncer de Pulmón (`lung_cancer_data.csv`)
- **Observaciones:** 23.658 registros de pacientes.
- **Atributos:** 38 variables clínicas, epidemiológicas y analíticas:
  - Factores sociodemográficos: Edad, Género, Etnia, Tipo de Seguro.
  - Hábitos e Historia: Historial de Tabaquismo, Paquetes-Año, Antecedentes Familiares.
  - Estadio y Tratamiento: Tamaño del Tumor (mm), Localización, Estadio (I–IV), Modalidad de Tratamiento, Meses de Supervivencia.
  - Comorbilidades: Diabetes, Hipertensión, Enfermedad Cardíaca, Enfermedad Pulmonar Crónica, Enfermedad Renal, Enfermedad Autoinmune.
  - Analítica Sanguínea: Presión Arterial, Hemoglobina, Leucocitos, Plaquetas, Albúmina, Fosfatasa Alcalina, Transaminasas (ALT, AST), Creatinina, LDH, Calcio, Potasio, Glucosa.
- **Función en el Proyecto:** Banco de pruebas a gran escala para análisis exploratorio multivariante y tablas de contingencia clínica.

---

## 🔬 Módulos Metodológicos

### 1. Análisis Exploratorio y Estadística Descriptiva
*Directorio: [`DESCRIPTIVE_ANALYSIS/`](DESCRIPTIVE_ANALYSIS/)*

- **Limpieza y Preparación:** Eliminación de identificadores arbitrarios (`id`, `Patient_ID`), conversión de diagnósticos a factores descriptivos (`benign`, `malign`) y verificación de integridad (`colSums(is.na(data))`).
- **Resumen Numérico:** Estimación de estadísticos paramétricos y no paramétricos con `summary()` y `pastecs::stat.desc()` (media, mediana, desviación típica, varianza, rango intercuartílico IQR y cuantiles).
- **Estudio de Colinealidad:** Las matrices de correlación de Pearson demostraron colinealidad casi perfecta entre las métricas de tamaño:
  - $\text{cor}(\text{radius\_mean}, \text{perimeter\_mean}) > 0.99$
  - $\text{cor}(\text{radius\_mean}, \text{area\_mean}) > 0.98$
  - $\text{cor}(\text{perimeter\_mean}, \text{area\_mean}) > 0.98$
  - Alta correlación ($> 0.85$) entre la versión `mean` y `worst` de cada parámetro.
- **Exploración Gráfica:** Diagramas de cajas (*boxplots*), gráficos de violín y gráficos de dispersión estratificados con `ggplot2` y `lattice`, evidenciando la marcada separación entre tumores benignos y malignos según su tamaño.
- **Evaluación de Normalidad:** Los gráficos Q-Q normales (`car::qqPlot`) y el cálculo de asimetría (*skewness*) indicaron desviaciones de la normalidad en las variables brutas, justificando análisis multivariantes más avanzados.

---

### 2. Regresión Lineal Múltiple
*Directorio: [`LINEAR_REGRESSION/`](LINEAR_REGRESSION/)*

#### Modelos de Cáncer de Mama ([`linear_regression_breast_cancer.R`](LINEAR_REGRESSION/linear_regression_breast_cancer.R))
- **Selección de la Respuesta:** Se escogió `radius_mean` tras verificar mediante ANOVA que discrimina significativamente el diagnóstico tumoral ($p = 8.47 \times 10^{-96}$).
- **Filtrado de Predictores:** Se descartaron variables redundantes (perímetro, área, métricas `_worst` y versiones `_se` fuertemente correlacionadas) para evitar inflación de varianza (multicolinealidad).
- **Eliminación Hacia Atrás (*Backward Elimination*):** A partir del modelo con variables admisibles y con un nivel $\alpha = 0.05$, se eliminaron secuencialmente las variables no significativas (`symmetry_se` $\rightarrow$ `texture_se` $\rightarrow$ `texture_mean`).
- **Modelo Final Seleccionado:**
  $$\text{radius\_mean} \sim \text{smoothness\_mean} + \text{compactness\_mean} + \text{concave.points\_mean} + \text{symmetry\_mean} + \text{fractal\_dimension\_mean} + \text{smoothness\_se}$$
- **Contraste de Hipótesis:**
  - Test $F$ global de significación: $p < 2.2 \times 10^{-16}$.
  - Test ANOVA para modelos anidados: Demostró que el modelo simplificado no pierde capacidad explicativa frente al modelo extendido ($p > 0.05$).
- **Diagnóstico del Modelo:**
  - Residuos vs. Valores Ajustados: Confirmaron linealidad y homocedasticidad.
  - Gráfico Q-Q y coeficiente de asimetría ($0.328$): Verificaron residuos aproximadamente normales y casi simétricos.
  - Distancia de Cook: Se detectó la observación `214` como punto de alto apalancamiento (*leverage*). Al reajustar el modelo sin dicho punto, los coeficientes y el $R^2$ ajustado permanecieron prácticamente invariables, probando la estabilidad del modelo.
- **Validación por Intervalos:**
  - Intervalos de confianza al 99% (datos de entrenamiento): Cobertura de ~20% debido a la estrechez del intervalo de la media estimada.
  - Intervalos de predicción al 95% (conjunto independiente de prueba del 20%): **>90% de observaciones predichas dentro de los límites**.

#### Modelos Lineales Alternativos ([`other_LRmodels_breast_cancer.R`](LINEAR_REGRESSION/other_LRmodels_breast_cancer.R))
- Se formularon modelos para predecir `area_mean`, `perimeter_mean` y un modelo partiendo de 21 predictores.
- Los resultados de cobertura en el conjunto de prueba fueron equivalentes (>90-93% dentro del intervalo de predicción), ratificando la coherencia geométrica de las variables nucleares.

#### Modelo de Cáncer de Próstata ([`linear_regression_prostate_cancer.r`](LINEAR_REGRESSION/linear_regression_prostate_cancer.r))
- Variable respuesta: `compactness` (ANOVA $p = 5.10 \times 10^{-8}$ según diagnóstico).
- La eliminación hacia atrás seleccionó: `perimeter`, `area`, `symmetry` y `fractal_dimension`.
- Cobertura de intervalos de predicción en test: **100% de acierto**.

---

### 3. Regresión Logística Binaria
*Directorio: [`LOGISTIC_REGRESSION/`](LOGISTIC_REGRESSION/)*

#### Clasificación en Cáncer de Mama ([`logistic_regression_breast_cancer.R`](LOGISTIC_REGRESSION/logistic_regression_breast_cancer.R))
- **Objetivo:** Predecir la probabilidad de que una lesión sea maligna ($1$) o benigna ($0$).
- **Inspección Visual de Predictores:** Diagramas de violín demostraron qué variables separan con mayor nitidez las clases (`radius_mean`, `compactness_mean`, `concavity_mean`).
- **Ajuste GLM (Binomial - Logit):** Tras depurar colinealidades y coeficientes no significativos, el modelo óptimo quedó formulado como:
  $$\text{logit}(P(\text{malign})) = \beta_0 + \beta_1(\text{texture\_mean}) + \beta_2(\text{compactness\_mean}) + \beta_3(\text{concave.points\_mean}) + \beta_4(\text{radius\_mean})$$
- **Rendimiento de Clasificación (Punto de Corte = 0.5):**
  - **Exactitud (*Accuracy*):** **94.38%**
  - **Sensibilidad (*Recall* de Malignos):** **96.64%**
  - **Especificidad:** Elevada capacidad para descartar benignos.
  - **Curva ROC y AUC:** Calculada mediante `pROC::roc()`, alcanzando un AUC cercano a 0.98, demostrando una excelente discriminación diagnóstica.

#### Clasificación en Cáncer de Próstata ([`logistic_regression_prostate_cancer.R`](LOGISTIC_REGRESSION/logistic_regression_prostate_cancer.R))
- Superposición de curvas logísticas univariantes sobre diagramas de dispersión, ilustrando la bondad de ajuste de variables como `perimeter` y `compactness` frente a `radius`.
- Selección por pasos reteniendo `compactness` y `fractal_dimension`.
- Análisis de la curva de intercambio entre sensibilidad y especificidad para localizar el umbral de corte óptimo.

---

### 4. Análisis de Componentes Principales (PCA)
*Directorio: [`PCA/`](PCA/)*

#### Estudio Comparativo en Cáncer de Mama ([`PCA_breast_cancer.R`](PCA/PCA_breast_cancer.R))
- **Diseño Dual:** Para evaluar el impacto de variables redundantes, se ajustaron y compararon dos modelos PCA con `FactoMineR::PCA(scale.unit = TRUE)`:
  1. **Modelo Completo (30 variables):** Medias, errores estándar y valores peores.
  2. **Modelo de Medias (10 variables):** Únicamente las medias de cada propiedad.
- **Selección de Componentes y Gráficos Scree:**
  - Criterio de Kaiser ($\lambda > 1$): 6 componentes en el modelo completo; 2 en el modelo de medias.
  - Regla del Codo (*Elbow Rule*): En ambos casos, el punto de inflexión se localiza en la Componente 3.
  - Las dos primeras componentes recogen el **63%** de la varianza en el modelo completo y cerca del **80%** en el modelo de medias.
- **Círculo de Correlaciones y Factores:**
  - **PC1:** Altamente correlacionada de forma positiva ($r > 0.80$) con variables morfológicas de tamaño y forma (`radius_mean`, `perimeter_mean`, `area_mean`, `compactness_mean`, `concavity_mean`, `concave.points_mean`).
  - **PC2:** Dominada principalmente por la dimensión fractal (`fractal_dimension_mean`, $r \approx 0.90$) y aspectos de textura.
- **Calidad de Representación ($\cos^2$) y Contribuciones ($\text{contrib}$):** Confirmaron proyecciones sólidas en la periferia del círculo de correlación.
- **Proyección Clínica y Diagnóstico:**
  - La visualización de individuos coloreados por diagnóstico evidenció una nítida separación sobre el **eje PC1**: los casos benignos se concentran en valores negativos de PC1, mientras que los malignos se desplazan a valores positivos.
  - Validación con ANOVA sobre las coordenadas de PC1: $F$-test $p = 3.13 \times 10^{-120}$.

#### PCA en Cáncer de Próstata ([`PCA_prostate_cancer.R`](PCA/PCA_prostate_cancer.R))
- Reducción de 8 variables continuas a 2 componentes principales que explican el **62.93%** de la varianza.
- Gráficos de biplot y dualidad analizando la relación geométrica entre los pacientes individuales y los vectores de las variables.

---

### 5. Análisis de Correspondencias (CA)
*Directorio: [`CA/`](CA/)*

Mientras el PCA opera sobre espacios euclídeos continuos, el Análisis de Correspondencias examina asociaciones en tablas de contingencia construidas a partir de variables discretizadas.

#### Cáncer de Mama ([`CA_breast_cancer.R`](CA/CA_breast_cancer.R))
- **Discretización:** Transformación de variables continuas en 4 categorías ordinales por cuartiles (*muy bajo*, *bajo*, *alto*, *muy alto*):
  - `radius_mean_cat` (tamaño del tumor).
  - `smoothness_mean_cat` (textura / suavidad superficial).
- **Tablas de Contingencia y Valores Esperados:**
  - Fuerte atracción positiva entre `radio muy alto` y `suavidad muy alta` (observados = 45 vs. esperados = 35.44).
  - Clara repulsión negativa entre `radio muy alto` y `suavidad muy baja` (observados = 17 vs. esperados = 35.69).
- **Test de Independencia:** La prueba de $\chi^2$ de Pearson arrojó un p-valor $< 0.05$, rechazando rotundamente la hipótesis de independencia.
- **Mapa Factorial 2D:** Representación conjunta de perfiles fila y columna visualizando la cercanía entre perfiles morfológicos.

#### Cáncer de Próstata ([`CA_prostate_cancer.R`](CA/CA_prostate_cancer.R) y [`TEST_CA_Multiple_variable_combination.R`](CA/TEST_CA_Multiple_variable_combination.R))
- Discretización basada en desviaciones estándar ($< \mu - \sigma$, $[\mu - \sigma, \mu + \sigma]$, $> \mu + \sigma$) en niveles *bajo*, *normal* y *alto*.
- Cálculo de perfiles fila/columna, residuos de Pearson e inercia total explicada.

---

### 6. Agrupamiento No Supervisado: K-Means
*Directorio: [`K-MEANS/`](K-MEANS/)*

#### K-Means en Cáncer de Mama ([`K-means_breast_cancer.R`](K-MEANS/K-means_breast_cancer.R))
- **Enfoque en Espacio Dual:** Se ejecutó K-Means tanto directamente sobre las variables originales estandarizadas como sobre las coordenadas reducidas de PCA (PC1–PC2).
- **Selección del Número de Clústeres:**
  - Barrido para $k \in [1, 50]$ con `nstart = 10`.
  - Análisis de curvas de suma de cuadrados intra-clúster (WCSS) y silueta; se determinó $k = 15$ para capturar subgrupos histológicos detallados.
- **Matriz de Confusión Cruzada (Heatmap):** Se generó un mapa de calor cruzando las asignaciones de clústeres entre el espacio original y el espacio PCA. Múltiples clústeres demostraron correspondencias biunívocas exactas (ej. Clúster 6 Original $\equiv$ Clúster 5 PCA; Clúster 3 Original $\equiv$ Clúster 4 PCA), confirmando que PCA retiene la topología y relaciones de vecindad de los datos.
- **Caracterización Fenotípica:**
  - Gráficos de violín facetados con paleta `scico::lajolla` detallando el perfil de cada variable por clúster.
  - Proyección del diagnóstico clínico sobre los clústeres en el plano PCA:
    - **5 clústeres puramente malignos** (alto radio, alta concavidad, PC1 positivo).
    - **6 clústeres puramente benignos** (bajo radio, baja concavidad, PC1 negativo).
    - **4 clústeres mixtos o de frontera**, correspondientes a casos histológicos limítrofes donde se requiere confirmación por biopsia.

#### K-Means en Cáncer de Próstata ([`K-Means_prostate_cancer.R`](K-MEANS/K-Means_prostate_cancer.R))
- Determinación de $k = 3$ óptimo mediante método del codo y silueta.
- Mapeo en el plano PCA identificando **2 sub-clústeres malignos** y **1 clúster benigno homogéneo**.

---

### 7. Agrupamiento Jerárquico Aglomerativo (HAA)
*Directorio: [`HAA/`](HAA/)*

- **Métrica y Enlace:** Cálculo de matrices de distancia euclídea (`stats::dist`) y agrupamiento jerárquico mediante **enlace completo** (*complete linkage*, `method = "complete"`).
- **Corte de Dendrogramas:** Evaluación de alturas de corte horizontal (`h`) y particiones verticales fijando $k = 2$ en variables originales y $k = 4$ en espacio PCA.
- **Mapas de Calor de Asignación:** Al comparar las particiones sobre variables originales frente a las de PCA, se comprobó que el espacio PCA desglosa el clúster original mayoritario en subfenotipos más específicos.
- **Correlación Clúster-Variable:** Determinación de qué variables numéricas correlacionan con la pertenencia a cada rama del árbol jerárquico.

---

### 8. Discusión Comparativa de Métodos de Clustering
*Scripts: [`DiscussionOfClusteringResults_breast_cancer.R`](DiscussionOfClusteringResults_breast_cancer.R) y [`DiscussionOfClusteringResults_prostate_cancer.R`](DiscussionOfClusteringResults_prostate_cancer.R)*

Los scripts de síntesis comparan de forma directa K-Means frente al Agrupamiento Jerárquico (HCA):
- Fijando $k = 3$ sobre las coordenadas PCA, ambos algoritmos muestran una alta concordancia global, pero revelan discrepancias en las zonas limítrofes:
  - En Cáncer de Próstata, el Clúster 1 de K-Means coincide íntegramente con el Clúster 2 de HCA.
  - Los casos intermedios varían en su asignación debido a la diferencia intrínseca en la función objetivo: K-Means optimiza la varianza intra-clúster respecto a centroides móviles, mientras que el enlace completo de HCA busca minimizar el diámetro máximo entre pares de observaciones.

---

## 💡 Principales Hallazgos e Implicaciones Clínicas

1. **El Tamaño y la Concavidad Mandan en la Malignidad:** En todos los análisis (modelos lineales, regresión logística y PCA), las variables ligadas al radio, perímetro, área y puntos cóncavos del núcleo celular resultaron ser los predictores estadísticamente más determinantes ($p < 10^{-90}$).
2. **Alta Eficiencia en la Compresión por PCA:** Reducir 30 parámetros de cáncer de mama a 2 componentes principales permite retener más del **63%** de la varianza total (y cerca del **80%** al filtrar las medias), logrando que la primera componente (PC1) separe casi linealmente los tumores benignos de los malignos ($p = 3.13 \times 10^{-120}$).
3. **Elevada Sensibilidad en Clasificación Logística:** El modelo logístico con 4 predictores obtuvo una exactitud del **94.38%** y una sensibilidad del **96.64%**, minimizando el riesgo clínico de falsos negativos en el diagnóstico.
4. **Detección No Supervisada de Casos Limítrofes:** El agrupamiento K-Means ($k = 15$) no solo aisló subgrupos homogéneos de malignidad y benignidad, sino que identificó 4 clústeres de transición donde coexisten ambos diagnósticos, señalando muestras donde el cribado por imagen por sí solo presenta ambigüedad diagnóstica.

---

## 🛠 Tecnologías y Librerías de R

El proyecto ha sido desarrollado en **R (versión 4.x)** y RStudio, empleando el siguiente ecosistema de paquetes:

| Categoría | Paquetes de R |
| :--- | :--- |
| **Manipulación de Datos** | `dplyr`, `tidyr`, `reshape2`, `glue`, `pastecs` |
| **Visualización Avanzada** | `ggplot2`, `lattice`, `plotrix`, `patchwork`, `plotly`, `fields`, `scico` |
| **Modelado y Contrastes** | `car`, `moments`, `pROC`, `caret`, `ResourceSelection` |
| **Multivariante y Clustering** | `FactoMineR`, `factoextra`, `stats` |

---

## 🚀 Guía de Reproducibilidad y Ejecución

### 1. Clonar el Repositorio
```bash
git clone https://github.com/ikeiba/cancerResearch.git
cd cancerResearch
```

### 2. Instalación de Paquetes Necesarios
Abra una sesión de R o RStudio y ejecute:
```R
paquetes <- c(
  "dplyr", "tidyr", "reshape2", "glue", "pastecs",
  "ggplot2", "lattice", "plotrix", "patchwork", "plotly", "fields", "scico",
  "car", "moments", "pROC", "caret", "ResourceSelection",
  "FactoMineR", "factoextra"
)

nuevos <- paquetes[!(paquetes %in% installed.packages()[, "Package"])]
if(length(nuevos) > 0) install.packages(nuevos)
```

### 3. Ejecutar los Scripts
Establezca el directorio de trabajo en la raíz del repositorio:
```R
setwd("ruta/a/cancerResearch")
```

Ejecute cualquier módulo directamente:
```R
# 1. Análisis Descriptivo
source("DESCRIPTIVE_ANALYSIS/descriptive_analysis_breast_cancer.R")

# 2. Regresión Lineal
source("LINEAR_REGRESSION/linear_regression_breast_cancer.R")

# 3. Regresión Logística
source("LOGISTIC_REGRESSION/logistic_regression_breast_cancer.R")

# 4. Análisis de Componentes Principales (PCA)
source("PCA/PCA_breast_cancer.R")

# 5. Análisis de Correspondencias (CA)
source("CA/CA_breast_cancer.R")

# 6. Agrupamiento K-Means
source("K-MEANS/K-means_breast_cancer.R")

# 7. Agrupamiento Jerárquico Aglomerativo
source("HAA/HAA_Breast_Cancer.R")

# 8. Síntesis Comparativa de Clustering
source("DiscussionOfClusteringResults_breast_cancer.R")
```

---

<div align="center">
  <sub>Desarrollado para la asignatura de Estadística Avanzada en la Universidad de Deusto &bull; 2025</sub><br>
  <sub><a href="README.md">🇬🇧 Switch to English Version</a></sub>
</div>

