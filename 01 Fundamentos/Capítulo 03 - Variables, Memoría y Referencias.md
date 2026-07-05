---
title: "Capítulo 3 - Variables, Memoria y Referencias"
book: "Python Moderno para Desarrolladores SIG"
subtitle: "Fundamentos, Arquitectura y Desarrollo Profesional con QGIS, PostGIS, PyQt e Inteligencia Artificial"
edition: "Primera Edición"
version: "2.0"
module: "Módulo I - Fundamentos"
chapter: 3
status: "En desarrollo"
authors:
  - Jorge Ayala Niño de Guzmán
  - ChatGPT (OpenAI)
license: "CC BY-SA 4.0"
last_update: "2026-07-04"
---

# Capítulo 3

# Variables, Memoria y Referencias

---

# Ruta del Conocimiento

```text
                     PYTHON MODERNO PARA DESARROLLADORES SIG

MÓDULO I — FUNDAMENTOS

✅ Capítulo 1  La Filosofía de Python

✅ Capítulo 2  Todo es un Objeto

✅ Capítulo 3  Variables, Memoria y Referencias    ← Usted está aquí

⬜ Capítulo 4  Tipos de Datos

⬜ Capítulo 5  Colecciones

⬜ Capítulo 6  Funciones

⬜ Capítulo 7  Clases y Objetos

⬜ Capítulo 8  Módulos y Paquetes
```

---

# Tiempo estimado

| Concepto | Valor |
|----------|-------|
| Duración | 6 horas |
| Dificultad | ⭐⭐⭐☆☆ |
| Laboratorios | 5 |
| Ejercicios | 12 |
| Proyecto AQUA-SIG | Modelo de memoria y referencias |

---

# Historial de cambios

## Versión 2.0

### Cambios

- Reestructuración completa del capítulo.
- Explicación detallada del modelo de memoria de Python.
- Diagramas conceptuales.
- Introducción a referencias y mutabilidad.
- Integración con el proyecto AQUA-SIG.

---

# Bitácora del Ingeniero

Hasta este momento hemos aprendido dos ideas fundamentales.

La primera fue que Python posee una filosofía basada en la simplicidad y la legibilidad del código.

La segunda fue descubrir que todo en Python es un objeto.

Ahora es momento de responder una pregunta mucho más profunda.

**¿Cómo administra Python esos objetos?**

Cada vez que escribimos una línea de código, el intérprete crea objetos, los almacena en memoria, los relaciona con nombres y controla automáticamente su ciclo de vida.

Comprender este mecanismo permitirá escribir programas más seguros, evitar errores difíciles de detectar y entender con mayor facilidad bibliotecas complejas como PyQt, NumPy, GeoPandas o la API de QGIS.

Este capítulo constituye uno de los pilares fundamentales del libro.

---

# Objetivos del capítulo

Al finalizar este capítulo serás capaz de:

- Comprender qué es una variable en Python.
- Diferenciar entre un nombre y un objeto.
- Comprender qué es una referencia.
- Analizar el ciclo de vida de un objeto.
- Entender la diferencia entre reasignar una referencia y modificar un objeto.
- Comprender la diferencia entre objetos mutables e inmutables.
- Aplicar estos conceptos al desarrollo de aplicaciones SIG.

---

# Introducción

Cuando comenzamos a programar solemos pensar que una variable es un espacio de memoria donde se almacena un dato.

Aunque esa idea resulta útil para introducir algunos conceptos, no describe correctamente el funcionamiento interno de Python.

En Python existen tres elementos claramente diferenciados:

- El nombre.
- El objeto.
- La referencia entre ambos.

Durante todo este capítulo aprenderemos a distinguir estos tres conceptos y veremos cómo interactúan entre sí.

Una vez comprendidos, gran parte del comportamiento del lenguaje resultará mucho más intuitivo.

---

# ¿Qué ocurre cuando escribimos una asignación?

