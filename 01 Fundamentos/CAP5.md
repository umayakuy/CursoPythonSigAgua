---
title: "Capítulo 5. Colecciones de Datos: Modelando la Información de la Ingeniería del Agua"
chapter: 5
book: "Python para Ingenieros del Agua con QGIS"
author_role: "Primera Parte"
---

# Capítulo 5
# Colecciones de Datos: Modelando la Información de la Ingeniería del Agua

> *"Los datos aislados describen una observación; las colecciones describen un sistema."*

---

## Ruta del Conocimiento

```text
Tipos Fundamentales
        │
        ▼
Dato individual
        │
        ▼
Colecciones
        │
        ▼
Modelado de información
        │
        ▼
Análisis
        │
        ▼
PyQGIS
```

**Tiempo estimado:** 2 horas

---

# Bitácora del Ingeniero

Hasta este momento hemos aprendido a representar un dato individual: un caudal, una precipitación, una coordenada UTM o el nombre de una estación hidrométrica.

Sin embargo, la Ingeniería del Agua casi nunca trabaja con un único dato.

Cuando un ingeniero analiza una cuenca hidrográfica, procesa cientos o miles de observaciones provenientes de estaciones meteorológicas e hidrométricas. Cuando desarrolla un proyecto en QGIS, una capa vectorial puede contener miles de entidades con numerosos atributos. Del mismo modo, un modelo digital de elevación está compuesto por millones de celdas.

La pregunta deja de ser **"¿Cómo almaceno un dato?"** y pasa a ser:

> **¿Cómo organizo grandes cantidades de información de forma eficiente y comprensible?**

Python responde a esa necesidad mediante las **colecciones**.

---

# Objetivos

Al finalizar esta primera parte podrás:

- Comprender por qué existen las colecciones.
- Diferenciar un dato individual de un conjunto de datos.
- Identificar problemas reales donde una colección resulta indispensable.
- Comprender la relación entre las colecciones de Python y la organización de datos utilizada posteriormente por PyQGIS.

---

# 5.1 ¿Por qué existen las colecciones?

Imaginemos que debemos registrar el caudal medio diario de una estación hidrométrica durante una semana.

Una primera aproximación podría ser:

```python
caudal_lunes = 2.31
caudal_martes = 2.48
caudal_miercoles = 2.27
caudal_jueves = 2.52
caudal_viernes = 2.43
caudal_sabado = 2.39
caudal_domingo = 2.45
```

Aunque funciona, rápidamente aparecen problemas:

- demasiadas variables;
- difícil recorrer los datos;
- difícil calcular estadísticas;
- difícil reutilizar el código.

La dificultad no está en Python.

Está en que **estamos utilizando variables para resolver un problema que requiere una colección**.

---

# 💧 Ingeniería del Agua en Acción

Una campaña de monitoreo registra diariamente:

- Caudal
- pH
- Conductividad eléctrica
- Temperatura
- Turbidez

en **45 estaciones** durante **365 días**.

Eso representa:

```text
45 estaciones

×

365 días

×

5 variables

=

82 125 observaciones
```

Nadie escribiría 82 125 variables.

Necesitamos una estructura que permita agrupar información relacionada.

Ahí nacen las colecciones.

---

# 5.2 Del dato al conjunto de datos

Observemos la evolución del problema.

## Un dato

```python
caudal = 2.35
```

Representa una única observación.

---

## Varios datos relacionados

```python
caudales = [
    2.35,
    2.48,
    2.51,
    2.44,
    2.39
]
```

Ahora la información posee contexto.

Ya no hablamos de un valor aislado, sino de una serie de mediciones.

---

# ¿Qué estamos modelando realmente?

No estamos aprendiendo una lista.

Estamos modelando un fenómeno hidrológico.

```text
Río
 │
 ├── Medición 1
 ├── Medición 2
 ├── Medición 3
 ├── Medición 4
 └── Medición 5

        │

        ▼

Lista de Python
```

---

# Pensando como Ingeniero

Un ingeniero rara vez pregunta:

> "¿Qué colección debo utilizar?"

Primero pregunta:

> "¿Cómo está organizada mi información?"

Después selecciona la estructura adecuada.

Ese cambio de perspectiva será una constante durante todo el libro.

---

# 🗺️ Conexión con QGIS

En QGIS una capa vectorial contiene muchas entidades.

Cada entidad posee atributos.

Más adelante descubriremos que muchas operaciones de PyQGIS consisten en recorrer colecciones de entidades.

Por ello, comprender las colecciones de Python es un requisito indispensable antes de comenzar a programar con PyQGIS.

---

# Proyecto AQUA-SIG

Durante todo el libro construiremos una aplicación que apoye la gestión de información hidrológica.

En este capítulo comenzaremos definiendo la información que deberá almacenar.

```text
AQUA-SIG

├── Estaciones
├── Cuencas
├── Ríos
├── Campañas
├── Mediciones
└── Resultados
```

Cada elemento será representado mediante las colecciones que aprenderemos en este capítulo.

---

# Buenas prácticas

