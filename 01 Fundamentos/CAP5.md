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

# 5.5 Operaciones Fundamentales con Listas

Hasta este punto aprendimos que una lista permite representar un conjunto de datos relacionados. Sin embargo, su verdadero potencial aparece cuando comenzamos a **administrar** esa información.

En una Empresa Prestadora de Servicios de Agua Potable (EPSA), diariamente se incorporan nuevos activos, se actualizan registros y se eliminan datos incorrectos. Las listas permiten realizar estas operaciones de forma sencilla y eficiente.

---

## 💧 Ingeniería del Agua en Acción

Durante una ampliación de la red de distribución se instalaron tres nuevas tuberías de PVC.

El Área de Catastro Técnico debe actualizar el inventario.

Inicialmente se dispone del siguiente listado de códigos:

```python
tuberias = [
    "T-001",
    "T-002",
    "T-003"
]
```

Posteriormente se instala una nueva tubería.

```python
tuberias.append("T-004")

print(tuberias)
```

Resultado:

```text
['T-001', 'T-002', 'T-003', 'T-004']
```

La operación `append()` incorpora un nuevo elemento al final de la lista.

---

## Agregar varios elementos

Durante otra jornada se registran dos nuevas tuberías.

```python
tuberias.extend([
    "T-005",
    "T-006"
])
```

Ahora la colección representa de forma fiel el inventario actualizado.

---

## Insertar un elemento en una posición específica

Si por motivos de organización se requiere incorporar un registro en una posición determinada:

```python
tuberias.insert(1, "T-001A")
```

Resultado conceptual:

```text
Antes

T-001
T-002
T-003

Después

T-001
T-001A
T-002
T-003
```

---

## Eliminar información

En ocasiones un registro fue cargado por error o corresponde a un activo dado de baja.

Eliminar por valor:

```python
tuberias.remove("T-001A")
```

Eliminar por posición:

```python
tuberias.pop(0)
```

Eliminar toda la colección:

```python
tuberias.clear()
```

Cada operación responde a una necesidad distinta.

---

## Conociendo el tamaño del inventario

Es frecuente responder preguntas como:

- ¿Cuántos pozos existen?
- ¿Cuántas válvulas fueron inspeccionadas?
- ¿Cuántas muestras de agua se analizaron?

La función `len()` responde estas preguntas.

```python
pozos = [
    "PZ-001",
    "PZ-002",
    "PZ-003",
    "PZ-004"
]

print(len(pozos))
```

Resultado:

```text
4
```

---

## Recorriendo una lista

Hasta ahora accedimos a elementos individuales.

Pero la mayor fortaleza de una lista consiste en procesar automáticamente todos sus elementos.

Supongamos que se registraron las presiones (m.c.a.) en distintos puntos de la red.

```python
presiones_mca = [
    28.4,
    30.1,
    29.6,
    31.8,
    27.9
]
```

Podemos recorrerlas utilizando un ciclo `for`.

```python
for presion in presiones_mca:
    print(f"{presion} m.c.a.")
```

Resultado:

```text
28.4 m.c.a.
30.1 m.c.a.
29.6 m.c.a.
31.8 m.c.a.
27.9 m.c.a.
```

En este momento no profundizaremos en el funcionamiento de `for`; ese tema será desarrollado en el capítulo dedicado al control del flujo. Por ahora basta comprender que una lista puede procesarse elemento por elemento de manera automática.

---

## 🏗️ Modelando un Activo de la Red

Antes de continuar, pensemos en la información que caracteriza una tubería.

No existe únicamente un diámetro.

También existen:

- código;
- material;
- longitud;
- presión de operación;
- año de instalación;
- estado.

Una sola lista de diámetros ya no será suficiente.

Necesitaremos una estructura capaz de asociar múltiples atributos a un mismo elemento.

Esa necesidad dará origen a una nueva colección que estudiaremos más adelante: **los diccionarios**.

---

## 🗺️ Conexión con QGIS

Cuando un técnico selecciona todas las tuberías de un sector hidráulico en QGIS, el software trabaja internamente con una colección de entidades.

Más adelante recorreremos esas entidades mediante Python para:

- calcular longitudes;
- validar atributos;
- generar reportes;
- actualizar información automáticamente.

Las operaciones básicas aprendidas con listas serán reutilizadas constantemente en PyQGIS.

---

## Buenas prácticas

- Utiliza `append()` cuando incorpores un único registro.
- Utiliza `extend()` cuando agregues varios registros simultáneamente.
- Evita modificar una lista mientras la recorres, salvo que comprendas perfectamente sus implicaciones.
- Mantén nombres descriptivos y relacionados con el dominio de la Ingeniería del Agua.

---

## Lo que acabas de aprender como Ingeniero del Agua

Una lista no solo almacena información: también permite administrarla.

Agregar, eliminar, recorrer y contabilizar elementos son tareas cotidianas en la gestión de redes de agua potable. Estas operaciones constituyen la base para automatizar inventarios, catastros técnicos y procesos de análisis que posteriormente realizaremos con Python y PyQGIS.
- Conserva las unidades cuando aporten claridad.
- Modela primero el problema y luego elige la colección adecuada.

# 5.6 Modelando Información Técnica mediante Listas

Hasta ahora hemos utilizado listas para almacenar valores individuales, como diámetros o presiones. Sin embargo, en un proyecto real rara vez trabajaremos con una única variable. Lo habitual es administrar información técnica perteneciente a diferentes componentes de un sistema de abastecimiento de agua potable.

La clave consiste en identificar **qué información pertenece al mismo contexto** y organizarla en colecciones independientes.

---

## 💧 Ingeniería del Agua en Acción

Durante una inspección técnica se recopila la siguiente información de una ampliación de red.

| Código | Material | Diámetro (mm) | Longitud (m) |
|:------:|:--------:|--------------:|-------------:|
| T-001 | PVC | 110 | 125.4 |
| T-002 | PVC | 90 | 84.7 |
| T-003 | PEAD | 63 | 42.8 |
| T-004 | Hierro Dúctil | 160 | 218.3 |

Como todavía no conocemos los diccionarios, una forma sencilla de organizar estos datos consiste en utilizar varias listas relacionadas.

```python
codigos = ["T-001", "T-002", "T-003", "T-004"]

materiales = ["PVC", "PVC", "PEAD", "Hierro Dúctil"]

diametros_mm = [110, 90, 63, 160]

longitudes_m = [125.4, 84.7, 42.8, 218.3]
```

Cada lista representa una característica del mismo conjunto de tuberías.

---

## Pensando como Ingeniero

Antes de escribir código conviene preguntarse:

- ¿Qué estoy inventariando?
- ¿Qué atributos necesito registrar?
- ¿Cómo se relacionan entre sí?

Este análisis previo evita estructuras confusas y facilita el mantenimiento del programa.

---

## Series de Calidad del Agua

El mismo principio puede aplicarse a resultados de laboratorio.

```python
ph = [7.18, 7.26, 7.14, 7.21]

cloro_residual = [0.62, 0.58, 0.67, 0.64]

turbidez = [0.38, 0.41, 0.36, 0.40]
```

Estas listas representan una campaña de muestreo realizada en distintos puntos de la red.

---

## Inventario de Pozos

```python
pozos = [
    "PZ-001",
    "PZ-002",
    "PZ-003",
    "PZ-004"
]

caudal_bombeo_ls = [
    18.5,
    22.0,
    15.8,
    19.4
]
```

Aunque esta solución resulta útil, pronto aparecerá una pregunta importante:

> ¿Cómo asociar toda la información de un mismo pozo en una única estructura?

Responderemos esa pregunta cuando estudiemos los **diccionarios**.

---

## 🗺️ Conexión con QGIS

Una tabla de atributos de QGIS contiene columnas con información similar:

- Código.
- Material.
- Diámetro.
- Longitud.
- Estado.
- Fecha de instalación.

Cada columna puede entenderse como una colección de valores relacionados. Más adelante aprenderemos a leer y modificar estos atributos utilizando PyQGIS.

---

## ⚠️ Error frecuente

No mezcles información de distinta naturaleza dentro de una misma lista.

Evita:

```python
datos = [
    "T-001",
    110,
    "PVC",
    125.4,
    True
]
```

Aunque Python lo permite, esta estructura pierde significado rápidamente cuando el proyecto crece.

Es preferible organizar la información de forma lógica y prepararse para utilizar estructuras más expresivas, como los diccionarios.

---

## Lo que acabas de aprender como Ingeniero del Agua

Una lista puede representar mucho más que números.

Puede almacenar códigos de activos, resultados de laboratorio, diámetros, materiales o cualquier otro conjunto de información relacionado.

A medida que aumente la complejidad de los datos, necesitaremos estructuras capaces de mantener unidas todas las características de un mismo elemento. Ese será el siguiente paso en nuestro proceso de modelado de información.

# 5.7 Cuando una Lista Ya No Es Suficiente

En las secciones anteriores organizamos la información mediante varias listas independientes. Este enfoque es útil para comprender el funcionamiento de las colecciones, pero presenta una limitación importante: **la relación entre los datos depende de mantener el mismo orden en todas las listas**.

Mientras el conjunto de información es pequeño, esta estrategia funciona. Sin embargo, conforme un proyecto crece, mantener listas paralelas se vuelve propenso a errores.

---

## 💧 Ingeniería del Agua en Acción

Supongamos que el Área de Catastro Técnico administra la siguiente información.

```python
codigos = ["T-001", "T-002", "T-003"]

diametros_mm = [110, 90, 160]

materiales = ["PVC", "PVC", "Hierro Dúctil"]

longitudes_m = [125.4, 84.7, 218.3]
```

Observa que el índice **0** representa siempre la misma tubería.

```text
Índice      0

Código      T-001

Diámetro    110 mm

Material    PVC

Longitud    125.4 m
```

Pero ¿qué ocurriría si alguien elimina accidentalmente un elemento de una sola lista?

```python
diametros_mm.pop(1)
```

Ahora las listas dejan de representar la misma información.

```text
Código      T-002

Material    PVC

Longitud    84.7

Diámetro    ❌ Ya no coincide
```

La información pierde consistencia.

---

## Modelando correctamente un activo

En la realidad, una tubería es un único activo con muchas propiedades.

No tiene sentido separar artificialmente sus características.

Necesitamos una estructura que permita mantener unidas todas ellas.

Ese será precisamente el propósito de los **diccionarios**, que estudiaremos en la siguiente sección.

---

## 🏗️ Modelando un Activo de la Red

Antes de elegir una estructura de datos conviene identificar los atributos que describen un elemento.

Una tubería puede caracterizarse mediante:

| Atributo | Unidad |
|----------|---------|
| Código | — |
| Material | — |
| Diámetro | mm |
| Longitud | m |
| Estado | — |
| Año de instalación | año |
| Presión de operación | m.c.a. |

Todos estos atributos pertenecen al mismo objeto físico.

Nuestro objetivo como programadores es representar esa realidad de la forma más natural posible.

---

## 🗺️ Conexión con QGIS

Si observas la tabla de atributos de una capa de tuberías en QGIS encontrarás exactamente este mismo concepto.

Cada fila representa una tubería.

Cada columna representa uno de sus atributos.

Durante los próximos capítulos aprenderemos a construir estructuras de Python que reflejen este modelo y posteriormente interactúen con las capas vectoriales mediante PyQGIS.

---

## Buenas prácticas

- Evita depender de varias listas paralelas cuando la información describe un mismo elemento.
- Piensa primero en el activo físico y después en la estructura de datos.
- Mantén una correspondencia clara entre el modelo de ingeniería y el modelo computacional.

---

## Lo que acabas de aprender como Ingeniero del Agua

Las listas son excelentes para representar secuencias de datos, pero no siempre son la mejor opción para describir activos complejos.

Comprender sus límites es tan importante como conocer sus ventajas. En la siguiente sección incorporaremos una nueva colección que permitirá modelar tuberías, pozos, reservorios y muestras de calidad del agua de una forma mucho más natural y cercana a la realidad.

# 5.8 Modelando Activos mediante Diccionarios

En la sección anterior descubrimos que una lista resulta insuficiente cuando un elemento posee múltiples atributos. Este escenario es muy frecuente en Ingeniería del Agua.