Consideremos la siguiente instrucción.

```python
x = 10
```

A simple vista parece una operación muy sencilla.

Sin embargo, el intérprete realiza internamente varias tareas.

De forma simplificada, el proceso es el siguiente.

1. Obtiene un objeto entero con valor `10`.
2. Si dicho objeto ya existe y puede reutilizarse, utiliza el existente.
3. Si no existe, crea uno nuevo.
4. Asocia el nombre `x` con ese objeto.
5. Incrementa el contador de referencias del objeto.

Todo este proceso ocurre en una fracción de segundo.

El resultado final puede representarse mediante el siguiente diagrama.

```text
Nombre

x
│
│
▼

┌───────────────────────┐
│       Objeto          │
│-----------------------│
│ Tipo : int            │
│ Valor: 10             │
└───────────────────────┘
```

Es importante observar que el nombre **no contiene** el objeto.

Únicamente permite acceder a él.

---

# Nombres y objetos

En Python los nombres funcionan como etiquetas.

Un nombre puede asociarse a cualquier objeto.

Por ejemplo.

```python
temperature = 18.5

city = "Cochabamba"

editable = True
```

En los tres casos ocurre exactamente el mismo mecanismo.

Cada nombre queda asociado a un objeto diferente.

```text
temperature ─────► 18.5

city ───────────► "Cochabamba"

editable ───────► True
```

La diferencia entre ellos radica únicamente en el tipo del objeto.

---

# Todo objeto posee identidad

Cada objeto creado por Python posee una identidad única durante la ejecución del programa.

Podemos consultar dicha identidad mediante la función incorporada `id()`.

```python
value = 10

print(id(value))
```

Resultado aproximado.

```text
140461357695152
```

Ese número representa la identidad del objeto durante la ejecución del programa.

No debe interpretarse como una dirección física de memoria ni utilizarse para escribir lógica de aplicación.

Su utilidad principal consiste en comprender cómo administra Python los objetos.

---

# El tipo del objeto

Todo objeto conoce su propio tipo.

Podemos consultarlo utilizando la función `type()`.

```python
value = 10

print(type(value))
```

Resultado.

```text
<class 'int'>
```

Otro ejemplo.

```python
name = "Python"

print(type(name))
```

Resultado.

```text
<class 'str'>
```

Y con una lista.

```python
layers = []

print(type(layers))
```

Resultado.

```text
<class 'list'>
```

El tipo determina qué operaciones puede realizar el objeto y cuáles no.

---

# Las tres propiedades fundamentales

En Python todos los objetos poseen tres propiedades esenciales.

| Propiedad | Descripción |
|------------|--------------------------------------------------------------|
| Identidad | Permite distinguir un objeto de cualquier otro. |
| Tipo | Define el comportamiento del objeto. |
| Valor | Representa la información almacenada. |

Podemos visualizar un objeto de la siguiente manera.

```text
┌────────────────────────────┐
│         Objeto             │
├────────────────────────────┤
│ Tipo      : int            │
│ Valor     : 10             │
│ Identidad : 140461357...   │
└────────────────────────────┘
```

Durante el resto del libro volveremos constantemente sobre estas tres propiedades.

Son la base del modelo de objetos de Python.

---

# Referencias

Cuando escribimos.

```python
a = 100
```

El nombre `a` queda asociado al objeto entero `100`.

Si posteriormente escribimos.

```python
b = a
```

No se crea un nuevo entero.

Simplemente aparece una segunda referencia hacia el mismo objeto.

```text
a ───────┐
         │
         ▼
     ┌─────────┐
     │   100   │
     └─────────┘
         ▲
         │
b ───────┘
```

Ambos nombres permiten acceder exactamente al mismo objeto.

Podemos comprobarlo fácilmente.

```python
a = 100
b = a

print(id(a))
print(id(b))
```

Los dos resultados serán iguales porque ambos nombres hacen referencia al mismo objeto.

