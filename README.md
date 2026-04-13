# Inteligencia Artificial — Practica de Laboratorio

## Analisis Exploratorio de Datos, Extraccion de Caracteristicas y Presentacion de Resultados

---

### Informacion General

| Campo | Detalle |
|---|---|
| **Estudiante** | Alex Guaman |
| **Asignatura** | Inteligencia Artificial / Machine Learning |
| **Tema** | Analisis Exploratorio de Datos (EDA) |
| **Dataset** | Heart Disease — UCI Machine Learning Repository |

---

### Objetivos

- Reforzar los conocimientos adquiridos sobre analisis exploratorio de datos.
- Aplicar tecnicas para extraer caracteristicas a partir de un conjunto de datos.
- Presentar los resultados y conclusiones mas relevantes.

---

### Estructura del Proyecto

```
PRACTICA-IA/
|
|-- data/
|   +-- heart_disease.data              # Dataset de enfermedad cardiaca (UCI)
|
|-- notebooks/
|   |-- 00_fundamentos_python.ipynb      # Fundamentos de Python
|   +-- 01_analisis_exploratorio_datos.ipynb  # EDA principal
|
|-- reports/                             # Reportes y presentaciones
|
|-- src/                                 # Codigo fuente auxiliar
|
|-- requirements.txt                     # Dependencias del proyecto
+-- README.md                            # Este archivo
```

---

### Dataset Utilizado

**Heart Disease Dataset** del repositorio UCI Machine Learning.

- **Registros:** 303 pacientes
- **Variables:** 14 atributos clinicos
- **Variable objetivo:** Diagnostico de enfermedad cardiaca (multiclase transformada a binaria)

| Variable | Descripcion |
|---|---|
| `edad` | Edad del paciente |
| `sexo` | Sexo (0 = Femenino, 1 = Masculino) |
| `tipo_dolor_pecho` | Tipo de dolor toracico (1-4) |
| `presion_arterial_reposo` | Presion arterial en reposo (mm Hg) |
| `colesterol` | Colesterol serico (mg/dl) |
| `azucar_ayunas` | Azucar en sangre en ayunas > 120 mg/dl |
| `electrocardiograma_reposo` | Resultados del ECG en reposo |
| `frecuencia_cardiaca_max` | Frecuencia cardiaca maxima alcanzada |
| `angina_ejercicio` | Angina inducida por el ejercicio |
| `oldpeak` | Depresion del segmento ST |
| `pendiente_st` | Pendiente del segmento ST |
| `num_vasos` | Numero de vasos principales coloreados por fluoroscopia |
| `tal` | Talasemia |
| `objetivo` | Diagnostico (0 = sano, 1-4 = enfermo) |

---

### Contenido del Analisis (EDA)

El notebook `01_analisis_exploratorio_datos.ipynb` desarrolla las siguientes etapas:

1. Carga y descripcion del dataset
2. Exploracion inicial — dimensiones, tipos de datos, primeros registros
3. Resumen estadistico descriptivo — media, desviacion estandar, percentiles
4. Limpieza de datos — deteccion y tratamiento de valores faltantes (imputacion con mediana)
5. Ingenieria de caracteristicas — creacion de variable `objetivo_binario`
6. Visualizacion de datos — histogramas, boxplots, graficos de barras
7. Analisis de variables categoricas — tablas de frecuencia y tablas cruzadas
8. Analisis de correlacion — matriz de correlacion con heatmap
9. Identificacion de las 3 variables mas correlacionadas con la variable objetivo
10. Analisis de outliers — deteccion formal mediante metodo IQR
11. Segmentacion de datos — analisis por sexo y tipo de dolor de pecho
12. Generacion de hipotesis — 5 hipotesis basadas en los patrones observados
13. Conclusiones finales — sintesis de hallazgos y proximos pasos

---

### Tecnologias y Librerias

| Libreria | Uso |
|---|---|
| Python 3.14+ | Lenguaje base |
| Pandas | Manipulacion y analisis de datos |
| NumPy | Operaciones numericas |
| Matplotlib | Visualizacion de datos |
| Seaborn | Visualizacion estadistica avanzada |

---

### Ejecucion

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/PRACTICA-IA.git

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

- **Factores de riesgo clave:** `frecuencia_cardiaca_max`, `oldpeak`, `tipo_dolor_pecho` y `angina_ejercicio` son los predictores mas fuertes de enfermedad cardiaca.
- **Diferencias por sexo:** Los hombres presentan mayor proporcion de enfermedad cardiaca (55.61%) frente a las mujeres (25.77%).
- **Tipo de dolor:** El tipo 4 (asintomatico) se asocia con la mayor tasa de enfermedad (72.92%).
- **Outliers:** Se detectaron valores atipicos en variables clinicas, pero se conservan por su relevancia medica.

---

> Proyecto desarrollado como parte de la practica de laboratorio de la asignatura de Inteligencia Artificial.
