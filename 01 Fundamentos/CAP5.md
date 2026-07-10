---
title: "Capítulo 5. Colecciones de Datos: Modelando la Información de Sistemas de Agua Potable con Python"
chapter: 5
book: "Python para Ingenieros del Agua con QGIS"
---

# Capítulo 5
# Colecciones de Datos: Modelando la Información de Sistemas de Agua Potable con Python

> **Cada línea de código debe ayudar a comprender, analizar o mejorar un sistema de agua.**

## Ruta del conocimiento

```text
Tipos de datos fundamentales
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
PyQGIS
```

**Tiempo estimado:** 2 horas 30 minutos

# Bitácora del Ingeniero

En los capítulos anteriores aprendimos a representar información individual mediante variables y tipos de datos fundamentales. Sin embargo, una Empresa Prestadora de Servicios de Agua Potable administra miles de elementos: tuberías, válvulas, hidrantes, pozos, reservorios, estaciones de bombeo, medidores y resultados de laboratorio.

La pregunta deja de ser:

> **¿Cómo almaceno un dato?**

y pasa a ser:

> **¿Cómo represento un sistema completo de información utilizando Python?**

La respuesta comienza con las **colecciones**.

# Objetivos

- Comprender por qué una variable deja de ser suficiente.
- Representar información técnica mediante colecciones.
- Preparar estructuras de datos para futuros desarrollos con PyQGIS.

# 5.1 Cuando una variable deja de ser suficiente

Supongamos que el área de operación registra diariamente la presión en distintos puntos de la red.

```python
presion_p1 = 28.4
presion_p2 = 31.2
presion_p3 = 29.7
presion_p4 = 30.5
presion_p5 = 27.9
```

Este enfoque funciona para pocos datos, pero rápidamente se vuelve difícil de mantener.

## 💧 Ingeniería del Agua en Acción

Durante una actualización del catastro técnico se registran:

| Activo | Cantidad |
|--------|---------:|
| Tuberías | 4862 |
| Válvulas | 713 |
| Hidrantes | 158 |
| Pozos | 24 |
| Reservorios | 8 |

Intentar representar esta información mediante variables individuales sería inviable.

Necesitamos estructuras capaces de almacenar conjuntos de datos relacionados.

# 5.2 Del dato al sistema

Una variable representa un dato.

```python
diametro_mm = 110
```

Una colección representa un conjunto de datos.

```python
diametros_mm = [
    63,
    90,
    110,
    160,
    200
]
```

## 🗺️ Conexión con QGIS

Una capa vectorial contiene miles de entidades con atributos como diámetro, material, longitud y presión.

Las colecciones que aprenderemos en este capítulo serán la base para manipular esas entidades mediante PyQGIS.

# Buenas prácticas

- Utiliza nombres relacionados con Ingeniería del Agua.

# 5.3 Comprendiendo las Colecciones

Hasta este punto hemos identificado que una variable resulta adecuada para representar un único dato. Sin embargo, en un sistema de agua potable la información rara vez se presenta de forma aislada.

Un tramo de tubería no existe por sí solo; forma parte de una red. Un pozo pertenece a un sistema de producción. Un resultado de laboratorio forma parte de una campaña de muestreo. Una válvula está asociada a un sector hidráulico.

En consecuencia, la programación también debe reflejar esa realidad.

Las **colecciones** son estructuras que permiten agrupar información relacionada bajo un mismo concepto.

---

## ¿Qué información suele agruparse?

En una EPSA es habitual trabajar con conjuntos de información como los siguientes:

| Información | Ejemplo |
|-------------|----------|
| Diámetros de tuberías | 63, 90, 110, 160 mm |
| Materiales | PVC, PEAD, Hierro dúctil |
| Presiones | 28.4, 30.2, 31.7 m.c.a. |
| Pozos | PZ-001, PZ-002, PZ-003 |
| Reservorios | R-01, R-02 |
| Muestras de calidad | pH, turbidez, cloro residual |

Todos estos casos tienen algo en común:

> No representan un único elemento, sino un **conjunto de datos relacionados**.

---

## Del inventario físico al modelo computacional

Antes de programar conviene preguntarse:

**¿Qué estoy representando?**

Si la respuesta es:

- una red,
- un inventario,
- una serie de mediciones,
- un conjunto de activos,
- una colección de resultados,

entonces probablemente necesitaremos una colección de Python.

```text
Sistema de Agua Potable

 ├── Red de distribución
 ├── Producción
 ├── Calidad del agua
 ├── Catastro técnico
 └── Operación

            │

            ▼

Colecciones de Python
```

---

## 💧 Ingeniería del Agua en Acción

El Área de Catastro Técnico recibe un archivo con los diámetros de las tuberías instaladas durante una ampliación de red.

En lugar de crear una variable por cada tubería:

```python
diametro_1 = 110
diametro_2 = 90
diametro_3 = 63
diametro_4 = 160
```

podemos representar toda la información mediante una colección:

```python
diametros_mm = [
    110,
    90,
    63,
    160
]
```

La segunda alternativa es más clara, más escalable y facilita el procesamiento automático de la información.

---

## ¿Qué colecciones aprenderemos?

Durante este capítulo estudiaremos las principales colecciones incorporadas en Python.

| Colección | Uso principal |
|-----------|---------------|
| list | Información ordenada y modificable |
| tuple | Información ordenada que no cambia |
| dict | Atributos asociados a un elemento |
| set | Valores únicos sin repetición |

Cada una resolverá un problema distinto dentro de la Ingeniería del Agua.

---

## 🗺️ Conexión con QGIS

Una capa de tuberías contiene cientos o miles de entidades.

Cada entidad posee atributos como:

- diámetro;
- material;
- longitud;
- estado;
- año de instalación.

En los capítulos dedicados a PyQGIS veremos que estos atributos pueden leerse, modificarse y analizarse mediante las mismas colecciones que aprenderemos aquí.

---

## Reflexión

Las colecciones no son un tema exclusivo de programación.

Son la forma en que transformamos la infraestructura física de un sistema de agua potable en un modelo digital capaz de ser consultado, analizado y automatizado mediante Python.

# 5.4 La primera colección: las listas (`list`)

Hasta este momento comprendimos por qué las colecciones son necesarias. El siguiente paso consiste en conocer la colección más utilizada en Python: **la lista**.

Una lista representa una secuencia ordenada de elementos. En Ingeniería del Agua resulta ideal para almacenar datos que cambian constantemente, como mediciones, inventarios o registros operativos.

---

## ¿Por qué las listas son tan importantes?

Gran parte de la información que administra una Empresa Prestadora de Servicios de Agua Potable puede representarse inicialmente mediante listas.

Por ejemplo:

- diámetros de tuberías;
- presiones registradas en la red;
- códigos de pozos;
- niveles de reservorios;
- resultados de cloro residual;
- longitudes de tuberías por sector.

La lista permite almacenar todos esos valores bajo un mismo concepto.

---

## 💧 Ingeniería del Agua en Acción

Durante una inspección de campo se registran los diámetros nominales (mm) de las tuberías instaladas en un nuevo sector.

| Tramo | Diámetro (mm) |
|------:|--------------:|
| T-001 | 110 |
| T-002 | 90 |
| T-003 | 90 |
| T-004 | 160 |
| T-005 | 110 |

La representación en Python es sencilla:

```python
diametros_mm = [110, 90, 90, 160, 110]
```

No estamos almacenando cinco variables independientes.

Estamos representando un único conjunto de información.

---

## Anatomía de una lista

```text
Índice

 0     1    2     3     4

┌────┬────┬────┬─────┬────┐
│110 │ 90 │ 90 │ 160 │110 │
└────┴────┴────┴─────┴────┘
```

Python identifica cada posición mediante un **índice**, comenzando desde cero.

---

## Accediendo a un elemento

```python
print(diametros_mm[0])
print(diametros_mm[3])
```

Resultado:

```text
110
160
```

El índice representa la posición del elemento dentro de la colección.

---

## ¿Qué ocurre internamente?

Cuando Python crea una lista reserva un espacio para almacenar referencias a cada elemento.

```text
Lista

┌────┬────┬────┬────┬────┐
│ •  │ •  │ •  │ •  │ •  │
└────┴────┴────┴────┴────┘
  │    │    │    │    │
110   90   90   160  110
```

Más adelante comprenderemos por qué esta característica hace que las listas sean modificables.

---

## 🗺️ Conexión con QGIS

En una capa de tuberías, cada entidad tiene atributos como diámetro, material o longitud.

Cuando recorramos una capa con PyQGIS, el patrón mental será muy parecido al que acabamos de aprender:

1. Existe una colección de entidades.
2. Cada entidad ocupa una posición dentro de un recorrido.
3. Podemos acceder y procesar cada elemento.

Por ello, dominar las listas simplificará enormemente el aprendizaje de PyQGIS.

---

## Buenas prácticas

- Agrupa únicamente información del mismo tipo o del mismo contexto.
- Utiliza nombres descriptivos (`diametros_mm`, `presiones_mca`, `codigos_pozos`).
- Evita crear una variable para cada observación cuando todas pertenecen al mismo conjunto.

---

## Reflexión

Una lista representa mucho más que una estructura de datos.

Es el primer paso para convertir una red de agua potable, un inventario técnico o una campaña de monitoreo en un modelo computacional capaz de ser procesado automáticamente mediante Python.
- Conserva las unidades cuando aporten claridad.
- Modela primero el problema y luego elige la colección adecuada.