---

# Reasignación

Ahora analizaremos el siguiente código.

```python
a = 100

b = a

a = 250
```

¿Qué ocurrió?

El objeto `100` continúa existiendo.

La única diferencia es que el nombre `a` dejó de apuntar a dicho objeto y comenzó a referirse a otro diferente.

El resultado puede representarse así.

```text
a ─────────► 250


b ─────────► 100
```

Este comportamiento constituye una de las ideas más importantes del lenguaje.

Python no modifica el objeto entero.

Simplemente cambia la referencia del nombre.

---

# Objetos mutables e inmutables

Una de las características más importantes del modelo de objetos de Python es que **no todos los objetos pueden modificarse** después de haber sido creados.

Dependiendo de su comportamiento, los objetos se clasifican en dos grandes grupos:

- Objetos **inmutables** (*immutable objects*).
- Objetos **mutables** (*mutable objects*).

Comprender esta diferencia permitirá explicar el comportamiento de las listas, diccionarios, funciones y clases durante todo el resto del libro.

---

# Objetos inmutables

Un objeto inmutable no puede cambiar su contenido una vez creado.

Si aparentemente cambia, en realidad Python crea un nuevo objeto.

Los principales tipos inmutables son:

| Tipo | Descripción |
|-------|-------------|
| int | Números enteros |
| float | Números reales |
| bool | Valores lógicos |
| complex | Números complejos |
| str | Cadenas de texto |
| tuple | Tuplas |

Veamos un ejemplo.

```python
number = 15

print(id(number))

number = 30

print(id(number))
```

La salida será similar a:

```text
140503428614800
140503428615440
```

Observa que el identificador cambió.

No se modificó el objeto original.

Python creó un nuevo objeto entero y el nombre `number` pasó a referirse a él.

---

# Visualizando la reasignación

Antes de la reasignación:

```text
number
   │
   ▼
┌──────────┐
│ int      │
│ Valor 15 │
└──────────┘
```

Después:

```text
number
   │
   ▼
┌──────────┐
│ int      │
│ Valor 30 │
└──────────┘
```

El objeto con valor **15** continúa existiendo mientras alguna referencia siga apuntando hacia él.

En caso contrario, Python podrá liberar la memoria automáticamente.

---

# Objetos mutables

Los objetos mutables sí permiten modificar su contenido.

Entre los más utilizados encontramos:

| Tipo | Descripción |
|-------|-------------|
| list | Lista |
| dict | Diccionario |
| set | Conjunto |
| bytearray | Arreglo de bytes |

En este caso el objeto permanece siendo el mismo.

Lo que cambia es su contenido interno.

---

# Primer ejemplo con listas

```python
layers = [
    "Water Network",
    "Sewer Network"
]

print(id(layers))
```

Ahora agregamos un nuevo elemento.

```python
layers.append("Hydrants")

print(id(layers))
```

El identificador será el mismo.

Python modificó el contenido del objeto existente.

No creó una lista nueva.

---

# Representación gráfica

Antes:

```text
layers
   │
   ▼

┌───────────────────────────────┐
│ Water Network                 │
│ Sewer Network                 │
└───────────────────────────────┘
```

Después del método `append()`:

```text
layers
   │
   ▼

┌───────────────────────────────┐
│ Water Network                 │
│ Sewer Network                 │
│ Hydrants                      │
└───────────────────────────────┘
```

La referencia no cambió.

Cambió el contenido del objeto.

---

# Compartiendo referencias

Analicemos el siguiente código.

```python
layers = [
    "Water",
    "Sewer"
]

backup = layers
```

Muchos programadores imaginan que existen dos listas.

En realidad solamente existe una.

```text
layers ─────┐
            │
            ▼

     ┌──────────────────────┐
     │ Water                │
     │ Sewer                │
     └──────────────────────┘
            ▲
            │
backup ─────┘
```

Ambos nombres hacen referencia exactamente al mismo objeto.