Una tubería no está definida únicamente por su diámetro. Un pozo no se caracteriza solo por su caudal de bombeo. Una muestra de calidad del agua no está representada únicamente por el valor de pH.

Cada elemento posee un conjunto de propiedades que deben mantenerse unidas.

Python resuelve este problema mediante los **diccionarios (`dict`)**.

---

## 💧 Ingeniería del Agua en Acción

Durante la actualización del catastro técnico se registra una nueva tubería de la red de distribución.

La información disponible es la siguiente:

| Atributo | Valor |
|-----------|----------------|
| Código | T-015 |
| Material | PVC |
| Diámetro | 110 mm |
| Longitud | 235.40 m |
| Estado | Operativa |
| Presión | 31.8 m.c.a. |

Toda esta información pertenece a un único activo.

Representarla mediante un diccionario resulta mucho más natural.

```python
tuberia = {
    "codigo": "T-015",
    "material": "PVC",
    "diametro_mm": 110,
    "longitud_m": 235.40,
    "estado": "Operativa",
    "presion_mca": 31.8
}
```

---

## ¿Qué representa un diccionario?

Un diccionario almacena información mediante pares **clave : valor**.

```text
┌──────────────────────────────────────┐
│ codigo         → T-015               │
│ material       → PVC                 │
│ diametro_mm    → 110                 │
│ longitud_m     → 235.40              │
│ estado         → Operativa           │
│ presion_mca    → 31.8                │
└──────────────────────────────────────┘
```

Las claves identifican cada atributo.

Los valores contienen la información correspondiente.

---

## Accediendo a un atributo

```python
print(tuberia["diametro_mm"])
print(tuberia["material"])
```

Resultado

```text
110
PVC
```

En lugar de recordar posiciones como ocurre en una lista, utilizamos el nombre del atributo.

Esto hace que el código sea mucho más legible.

---

## Modificando información

Durante una inspección se reemplaza la tubería por una de mayor diámetro.

```python
tuberia["diametro_mm"] = 160
```

También es posible actualizar el estado operativo.

```python
tuberia["estado"] = "Fuera de servicio"
```

---

## Agregando nuevos atributos

A medida que evoluciona el proyecto pueden incorporarse nuevos datos.

```python
tuberia["anio_instalacion"] = 2025
```

Los diccionarios permiten ampliar la información sin modificar toda la estructura.

---

## 💧 Calidad del Agua

Los diccionarios también resultan ideales para representar una muestra de laboratorio.

```python
muestra = {
    "codigo": "M-024",
    "ph": 7.18,
    "cloro_residual_mg_l": 0.68,
    "turbidez_ntu": 0.41,
    "conductividad_us_cm": 435
}
```

Todos los resultados permanecen asociados a una misma muestra.

---

## 💧 Pozos

```python
pozo = {
    "codigo": "PZ-003",
    "profundidad_m": 128.5,
    "nivel_estatico_m": 21.4,
    "nivel_dinamico_m": 35.8,
    "caudal_ls": 19.6
}
```

Cada pozo representa un único activo con múltiples características técnicas.

---

## 🗺️ Conexión con QGIS

Observa la similitud entre un diccionario y una fila de la tabla de atributos de QGIS.

Cada campo de la tabla corresponde a una clave del diccionario.

Esta analogía facilitará enormemente el aprendizaje de PyQGIS, donde trabajaremos continuamente con atributos de entidades geográficas.

---

## Buenas prácticas

- Utiliza claves descriptivas.
- Mantén una nomenclatura consistente.
- Incluye unidades cuando aporten claridad (`diametro_mm`, `presion_mca`).
- Evita abreviaturas ambiguas.

---

## Lo que acabas de aprender como Ingeniero del Agua

Un diccionario permite representar un activo completo y no únicamente una colección de valores.

A partir de este momento ya es posible modelar tuberías, pozos, reservorios o muestras de calidad del agua de una manera muy similar a como aparecen en un sistema SIG o en una base de datos técnica.

En la siguiente sección veremos cómo combinar listas y diccionarios para representar redes completas de distribución de agua potable.