- Utiliza nombres que representen conceptos de Ingeniería del Agua.
- Evita ejemplos genéricos como `x`, `dato` o `lista1`.
- Piensa primero en el problema y luego en la estructura de datos.

---

# Error frecuente

Muchos principiantes crean una variable por cada medición.

Ese enfoque funciona con pocos datos, pero se vuelve inmanejable en proyectos reales.

Las colecciones existen precisamente para resolver ese problema.

---

# Lo que acabas de aprender como Ingeniero del Agua

Hoy no aprendiste únicamente un nuevo concepto de Python.

Aprendiste que la programación comienza cuando dejamos de pensar en datos aislados y empezamos a representar sistemas completos.

Una red hidrométrica, una campaña de monitoreo o una tabla de atributos de QGIS son, en esencia, **colecciones de información**.

En la siguiente parte comenzaremos a estudiar la primera y más utilizada de todas ellas: **las listas**.

# 5.3 La primera gran colección: las listas (`list`)

> **Idea clave:** Una lista permite almacenar una secuencia ordenada de elementos. En Ingeniería del Agua es la estructura natural para representar observaciones, estaciones, campañas de monitoreo o resultados de simulaciones.

---

## 💧 Ingeniería del Agua en Acción

Supongamos que durante una campaña de aforo se obtuvieron los siguientes caudales (m³/s):

| Hora | Caudal |
|------:|-------:|
|08:00|2.31|
|10:00|2.45|
|12:00|2.58|
|14:00|2.49|
|16:00|2.37|

En Python podemos representarlos como una lista.

```python
caudales = [2.31, 2.45, 2.58, 2.49, 2.37]
```

No estamos almacenando cinco variables independientes.

Estamos representando una **serie de observaciones**.

---

# ¿Por qué una lista?

Porque conserva:

- el orden;
- todos los elementos;
- la posibilidad de recorrerlos;
- la posibilidad de modificarlos.

```text
Índice

 0      1      2      3      4

┌────┬────┬────┬────┬────┐
│2.31│2.45│2.58│2.49│2.37│
└────┴────┴────┴────┴────┘
```

Los índices comienzan en **0**, una característica fundamental de Python.

---

# Creando listas

Lista de estaciones hidrométricas:

```python
estaciones = [
    "ROC001",
    "ROC002",
    "ROC003",
    "ROC004"
]
```

Lista de precipitaciones diarias:

```python
precipitaciones = [
    12.5,
    0.0,
    5.8,
    18.2,
    7.4
]
```

Lista de nombres de cuencas:

```python
cuencas = [
    "Río Rocha",
    "Katari",
    "Desaguadero",
    "Pilcomayo"
]
```

---

# Accediendo a los elementos

```python
caudales = [2.31, 2.45, 2.58, 2.49]

print(caudales[0])
print(caudales[2])
```

Resultado

```text
2.31
2.58
```

---

# 🗺️ Conexión con QGIS

Cuando más adelante obtengamos todas las entidades de una capa vectorial, conceptualmente estaremos trabajando con una colección ordenada.

Comprender cómo acceder a un elemento mediante su posición facilitará posteriormente el trabajo con entidades y atributos en PyQGIS.

---

# Longitud de una lista

Durante un monitoreo es común preguntar:

> ¿Cuántas observaciones tenemos?

```python
numero_observaciones = len(caudales)

print(numero_observaciones)
```

Resultado

```text
4
```

---

# Agregando nuevos registros

Cada nueva medición puede incorporarse utilizando `append()`.

```python
caudales = [2.31, 2.45, 2.58]

caudales.append(2.62)
```

Ahora la lista contiene cuatro mediciones.

---

# Recorriendo una lista

El verdadero potencial aparece cuando recorremos automáticamente todas las observaciones.

```python
caudales = [2.31, 2.45, 2.58, 2.49]

for caudal in caudales:
    print(caudal)
```

Esta idea será utilizada constantemente para procesar:

- estaciones;
- capas SIG;
- registros meteorológicos;
- resultados hidráulicos.

---

# 💡 Consejo del Ingeniero

Antes de escribir muchas variables con el mismo significado, pregúntate:

> ¿Estoy describiendo un solo dato o una colección de datos?

Si la respuesta es una colección, probablemente necesites una lista.

---

# 🚀 Proyecto AQUA-SIG

La primera versión del sistema almacenará las estaciones disponibles.

```python
estaciones = [
    "ROC001",
    "ROC002",
    "ROC003",
    "ROC004",
    "ROC005"
]
```

Más adelante cada estación incorporará atributos, geometría y resultados de monitoreo.

---

# Resumen de esta segunda parte

En esta sección aprendimos que una lista es mucho más que una estructura de Python.

Es la forma natural de representar información secuencial en Ingeniería del Agua:

- campañas de monitoreo;
- series de caudales;
- precipitaciones;
- estaciones;
- resultados de modelos.

En la siguiente parte ampliaremos las operaciones sobre listas y conoceremos nuevas colecciones como tuplas y diccionarios, fundamentales para modelar atributos y preparar datos para PyQGIS.