---

# Modificando una referencia compartida

Ahora ejecutamos.

```python
layers.append("Hydrants")
```

¿Qué ocurre?

```python
print(backup)
```

Resultado.

```text
['Water', 'Sewer', 'Hydrants']
```

¿Por qué apareció el nuevo elemento?

Porque **no existen dos listas**.

Existe una única lista con dos referencias.

---

# Comprobándolo mediante id()

```python
layers = [
    "Water",
    "Sewer"
]

backup = layers

print(id(layers))
print(id(backup))
```

La salida será similar a:

```text
2250843847552
2250843847552
```

El mismo identificador confirma que ambos nombres hacen referencia al mismo objeto.

---

# Copiando un objeto

En muchas situaciones necesitamos una copia independiente.

Para ello podemos utilizar el método `copy()`.

```python
layers = [
    "Water",
    "Sewer"
]

backup = layers.copy()
```

Ahora sí existen dos listas.

```text
layers ─────► Lista A

backup ─────► Lista B
```

Modificar una de ellas no afectará a la otra.

---

# Ejemplo

```python
layers = [
    "Water",
    "Sewer"
]

backup = layers.copy()

layers.append("Hydrants")

print(layers)

print(backup)
```

Resultado.

```text
['Water', 'Sewer', 'Hydrants']

['Water', 'Sewer']
```

Cada variable hace referencia a un objeto diferente.

---

# Copia superficial

El método `copy()` realiza una **copia superficial** (*shallow copy*).

Esto significa que únicamente copia el primer nivel de la estructura.

Por ejemplo.

```python
network = [
    ["Water"],
    ["Sewer"]
]

backup = network.copy()
```

La lista principal fue duplicada.

Sin embargo, las listas internas continúan compartiéndose.

Este comportamiento será estudiado con mayor profundidad cuando trabajemos con módulos especializados como `copy`.

---

# ¿Cuándo utilizar referencias?

Las referencias son útiles cuando varias partes del programa necesitan trabajar sobre el mismo objeto.

Por ejemplo.

- Una capa activa en QGIS.
- Una conexión a una base de datos.
- Una configuración compartida.
- Un proyecto abierto.

En estos casos resulta más eficiente compartir un único objeto que crear múltiples copias.

---

# ¿Cuándo utilizar copias?

Las copias son recomendables cuando deseamos preservar el estado original de un objeto.

Algunos ejemplos son:

- Antes de aplicar un algoritmo de procesamiento.
- Antes de modificar una configuración.
- Para implementar operaciones de deshacer (*Undo*).
- Para comparar estados antes y después de un procesamiento.

Elegir correctamente entre compartir referencias o crear copias es una decisión de diseño importante.

---

# Internamente (CPython)

Hasta ahora hemos estudiado el comportamiento visible de los objetos. Sin embargo, una de las fortalezas de Python es que gran parte de la administración de memoria ocurre automáticamente.

Como desarrolladores no necesitamos reservar ni liberar memoria manualmente, pero comprender cómo funciona este mecanismo nos ayudará a escribir programas más eficientes y a entender el comportamiento de bibliotecas como NumPy, PyQt, GeoPandas o la API de QGIS.

---

# El ciclo de vida de un objeto

Todo objeto creado durante la ejecución de un programa atraviesa un ciclo de vida compuesto por varias etapas.

```text
           Creación
               │
               ▼
      Asociación a un nombre
               │
               ▼
          Utilización
               │
               ▼
      Pérdida de referencias
               │
               ▼
      Liberación de memoria
```

Este proceso ocurre continuamente durante la ejecución de cualquier programa en Python.

---

# Creación de objetos

Cada vez que escribimos una instrucción como:

```python
layer_name = "Water Network"
```

Python crea un objeto de tipo `str` (o reutiliza uno existente cuando es posible) y asocia el nombre `layer_name` a dicho objeto.

