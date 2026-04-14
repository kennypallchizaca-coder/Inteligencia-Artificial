# Inteligencia Artificial — Practica de Laboratorio

## Analisis Exploratorio de Datos, Extraccion de Caracteristicas y Presentacion de Resultados

---

### Informacion General

| Campo | Detalle |
|---|---|
| **Estudiante** | Alex Guaman |
| **Asignatura** | Inteligencia Artificial / Machine Learning |
| **Tema** | Analisis Exploratorio de Datos (EDA) |
| **Dataset** | Titanic — Kaggle / Seaborn (891 obs. × 15 vars.) |

---

### Objetivos

- Reforzar los conocimientos adquiridos sobre analisis exploratorio de datos.
- Aplicar tecnicas para extraer caracteristicas a partir de un conjunto de datos.
- Presentar los resultados y conclusiones mas relevantes.

---

### Estructura del Proyecto

```
PRACTICA-IA-2.0/
|
|-- data/
|   +-- titanic.csv                          # Dataset de Titanic (Kaggle / Seaborn)
|
|-- notebooks/
|   |-- 00_fundamentos_python.ipynb          # Fundamentos de Python
|   +-- 01_analisis_exploratorio_datos.ipynb # EDA principal (Titanic)
|
|-- reports/
|   +-- Presentacion_Resultados_EDA_MATRIX.pptx  # Presentacion final (10 slides)
|
|-- src/                                     # Codigo fuente auxiliar
|
|-- requirements.txt                         # Dependencias del proyecto
+-- README.md                                # Este archivo
```

---

### Dataset Utilizado

**Titanic Dataset** — Kaggle / UCI Machine Learning Repository.

- **Registros:** 891 pasajeros
- **Variables:** 15 atributos demograficos, economicos y sociales
- **Variable objetivo (Y):** `survived` — Diagostico binario de supervivencia

| Variable | Descripcion |
|---|---|
| `survived` | Variable objetivo: 0 = No sobrevivio, 1 = Sobrevivio |
| `pclass` | Clase del boleto (1 = 1ra, 2 = 2da, 3 = 3ra) |
| `sex` | Genero del pasajero |
| `age` | Edad del pasajero (en anos) |
| `sibsp` | Numero de hermanos/conyuges a bordo |
| `parch` | Numero de padres/hijos a bordo |
| `fare` | Tarifa del boleto pagada (en libras esterinas) |
| `embarked` | Puerto de embarque (C=Cherbourg, Q=Queenstown, S=Southampton) |
| `deck` | Cubierta del barco (descartada: 77.1% de nulos) |

---

### Contenido del Analisis (EDA)

El notebook `01_analisis_exploratorio_datos.ipynb` desarrolla las siguientes etapas:

1. Carga y descripcion del dataset
2. Exploracion inicial — dimensiones, tipos de datos, primeros registros
3. Resumen estadistico descriptivo — media, desviacion estandar, percentiles
4. Limpieza de datos — valores faltantes (imputacion mediana/moda, eliminacion de `deck`)
5. Ingenieria de caracteristicas — creacion de `family_size`, `is_alone`, `sex_encoded`
6. Visualizacion de datos — histogramas, boxplots, graficos de barras
7. Analisis de variables categoricas — tablas de frecuencia y tablas cruzadas
8. Analisis de correlacion — matriz de correlacion con heatmap
9. Identificacion de las 3 variables mas correlacionadas con la variable objetivo
10. Analisis de outliers — deteccion formal mediante metodo IQR
11. Segmentacion de datos — analisis por sexo × clase y tamano de familia
12. Generacion de hipotesis — 5 hipotesis basadas en los patrones observados
13. Conclusiones finales — sintesis de hallazgos y proximos pasos

---

### Tecnologias y Librerias

| Libreria | Uso |
|---|---|
| Python 3.11+ | Lenguaje base |
| Pandas | Manipulacion y analisis de datos |
| NumPy | Operaciones numericas |
| Matplotlib | Visualizacion de datos |
| Seaborn | Visualizacion estadistica avanzada |
| python-pptx | Generacion de presentaciones |

---

### Ejecucion

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/PRACTICA-IA-2.0.git

# 2. Crear entorno virtual
python -m venv .venv

# 3. Activar entorno virtual (Windows)
.venv\Scripts\activate

# 4. Instalar dependencias
pip install -r requirements.txt

# 5. Abrir Jupyter Notebook
jupyter notebook notebooks/01_analisis_exploratorio_datos.ipynb
```

---

### Hallazgos Principales

- **Factor de mayor impacto:** El genero (`sex`) es el predictor mas fuerte. Las mujeres sobrevivieron en un 74.2% vs. hombres con solo un 18.9%.
- **Desigualdad social:** Los pasajeros de 1ra clase sobrevivieron en un 62.9% vs. 24.2% en 3ra clase.
- **Tarifa como proxy socioeconomico:** A mayor tarifa pagada, mayor probabilidad de supervivencia (correlacion r=+0.26).
- **Outliers conservados:** Los valores extremos en `fare` (hasta 512£) representan pasajeros historicos verificables y se mantienen en el dataset.

---

> Proyecto desarrollado como parte de la practica de laboratorio de la asignatura de Inteligencia Artificial.
