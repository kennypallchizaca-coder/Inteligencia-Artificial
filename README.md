# Inteligencia Artificial — Practica de Laboratorio

## Analisis Exploratorio de Datos, Transformacion de Variables y Preparacion de Datos para ML

---

### Informacion General

| Campo | Detalle |
|---|---|
| **Estudiante** | Alex Guaman |
| **Asignatura** | Inteligencia Artificial / Machine Learning |
| **Temas** | EDA · Transformacion de Variables · Pipelines de ML |
| **Datasets** | Titanic (891 obs.) · DATOS-IA (6 obs.) |

---

### Objetivos

- Reforzar los conocimientos adquiridos sobre analisis exploratorio de datos.
- Aplicar tecnicas de transformacion de variables categoricas y numericas.
- Construir pipelines de preprocesamiento reproducibles con scikit-learn.
- Presentar los resultados y conclusiones mas relevantes.

---

### Estructura del Proyecto

```
PRACTICA-IA-2.0/
|
|-- data/
|   |-- titanic.csv                          # Dataset Titanic (Kaggle / Seaborn)
|   +-- DATOS-IA.xlsx                        # Dataset de practica (variables mixtas)
|
|-- notebooks/
|   |-- 00_fundamentos_python.ipynb          # Fundamentos de Python
|   |-- 01_analisis_exploratorio_datos.ipynb # EDA principal (Titanic)
|   +-- 02_transformacion_variables.ipynb    # Transformacion de variables (DATOS-IA)
|
|-- reports/
|   +-- Presentacion_Resultados_EDA_MATRIX.pptx  # Presentacion final (10 slides)
|
|-- src/                                     # Codigo fuente auxiliar
|-- requirements.txt                         # Dependencias del proyecto
+-- README.md                                # Este archivo
```

---

### Datasets Utilizados

#### Dataset 1 — Titanic

**Fuente:** Kaggle / UCI Machine Learning Repository.

- **Registros:** 891 pasajeros
- **Variables:** 15 atributos demograficos, economicos y sociales
- **Variable objetivo:** `survived` — 0 = No sobrevivio, 1 = Sobrevivio

| Variable | Descripcion |
|---|---|
| `survived` | Variable objetivo: 0 = No sobrevivio, 1 = Sobrevivio |
| `pclass` | Clase del boleto (1 = 1ra, 2 = 2da, 3 = 3ra) |
| `sex` | Genero del pasajero |
| `age` | Edad del pasajero (en anos) |
| `sibsp` | Numero de hermanos/conyuges a bordo |
| `parch` | Numero de padres/hijos a bordo |
| `fare` | Tarifa del boleto pagada (en libras esterinas) |
| `embarked` | Puerto de embarque (C, Q, S) |

#### Dataset 2 — DATOS-IA.xlsx

**Fuente:** Archivo del curso de Inteligencia Artificial.

- **Registros:** 6 personas
- **Variables:** 4 atributos de distinto tipo

| Variable | Tipo | Naturaleza | Valores |
|---|---|---|---|
| `sexo` | Categorica | Nominal | F, M |
| `edad` | Numerica | Continua | Valores enteros (anos) |
| `pais` | Categorica | Nominal | Brasil, Espana, Chile, Ecuador |
| `nivelSatisfaccion` | Categorica | Ordinal | no me gusta, neutral, me gusta |

---

### Practicas de Laboratorio

#### Practica 01 — Analisis Exploratorio de Datos (EDA)

**Notebook:** `01_analisis_exploratorio_datos.ipynb` | **Dataset:** Titanic

Etapas desarrolladas:

1. Carga y descripcion del dataset
2. Exploracion inicial: dimensiones, tipos de datos, primeros registros
3. Resumen estadistico descriptivo: media, desviacion estandar, percentiles
4. Limpieza de datos: valores faltantes (imputacion mediana/moda)
5. Ingenieria de caracteristicas: `family_size`, `is_alone`, `sex_encoded`
6. Visualizaciones: histogramas, boxplots, graficos de barras
7. Analisis de variables categoricas: tablas de frecuencia y tablas cruzadas
8. Analisis de correlacion: matriz de correlacion con heatmap
9. Identificacion de las 3 variables mas correlacionadas con la variable objetivo
10. Analisis de outliers: deteccion formal mediante metodo IQR
11. Segmentacion de datos: analisis por sexo x clase y tamano de familia
12. Generacion de hipotesis: 5 hipotesis basadas en los patrones observados
13. Conclusiones finales: sintesis de hallazgos y proximos pasos

---

#### Practica 02 — Transformacion de Variables

**Notebook:** `02_transformacion_variables.ipynb` | **Dataset:** DATOS-IA.xlsx

Actividades en clase:

1. **Tabla de diseno de transformaciones** — clasificacion de las 4 variables por tipo y naturaleza
2. **Transformaciones categoricas:**
   - `OneHotEncoder` para variables nominales (`sexo`, `pais`) → 6 columnas binarias
   - `OrdinalEncoder` para variable ordinal (`nivelSatisfaccion`) → orden: no me gusta < neutral < me gusta
3. **Transformaciones numericas:**
   - `StandardScaler` (Z-score) para `edad` → media=0, desviacion estandar=1
4. **Estadisticos post-transformacion:**
   - Media de `edad` estandarizada ≈ 0
   - Desviacion estandar de `edad` estandarizada ≈ 1

**Herramientas:** `Pipeline`, `ColumnTransformer`, `OneHotEncoder`, `OrdinalEncoder`, `StandardScaler` (scikit-learn).

---

### Tecnologias y Librerias

| Libreria | Version | Uso |
|---|---|---|
| Python | 3.10+ | Lenguaje base |
| Pandas | latest | Manipulacion y analisis de datos |
| NumPy | latest | Operaciones numericas |
| Matplotlib | latest | Visualizacion de datos |
| Seaborn | latest | Visualizacion estadistica avanzada |
| scikit-learn | latest | Transformacion de variables y pipelines |
| openpyxl | latest | Lectura de archivos Excel |
| python-pptx | latest | Generacion de presentaciones |

---

### Ejecucion

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/PRACTICA-IA-2.0.git
cd PRACTICA-IA-2.0

# 2. Crear y activar entorno virtual (Windows)
python -m venv .venv
.venv\Scripts\activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Abrir los notebooks
jupyter notebook notebooks/01_analisis_exploratorio_datos.ipynb
jupyter notebook notebooks/02_transformacion_variables.ipynb
```

---

### Hallazgos Principales

#### Practica 01 — EDA Titanic

- **Factor de mayor impacto:** El genero es el predictor mas fuerte. Las mujeres sobrevivieron en un 74.2% vs. 18.9% de los hombres.
- **Desigualdad social:** 1ra clase: 62.9% de supervivencia vs. 3ra clase: 24.2%.
- **Tarifa como proxy:** A mayor tarifa pagada, mayor probabilidad de supervivencia (r=+0.26).
- **Outliers conservados:** Valores extremos en `fare` (hasta 512 libras) son verificables historicamente.

#### Practica 02 — Transformacion de Variables

- Las variables nominales `sexo` y `pais` generan **6 columnas binarias** tras One-Hot Encoding (2 para sexo + 4 para paises: Brasil, Chile, Ecuador, Espana).
- La estandarizacion Z-score de `edad` produce **media ≈ 0** y **desviacion estandar ≈ 1**.
- El pipeline `Pipeline + ColumnTransformer` garantiza reproducibilidad y previene *data leakage*.

---

> Proyecto desarrollado como parte de la practica de laboratorio de la asignatura de Inteligencia Artificial.