Lo mismo ocurre con cualquier otro tipo de dato.

```python
count = 25

coordinates = []

station = {}
```

Cada instrucción produce uno o varios objetos nuevos.

---

# Referencias

Cuando un nombre apunta a un objeto, se dice que existe una referencia.

```python
a = 100

b = a
```

Ahora existen dos referencias hacia el mismo objeto.

```text
a ───────┐
         │
         ▼
    ┌────────────┐
    │    100     │
    └────────────┘
         ▲
         │
b ───────┘
```

Mientras exista al menos una referencia, el objeto seguirá disponible.

---

# Conteo de referencias

CPython utiliza principalmente un mecanismo denominado **Reference Counting**.

Cada objeto mantiene internamente un contador que indica cuántas referencias existen hacia él.

Podemos imaginarlo así.

```text
Objeto

┌─────────────────────┐
│ Valor : 100         │
│ Referencias : 2     │
└─────────────────────┘
```

Cuando ejecutamos:

```python
a = None
```

el contador disminuye.

```text
Objeto

┌─────────────────────┐
│ Valor : 100         │
│ Referencias : 1     │
└─────────────────────┘
```

Si posteriormente escribimos:

```python
b = None
```

el contador llegará a cero.

```text
Objeto

┌─────────────────────┐
│ Valor : 100         │
│ Referencias : 0     │
└─────────────────────┘
```

En ese momento Python puede liberar la memoria utilizada por dicho objeto.

---

# El recolector de basura

Existen situaciones donde dos objetos se referencian mutuamente.

Por ejemplo:

```text
Objeto A ─────► Objeto B
     ▲             │
     └─────────────┘
```

Aunque ya no exista ningún nombre que permita acceder a ellos, ambos continúan manteniendo referencias entre sí.

Para resolver estos casos CPython incorpora un **Garbage Collector**, encargado de detectar objetos inaccesibles y liberar automáticamente la memoria.

En la mayoría de los programas este proceso es completamente transparente para el desarrollador.

---

# ¿Debemos preocuparnos por la memoria?

En la mayoría de las aplicaciones, no.

Python administra automáticamente la memoria y elimina los objetos que dejan de utilizarse.

Sin embargo, comprender este mecanismo resulta muy útil cuando trabajamos con:

- grandes volúmenes de datos;
- imágenes satelitales;
- nubes de puntos LiDAR;
- modelos digitales de elevación;
- capas vectoriales con millones de entidades.

En estos casos, conocer el ciclo de vida de los objetos ayuda a reducir el consumo de memoria y mejorar el rendimiento de las aplicaciones.

---

# El objeto `None`

Python dispone de un objeto especial llamado `None`.

Representa la ausencia de un valor.

```python
layer = None
```

Esto no elimina el objeto anterior.

Simplemente hace que el nombre `layer` deje de apuntar a él y pase a referirse al objeto `None`.

```text
Antes

layer ─────► QgsVectorLayer

Después

layer ─────► None
```

Si ninguna otra referencia apunta al objeto original, este podrá ser liberado por Python.

---

# 🌎 Aplicación en SIG

Supongamos que abrimos una capa en QGIS.

```python
layer = iface.activeLayer()
```

Posteriormente obtenemos una segunda referencia.

```python
selected_layer = layer
```

Ahora ambas variables apuntan al mismo objeto.

```text
layer ─────────────┐
                   │
                   ▼
          QgsVectorLayer
                   ▲
                   │
selected_layer ────┘
```

Si iniciamos una edición:

```python
layer.startEditing()
```

también observaremos el cambio mediante:

```python
selected_layer.isEditable()
```

porque ambas referencias representan el mismo objeto.

Comprender este comportamiento evita muchos errores al desarrollar complementos para QGIS.

---

# 🏗️ Diseño de Software — AQUA-SIG

En AQUA-SIG cada elemento importante del sistema será representado mediante un objeto.

Por ejemplo:

```python
project = {
    "name": "AQUA-SIG",
    "layers": [],
    "version": "1.0"
}
```

A medida que el libro avance, este modelo evolucionará.

```text
Diccionario

        │

        ▼

Clase Project

        │

        ▼

Objeto Project

        │

        ▼

Aplicación completa
```

Este crecimiento progresivo permitirá comprender cómo un diseño sencillo puede transformarse en una arquitectura profesional.

---

# Consejo del Ingeniero

Cuando observes un comportamiento inesperado en un programa, no pienses únicamente en el código que acabas de escribir.

Pregúntate también:

- ¿Cuántas referencias existen hacia este objeto?
- ¿Estoy modificando el objeto correcto?
- ¿Necesito compartirlo o crear una copia?

En muchas ocasiones, responder estas preguntas permite localizar el problema mucho más rápido que revisar cientos de líneas de código.

---

# Laboratorio 1 — Explorando Objetos

## Objetivo

Comprender que toda variable hace referencia a un objeto y que cada objeto posee una identidad, un tipo y un valor.

### Ejercicio

Crear el siguiente programa.

```python
integer_value = 25
float_value = 18.75
text_value = "Python"
boolean_value = True

print(type(integer_value), id(integer_value))
print(type(float_value), id(float_value))
print(type(text_value), id(text_value))
print(type(boolean_value), id(boolean_value))
```

### Preguntas

1. ¿Todos los objetos poseen un identificador?
2. ¿Qué representa el resultado de `type()`?
3. ¿Puede cambiar el identificador de un objeto durante su vida útil?

---

# Laboratorio 2 — Referencias

Crear el siguiente programa.

```python
layer_name = "Water Network"

another_name = layer_name

print(id(layer_name))
print(id(another_name))
```

Responder.

- ¿Cuántos objetos existen?
- ¿Cuántos nombres hacen referencia al objeto?

---

# Laboratorio 3 — Objetos Mutables

```python
layers = [
    "Water",
    "Sewer"
]

backup = layers

layers.append("Hydrants")

print(layers)
print(backup)
```

Analizar.

¿Por qué ambas variables muestran exactamente el mismo contenido?

Realizar un diagrama de memoria representando la situación.

---

# Laboratorio 4 — Copias

Modificar el ejemplo anterior.

```python
layers = [
    "Water",
    "Sewer"
]

backup = layers.copy()

layers.append("Hydrants")

print(layers)
print(backup)
```

Responder.

- ¿Cuántas listas existen ahora?
- ¿Por qué el contenido es diferente?

---

# Laboratorio 5 — Consola Python de QGIS

Abrir QGIS.

Seleccionar una capa vectorial.

En la Consola Python ejecutar.

```python
layer = iface.activeLayer()

print(layer)

print(type(layer))

print(id(layer))
```

Ahora crear otra referencia.

```python
other = layer

print(id(other))
```

Comprobar que ambos nombres hacen referencia al mismo objeto.

---

# Laboratorio 6 — Explorando Objetos

Python incorpora la función `dir()`.

Permite conocer los atributos y métodos disponibles.

```python
layer = iface.activeLayer()

print(dir(layer))
```

Observar la gran cantidad de métodos disponibles.

En capítulos posteriores aprenderemos a utilizar muchos de ellos.

---

# Buenas prácticas

A partir de este capítulo seguiremos algunas recomendaciones que aparecerán durante todo el libro.

## Utilizar nombres descriptivos

Incorrecto.

```python
a = []
```

Correcto.

```python
layers = []
```

---

Incorrecto.

```python
x = 32719
```

Correcto.

```python
epsg_code = 32719
```

Los nombres descriptivos facilitan enormemente la lectura del código.

---

## No modificar objetos accidentalmente

Antes de modificar una lista importante pregúntate.

> ¿Deseo modificar el objeto original o necesito una copia?

Cuando exista duda, analiza cuidadosamente si debes utilizar una referencia o crear una copia.

