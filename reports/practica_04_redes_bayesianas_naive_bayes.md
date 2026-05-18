# Practica 04 - Redes Bayesianas y Naive Bayes

**Asignatura:** Inteligencia Artificial / Machine Learning  
**Titulo:** Aplicaciones de las Redes Bayesianas como herramientas de soporte a la toma de decisiones  
**Objetivo:** Desarrollar modelos para realizar la clasificacion de patrones mediante machine learning.

## 1. Investigacion: ejemplo de aplicacion de una Red Bayesiana

### a. Explicacion del caso de estudio

El caso de estudio corresponde a una red bayesiana para un sistema de alarma domiciliaria. La alarma puede sonar por un robo o por un terremoto. Luego, si la alarma suena, dos vecinos pueden llamar para reportar el evento.

La red funciona como una herramienta de apoyo a decisiones porque permite estimar la probabilidad de que exista un robo cuando solo se observan evidencias indirectas, como llamadas de vecinos o el sonido de la alarma. La decision no se toma con certeza absoluta, sino con probabilidades actualizadas mediante Bayes.

### b. Variables, valores, diagrama y tablas de probabilidad

| Variable | Descripcion | Valores |
|---|---|---|
| B | Robo | Si / No |
| E | Terremoto | Si / No |
| A | Alarma | Si / No |
| J | John llama | Si / No |
| M | Maria llama | Si / No |

**Diagrama de la red**

```text
Robo (B) ----------\
                    > Alarma (A) ---> John llama (J)
Terremoto (E) -----/                 \
                                      ---> Maria llama (M)
```

**Probabilidades iniciales**

| Variable | P(Si) | P(No) |
|---|---:|---:|
| Robo B | 0.001 | 0.999 |
| Terremoto E | 0.002 | 0.998 |

**Tabla condicional de la alarma**

| Robo B | Terremoto E | P(Alarma=Si) | P(Alarma=No) |
|---|---|---:|---:|
| Si | Si | 0.950 | 0.050 |
| Si | No | 0.940 | 0.060 |
| No | Si | 0.290 | 0.710 |
| No | No | 0.001 | 0.999 |

**Tabla condicional de llamadas**

| Alarma A | P(John llama=Si) | P(Maria llama=Si) |
|---|---:|---:|
| Si | 0.90 | 0.70 |
| No | 0.05 | 0.01 |

La probabilidad conjunta de la red se factoriza asi:

```text
P(B,E,A,J,M) = P(B)P(E)P(A|B,E)P(J|A)P(M|A)
```

### c. Dos ejemplos de prediccion siguiendo la red bayesiana

**Ejemplo 1: probabilidad de robo si John y Maria llaman**

Consulta:

```text
P(Robo=Si | John llama=Si, Maria llama=Si)
```

Usando enumeracion sobre las variables no observadas `Alarma` y `Terremoto`, el resultado es:

```text
P(Robo=Si | J=Si, M=Si) = 0.2842 = 28.42%
```

Interpretacion: aunque el robo inicialmente tiene una probabilidad muy baja, dos llamadas elevan la probabilidad a 28.42%. No llega a 100% porque tambien pueden existir falsas alarmas o llamadas equivocadas.

**Ejemplo 2: probabilidad de robo si la alarma sono y no hubo terremoto**

Consulta:

```text
P(Robo=Si | Alarma=Si, Terremoto=No)
```

Calculo:

```text
P(B|A,noE) = [P(A|B,noE)P(B)] / [P(A|B,noE)P(B) + P(A|noB,noE)P(noB)]

P(B|A,noE) = (0.94 * 0.001) / [(0.94 * 0.001) + (0.001 * 0.999)]
P(B|A,noE) = 0.4848 = 48.48%
```

Interpretacion: al saber que no hubo terremoto, se elimina una causa alternativa de la alarma. Por eso la probabilidad de robo aumenta a 48.48%.

## 2. Fase de preparacion de datos

Para no reutilizar los archivos existentes del proyecto, se selecciono un dataset nuevo: **Breast Cancer Wisconsin (Diagnostic)**. La copia local usada en la practica se guardo en `data/breast_cancer_wisconsin_diagnostic.csv`.

Caracteristicas principales:

| Elemento | Descripcion |
|---|---|
| Fuente | UCI Machine Learning Repository / scikit-learn |
| Registros | 569 |
| Variables predictoras | 30 |
| Tipo de variables | Numericas continuas |
| Variable objetivo | Diagnostico |
| Clases | malignant, benign |

Preparacion realizada:

1. Carga del dataset nuevo desde el CSV local `data/breast_cancer_wisconsin_diagnostic.csv`.
2. Revision de dimensiones, tipos de datos y primeras filas.
3. Verificacion de valores faltantes.
4. Revision de distribucion de clases.
5. Separacion entre variables predictoras `X` y variable objetivo `y`.
6. Division en entrenamiento y prueba con `train_test_split`, usando estratificacion.
7. Construccion de un `Pipeline` con `StandardScaler` y `GaussianNB`.

Archivos agregados en `data/` para esta practica:

| Archivo | Uso |
|---|---|
| `breast_cancer_wisconsin_diagnostic.csv` | Dataset principal para el modelo Naive Bayes. |
| `red_bayesiana_alarma_prior.csv` | Probabilidades iniciales de robo y terremoto. |
| `red_bayesiana_alarma_cpt_alarma.csv` | Tabla condicional de la alarma. |
| `red_bayesiana_alarma_cpt_llamadas.csv` | Tabla condicional de llamadas. |
| `nuevos_samples_bayes.csv` | Dos samples nuevos para prediccion. |

## 3. Fase de modelado: Naive Bayes

Se desarrollo un modelo **Gaussian Naive Bayes**. La eleccion se justifica porque el dataset contiene variables numericas continuas. Este tipo de Naive Bayes estima una distribucion normal por variable y por clase.

Configuracion usada:

```python
modelo_nb = Pipeline(steps=[
    ("scaler", StandardScaler()),
    ("naive_bayes", GaussianNB())
])
```

Resultado obtenido con una division 80/20, `random_state=42` y estratificacion:

```text
Accuracy en prueba: 0.9298
```

Matriz de confusion:

| Clase real / predicha | malignant | benign |
|---|---:|---:|
| malignant | 38 | 4 |
| benign | 4 | 68 |

El modelo logra un rendimiento adecuado para una linea base probabilistica. Ademas, entrega probabilidades por clase, lo cual es util para soporte a decisiones.

## 4. Prediccion de nuevos samples

Se construyeron dos samples nuevos de forma sintetica, usando la mediana de las variables por clase. No se copiaron filas existentes del dataset.

| Sample | Descripcion | Prediccion esperada |
|---|---|---|
| sample_nuevo_perfil_benigno | Perfil mediano de tumores benignos | benign |
| sample_nuevo_perfil_maligno | Perfil mediano de tumores malignos | malignant |

Resultados del modelo:

| Sample | Prediccion | P(malignant) | P(benign) |
|---|---|---:|---:|
| sample_nuevo_perfil_benigno | benign | 0.0000 | 1.0000 |
| sample_nuevo_perfil_maligno | malignant | 1.0000 | 0.0000 |

Interpretacion: el modelo clasifica correctamente los dos perfiles nuevos. El perfil benigno recibe probabilidad casi total de clase benigna, mientras que el perfil maligno recibe probabilidad casi total de clase maligna. En un problema medico real, estas salidas deben entenderse como apoyo al analisis y no como diagnostico final.

## 5. Conclusiones

- El teorema de Bayes permite actualizar probabilidades iniciales cuando aparece nueva evidencia.
- Las Redes Bayesianas son utiles para representar dependencias causales y razonar con incertidumbre.
- En la red de alarma, las llamadas de John y Maria aumentan la probabilidad de robo, pero no eliminan la incertidumbre.
- El dataset Breast Cancer Wisconsin (Diagnostic) permitio desarrollar una practica de clasificacion binaria con variables numericas continuas.
- `GaussianNB` fue una eleccion adecuada como modelo base por el tipo de variables y por su interpretacion probabilistica.
- Las predicciones de dos samples nuevos demuestran que el modelo puede separar perfiles representativos benignos y malignos.

## Referencias APA

Russell, S., & Norvig, P. (2021). *Artificial intelligence: A modern approach* (4th ed.). Pearson. https://aima.cs.berkeley.edu/

Scikit-learn developers. (2026). *Naive Bayes*. Scikit-learn documentation. https://scikit-learn.org/stable/modules/naive_bayes.html

Scikit-learn developers. (2026). *load_breast_cancer*. Scikit-learn documentation. https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_breast_cancer.html

Wolberg, W., Mangasarian, O., & Street, N. (1993). *Breast Cancer Wisconsin (Diagnostic)* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5DW2B

Zhang, H. (2004). The optimality of naive Bayes. *Proceedings of the Seventeenth International Florida Artificial Intelligence Research Society Conference*. https://www.cs.unb.ca/~hzhang/publications/FLAIRS04ZhangH.pdf