---

## Comprender antes de optimizar

Python administra automáticamente la memoria.

No intentes optimizar el consumo de memoria sin comprender previamente cómo funciona el modelo de objetos.

Un diseño claro suele producir mejores resultados que una optimización prematura.

---

# Errores frecuentes

## Error 1

Pensar que una variable contiene un dato.

En realidad contiene una referencia hacia un objeto.

---

## Error 2

Confundir una referencia con una copia.

```python
a = b
```

No crea una copia.

Únicamente crea una nueva referencia.

---

## Error 3

Modificar listas compartidas sin saberlo.

```python
backup = layers
```

Ambas variables representan el mismo objeto.

---

## Error 4

Olvidar que las listas son mutables.

```python
layers.append(...)
```

El objeto cambia.

No se crea una nueva lista.

---

## Error 5

Pensar que `id()` representa una dirección física de memoria.

El resultado de `id()` debe interpretarse únicamente como un identificador del objeto durante la ejecución del programa.

---

# Conceptos clave

Al finalizar este capítulo deberías dominar los siguientes conceptos.

- Objeto
- Nombre
- Referencia
- Identidad
- Tipo
- Valor
- Mutabilidad
- Inmutabilidad
- Conteo de referencias
- Recolector de basura
- Reasignación
- Copia
- Referencia compartida

Estos conceptos aparecerán continuamente durante el resto del libro.

---

# Resumen

En este capítulo profundizamos en el funcionamiento interno del modelo de objetos de Python.

Aprendimos que una variable no almacena directamente un valor, sino que actúa como un nombre asociado a un objeto.

Estudiamos cómo Python administra las referencias, analizamos la diferencia entre objetos mutables e inmutables y comprendimos el papel del conteo de referencias y del recolector de basura dentro de CPython.

Estos conocimientos constituyen la base necesaria para comprender estructuras de datos más complejas, funciones, clases y el funcionamiento interno de bibliotecas como QGIS, PyQt y GeoPandas.

A partir de este momento utilizaremos estos conceptos de manera natural en todos los capítulos siguientes.

---

# Lo aprendido hoy

Ahora sabes que:

- Una variable es un nombre asociado a un objeto.
- Todo objeto posee identidad, tipo y valor.
- La asignación crea referencias.
- Existen objetos mutables e inmutables.
- Compartir una referencia no equivale a crear una copia.
- CPython administra automáticamente la memoria mediante conteo de referencias y un recolector de basura.
- Comprender el modelo de objetos facilita el desarrollo de aplicaciones robustas con Python y QGIS.

---

# Lo que construiremos mañana

Hasta ahora hemos trabajado con objetos sin estudiar en detalle sus características.

En el siguiente capítulo conoceremos los **tipos de datos fundamentales de Python**.

Aprenderemos cómo representar correctamente números, cadenas de texto, valores lógicos y otros tipos básicos, comprendiendo cuándo utilizar cada uno dentro del proyecto AQUA-SIG.

Ese conocimiento será la base para comenzar a construir estructuras de datos más complejas en los capítulos posteriores.

---

# Bibliografía recomendada

## Documentación oficial

- Python Software Foundation. *The Python Data Model*.
- Python Software Foundation. *Built-in Types*.
- Python Software Foundation. *Data Structures*.

## Libros

- Luciano Ramalho. *Fluent Python*.
- Brett Slatkin. *Effective Python*.
- David Beazley. *Python Cookbook*.
- Mark Lutz. *Learning Python*.

## Recursos adicionales

- Documentación oficial de QGIS.
- Documentación oficial de PyQGIS.
- Documentación oficial de GeoPandas.
- Documentación oficial de Shapely.

---

> *"Comprender el modelo de objetos de Python significa comprender el lenguaje. A partir de este capítulo, cada línea de código tendrá un significado mucho más profundo que una simple secuencia de instrucciones."*

---
