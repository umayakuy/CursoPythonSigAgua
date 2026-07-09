---
title: "Capítulo 4 - Tipos de Datos Fundamentales"
book: "Python Moderno para Desarrolladores SIG"
subtitle: "Fundamentos, Arquitectura y Desarrollo Profesional con QGIS, PostGIS, PyQt e Inteligencia Artificial"
edition: "Primera Edición"
version: "2.0"
module: "Módulo I - Fundamentos"
chapter: 4
status: "En desarrollo"
authors:
  - Jorge Ayala Niño de Guzmán
  - ChatGPT (OpenAI)
license: "CC BY-SA 4.0"
last_update: "2026-07-04"
---

# Capítulo 4

# Tipos de Datos Fundamentales

---

# Ruta del Conocimiento

```text
                     PYTHON MODERNO PARA DESARROLLADORES SIG

MÓDULO I — FUNDAMENTOS

✅ Capítulo 1  La Filosofía de Python

✅ Capítulo 2  Todo es un Objeto

✅ Capítulo 3  Variables, Memoria y Referencias

✅ Capítulo 4  Tipos de Datos Fundamentales   ← Usted está aquí

⬜ Capítulo 5  Colecciones

⬜ Capítulo 6  Funciones

⬜ Capítulo 7  Clases y Objetos

⬜ Capítulo 8  Módulos y Paquetes
```

---

# Tiempo estimado

| Concepto | Valor |
|----------|-------|
| Duración | 8 horas |
| Dificultad | ⭐⭐⭐☆☆ |
| Laboratorios | 6 |
| Ejercicios | 15 |
| Proyecto AQUA-SIG | Modelado de datos geoespaciales |

---

# Bitácora del Ingeniero

En el capítulo anterior aprendimos que toda variable hace referencia a un objeto.

Ahora surge una pregunta natural:

**¿Qué clase de objetos existen en Python?**

La respuesta es mucho más amplia de lo que parece.

Python incorpora numerosos tipos de datos diseñados para representar información de distinta naturaleza: números, texto, valores lógicos, secuencias, estructuras de datos y mucho más.

Elegir correctamente el tipo de dato es una de las decisiones más importantes durante el diseño de un programa.

Un buen modelo de datos facilita el desarrollo, mejora el rendimiento y hace que el código sea más claro y mantenible.

---

# Objetivos del capítulo

Al finalizar este capítulo serás capaz de:

- Identificar los principales tipos de datos incorporados en Python.
- Comprender cuándo utilizar cada uno.
- Diferenciar tipos numéricos, textuales y lógicos.
- Analizar las características de los tipos inmutables.
- Aplicar estos conceptos al desarrollo de aplicaciones SIG.

---

# Introducción

Todo programa necesita representar información.

Por ejemplo:

- Un nombre de una capa.
- Una coordenada.
- Un código EPSG.
- Una elevación.
- Un área.
- Una fecha.
- Un estado de edición.

Cada uno de estos datos posee características diferentes.

Python proporciona distintos tipos de datos para representar cada situación de la forma más adecuada.

Elegir correctamente el tipo de dato no solo mejora la claridad del código, sino que también evita errores y facilita el mantenimiento del software.

---

# Clasificación de los tipos de datos

Los tipos incorporados en Python pueden agruparse en varias categorías.

```text
Tipos de Datos

├── Numéricos
│   ├── int
│   ├── float
│   └── complex
│
├── Lógicos
│   └── bool
│
├── Texto
│   └── str
│
├── Colecciones
│   ├── list
│   ├── tuple
│   ├── dict
│   └── set
│
├── Binarios
│   ├── bytes
│   ├── bytearray
│   └── memoryview
│
└── Especiales
    └── NoneType
```

En este capítulo estudiaremos los tipos fundamentales.

Las colecciones se analizarán con profundidad en el siguiente capítulo.

---

# Los números en Python

Python incorpora tres tipos numéricos principales.

| Tipo | Descripción | Ejemplo |
|------|-------------|----------|
| int | Enteros | 25 |
| float | Reales | 15.75 |
| complex | Complejos | 4+3j |

Cada uno responde a necesidades específicas.

---

# El tipo int

Representa números enteros.

```python
population = 120000

epsg = 32719

features = 15284
```

Podemos comprobar su tipo.

```python
print(type(population))
```

Resultado.

```text
<class 'int'>
```

A diferencia de otros lenguajes, los enteros en Python no poseen un tamaño fijo.

Pueden crecer tanto como la memoria disponible lo permita.

Por ejemplo.

```python
value = 999999999999999999999999999999999999999999
```

Python administrará automáticamente la precisión necesaria.

---

# Operaciones con enteros

```python
a = 15

b = 8
```

```python
print(a + b)

print(a - b)

print(a * b)

print(a / b)

print(a // b)

print(a % b)

print(a ** b)
```

Cada operador tiene un significado específico.

| Operador | Descripción |
|-----------|-------------|
| + | Suma |
| - | Resta |
| * | Multiplicación |
| / | División |
| // | División entera |
| % | Residuo |
| ** | Potencia |

Estos operadores aparecerán continuamente durante el desarrollo del libro.

---

# Aplicación en SIG

Supongamos que deseamos conocer el número de entidades de una capa.

```python
feature_count = layer.featureCount()

print(feature_count)
```

El resultado será un número entero.

```python
print(type(feature_count))
```

Salida.

```text
<class 'int'>
```

Este tipo de dato resulta adecuado porque una capa no puede contener un número fraccionario de entidades.

---

# El tipo float

Los números reales permiten representar valores con parte decimal.

Ejemplos.

```python
elevation = 2568.42

temperature = 18.7

area = 2456.81

distance = 145.38
```

Todos estos valores son objetos de tipo `float`.

```python
print(type(area))
```

Resultado.

```text
<class 'float'>
```

Los valores de tipo `float` son ampliamente utilizados en aplicaciones geoespaciales, donde es habitual trabajar con coordenadas, distancias, áreas, pendientes y elevaciones.

---

# Precisión en los números reales

Es importante comprender que los números de tipo `float` se representan internamente mediante el estándar IEEE 754.

Como consecuencia, algunos valores no pueden almacenarse con precisión absoluta.

Por ejemplo.

```python
print(0.1 + 0.2)
```

El resultado puede sorprender.

```text
0.30000000000000004
```

No se trata de un error de Python, sino de una característica de la representación binaria de los números reales utilizada por la mayoría de los lenguajes de programación.

En aplicaciones científicas y de ingeniería es importante tener presente este comportamiento al realizar comparaciones entre valores de punto flotante.

aplicaciones SIG y en el proyecto AQUA-SIG.

---

# El tipo `complex`

Aunque su uso es menos frecuente en el desarrollo de aplicaciones SIG, Python incorpora soporte nativo para números complejos.

Un número complejo está formado por una parte real y una parte imaginaria.

```python
impedance = 3 + 4j

print(type(impedance))
```

Resultado.

```text
<class 'complex'>
```

Podemos acceder a sus componentes mediante las propiedades `real` e `imag`.

```python
print(impedance.real)

print(impedance.imag)
```

Resultado.

```text
3.0

4.0
```

Los números complejos son utilizados principalmente en:

- Ingeniería eléctrica.
- Procesamiento de señales.
- Física.
- Telecomunicaciones.
- Simulación matemática.

En la mayoría de aplicaciones desarrolladas con QGIS raramente serán necesarios, pero forman parte de los tipos fundamentales del lenguaje.

---

# El tipo `bool`

El tipo `bool` representa valores lógicos.

Solo existen dos posibles valores.

```python
True

False
```

Todo objeto de este tipo pertenece a la clase `bool`.

```python
editable = True

print(type(editable))
```

Resultado.

```text
<class 'bool'>
```

---

# ¿Para qué sirven los valores lógicos?

Los valores booleanos permiten representar estados.

Por ejemplo.

```python
layer_loaded = True

editing = False

connected = True

visible = True
```

Cada variable representa una condición del programa.

Más adelante utilizaremos estos valores para controlar el flujo de ejecución mediante estructuras condicionales.

---

# Operadores lógicos

Python incorpora tres operadores lógicos principales.

| Operador | Significado |
|-----------|-------------|
| and | Ambas condiciones deben cumplirse |
| or | Basta con que una condición sea verdadera |
| not | Invierte el valor lógico |

Ejemplo.

```python
editable = True

selected = False

print(editable and selected)

print(editable or selected)

print(not selected)
```

Resultado.

```text
False

True

True
```

Estos operadores aparecerán constantemente cuando trabajemos con estructuras `if`, `while` y filtros de datos.

---

# Comparaciones

Las comparaciones producen siempre un valor booleano.

```python
scale = 25000

print(scale > 10000)

print(scale == 25000)

print(scale != 50000)
```

Resultado.

```text
True

True

True
```

Los operadores de comparación más utilizados son:

| Operador | Descripción |
|-----------|-------------|
| == | Igual |
| != | Diferente |
| > | Mayor que |
| < | Menor que |
| >= | Mayor o igual |
| <= | Menor o igual |

---

# Aplicación en SIG

Es habitual verificar condiciones antes de ejecutar una operación.

```python
layer = iface.activeLayer()

print(layer.isEditable())
```

El método devuelve un valor booleano.

```text
True
```

o

```text
False
```

Este resultado puede utilizarse posteriormente para decidir si una operación puede continuar.

---

# El tipo `str`

Uno de los tipos más utilizados en Python es `str`.

Representa cadenas de texto.

```python
city = "La Paz"

river = "Río Desaguadero"

project = "AQUA-SIG"
```

Todos estos objetos pertenecen al tipo `str`.

```python
print(type(city))
```

Resultado.

```text
<class 'str'>
```

---

# Creando cadenas

Las cadenas pueden definirse utilizando comillas simples o dobles.

```python
name = "Python"

language = 'Español'
```

Ambas formas son equivalentes.

También es posible crear cadenas multilínea.

```python
description = """
Sistema de Gestión
de Agua Potable
"""
```

Este formato resulta útil para documentación, consultas SQL o textos extensos.

---

# Longitud de una cadena

Python incorpora la función `len()`.

```python
project = "AQUA-SIG"

print(len(project))
```

Resultado.

```text
8
```

`len()` será una de las funciones más utilizadas durante el desarrollo del libro.

---

# Concatenación

Las cadenas pueden unirse mediante el operador `+`.

```python
city = "El Alto"

country = "Bolivia"

location = city + ", " + country

print(location)
```

Resultado.

```text
El Alto, Bolivia
```

---

# Repetición

También pueden repetirse utilizando `*`.

```python
print("-" * 40)
```

Resultado.

```text
----------------------------------------
```

Esta técnica resulta útil para generar separadores en la salida por consola.

---

# Conversión de tipos

Frecuentemente necesitaremos convertir un tipo de dato en otro.

Por ejemplo.

```python
epsg = 32719

text = str(epsg)

print(type(text))
```

Resultado.

```text
<class 'str'>
```

También podemos realizar la operación inversa.

```python
value = "250"

number = int(value)
```

O convertir a número real.

```python
distance = "152.8"

meters = float(distance)
```

Las funciones de conversión más utilizadas son:

| Función | Resultado |
|----------|-----------|
| int() | Convierte a entero |
| float() | Convierte a real |
| str() | Convierte a texto |
| bool() | Convierte a lógico |

---

# Formato de cadenas

Una de las características más potentes de Python moderno son las **f-strings**.

Ejemplo.

```python
layer_name = "Water Network"

features = 15428

message = f"La capa {layer_name} contiene {features} entidades."

print(message)
```

Resultado.

```text
La capa Water Network contiene 15428 entidades.
```

Las f-strings son claras, eficientes y fáciles de leer.

A partir de este libro serán el mecanismo recomendado para construir mensajes.

---

# El objeto `None`

Existe un objeto especial denominado `None`.

Representa la ausencia de un valor.

```python
layer = None
```

Su tipo es:

```python
print(type(layer))
```

Resultado.

```text
<class 'NoneType'>
```

`None` no significa cero.

Tampoco significa una cadena vacía.

Representa simplemente que no existe un valor asociado.

---

# Aplicación en AQUA-SIG

Supongamos que el usuario aún no ha seleccionado ninguna capa.

```python
selected_layer = None
```

Más adelante, cuando el usuario seleccione una capa.

```python
selected_layer = iface.activeLayer()
```

La variable dejará de apuntar al objeto `None` y comenzará a referirse al objeto `QgsVectorLayer`.

Este patrón aparecerá constantemente durante el desarrollo del proyecto.

---
---

# Conversión de Tipos de Datos

En un programa es frecuente que la información provenga de diferentes fuentes.

Por ejemplo:

- Entrada del usuario.
- Archivos CSV.
- Bases de datos PostgreSQL.
- Archivos GeoPackage.
- Servicios Web.
- API de QGIS.

En muchos casos será necesario convertir un tipo de dato en otro antes de procesarlo.

Python proporciona funciones integradas para realizar estas conversiones de forma sencilla.

---

# Conversión a Entero

La función `int()` permite convertir diferentes tipos de datos en un número entero.

```python
value = "150"

number = int(value)

print(number)

print(type(number))
```

Resultado.

```text
150

<class 'int'>
```

También es posible convertir un número real.

```python
value = 25.98

number = int(value)

print(number)
```

Resultado.

```text
25
```

Es importante observar que **no se realiza un redondeo**.

La parte decimal simplemente se elimina.

---

# Conversión a Número Real

La función `float()` convierte un objeto a un número de punto flotante.

```python
value = "125.75"

distance = float(value)

print(distance)
```

Resultado.

```text
125.75
```

También puede convertir enteros.

```python
count = 12

result = float(count)

print(result)
```

Resultado.

```text
12.0
```

---

# Conversión a Texto

Todo objeto puede convertirse a una cadena utilizando `str()`.

```python
epsg = 32719

text = str(epsg)

print(text)

print(type(text))
```

Resultado.

```text
32719

<class 'str'>
```

Esta conversión resulta muy útil para construir mensajes o generar informes.

---

# Conversión a Booleano

La función `bool()` convierte un objeto en un valor lógico.

```python
print(bool(1))

print(bool(0))
```

Resultado.

```text
True

False
```

También funciona con cadenas.

```python
print(bool("Python"))

print(bool(""))
```

Resultado.

```text
True

False
```

---

# Valores considerados falsos

Python considera automáticamente algunos objetos como falsos.

| Valor | Resultado |
|--------|-----------|
| `None` | False |
| `0` | False |
| `0.0` | False |
| `""` | False |
| `[]` | False |
| `{}` | False |
| `set()` | False |

Todos los demás objetos son considerados verdaderos.

Esta característica simplifica considerablemente la escritura de condiciones.

---

# Conversión Implícita

En algunas operaciones Python realiza conversiones automáticamente.

Ejemplo.

```python
value = 15

distance = 12.5

result = value + distance

print(result)

print(type(result))
```

Resultado.

```text
27.5

<class 'float'>
```

Python promovió automáticamente el entero a un número real antes de realizar la suma.

Este proceso se denomina **conversión implícita**.

---

# Conversión Explícita

Cuando el programador solicita la conversión utilizando una función como `int()`, `float()` o `str()`, hablamos de una **conversión explícita**.

```python
value = "25"

number = int(value)
```

En este caso la conversión es completamente controlada por el desarrollador.

---

# Errores durante la conversión

No todas las conversiones son posibles.

Por ejemplo.

```python
value = "Python"

number = int(value)
```

Resultado.

```text
ValueError:
invalid literal for int()
```

Python genera una excepción indicando que la conversión no puede realizarse.

Más adelante aprenderemos a controlar estas situaciones mediante el manejo de excepciones.

---

# Operaciones entre tipos compatibles

Python permite combinar distintos tipos cuando la operación tiene sentido.

```python
distance = 120.5

extra = 15

total = distance + extra

print(total)
```

Resultado.

```text
135.5
```

Sin embargo, algunas operaciones no son válidas.

```python
"100" + 20
```

Resultado.

```text
TypeError
```

El texto y el número pertenecen a tipos distintos.

Antes de operar debemos convertir uno de ellos.

```python
result = int("100") + 20

print(result)
```

Resultado.

```text
120
```

---

# Aplicación en SIG

Supongamos que un archivo CSV contiene el código EPSG como texto.

```text
32719
```

Después de leer el archivo obtenemos.

```python
epsg = "32719"
```

Para utilizar ese código dentro de la API de QGIS será necesario convertirlo.

```python
epsg = int(epsg)
```

Ahora el dato posee el tipo adecuado.

---

# Lectura de Coordenadas

Supongamos que un archivo contiene las siguientes coordenadas.

```text
X,Y

723451.28,-8123456.42
```

Inicialmente ambos valores son texto.

```python
x = "723451.28"

y = "-8123456.42"
```

Antes de realizar cálculos deben convertirse.

```python
x = float(x)

y = float(y)
```

A partir de este momento podrán utilizarse para crear geometrías, calcular distancias o realizar análisis espaciales.

---

# Diseño de Software — AQUA-SIG

Durante el desarrollo de AQUA-SIG recibiremos información desde múltiples fuentes.

```text
Archivos CSV

GeoJSON

GeoPackage

PostgreSQL

Servicios WMS

Servicios WFS

API REST
```

Cada fuente puede representar los datos utilizando distintos tipos.

Uno de los primeros pasos del procesamiento consistirá en validar y convertir correctamente esos datos antes de utilizarlos.

Una correcta conversión evita errores difíciles de detectar en etapas posteriores del procesamiento.

---

# Consejo del Ingeniero

Nunca supongas que los datos tienen el tipo correcto.

Siempre verifica.

```python
print(type(variable))
```

o

```python
isinstance(variable, int)
```

Validar el tipo de los datos antes de procesarlos reduce considerablemente la aparición de errores durante la ejecución del programa.

---

# Laboratorio 1 — Identificando Tipos de Datos

## Objetivo

Reconocer el tipo de dato asociado a diferentes objetos utilizando la función `type()`.

### Ejercicio

Crear el siguiente programa.

```python
epsg = 32719
city = "El Alto"
area = 15234.85
editable = True
layer = None

print(type(epsg))
print(type(city))
print(type(area))
print(type(editable))
print(type(layer))
```

### Preguntas

1. ¿Qué tipo corresponde a cada variable?
2. ¿Cuál de ellas representa la ausencia de un valor?
3. ¿Cuál utilizarías para almacenar una coordenada UTM?

---

# Laboratorio 2 — Operaciones Numéricas

Crear el siguiente programa.

```python
length = 1250.75
width = 350.20

surface = length * width

print(surface)
```

### Actividades

- Cambiar los valores.
- Calcular un perímetro.
- Calcular una distancia promedio.

---

# Laboratorio 3 — Conversión de Tipos

Crear el siguiente programa.

```python
epsg = "32719"

print(type(epsg))

epsg = int(epsg)

print(type(epsg))
```

Responder.

- ¿Por qué es necesaria la conversión?
- ¿Qué ocurriría si intentamos realizar operaciones matemáticas sin convertir el dato?

---

# Laboratorio 4 — Cadenas de Texto

Crear el siguiente programa.

```python
project = "AQUA-SIG"

organization = "UmaYakuY Consultores SRL"

message = f"Proyecto: {project} - Organización: {organization}"

print(message)
```

Modificar el ejemplo agregando el nombre de una ciudad, un departamento y un código EPSG.

---

# Laboratorio 5 — Valores Booleanos

Crear el siguiente programa.

```python
editable = True

selected = False

print(editable and selected)

print(editable or selected)

print(not editable)
```

Analizar el resultado obtenido.

---

# Laboratorio 6 — Conversión de Coordenadas

Supongamos que un archivo CSV contiene las siguientes coordenadas.

```text
X,Y

623451.24,8112546.80
```

Inicialmente los datos son cadenas.

```python
x = "623451.24"

y = "8112546.80"
```

Convertir ambos valores al tipo adecuado.

```python
x = float(x)

y = float(y)

print(type(x))

print(type(y))
```

---

# Laboratorio 7 — Validación de Tipos

Python incorpora la función `isinstance()` para verificar el tipo de un objeto.

```python
distance = 152.45

print(isinstance(distance, float))

print(isinstance(distance, int))
```

Analizar el resultado.

Modificar el ejemplo utilizando otros tipos de datos.

---

# Buenas Prácticas

## Utilizar el tipo adecuado

Seleccionar correctamente el tipo de dato facilita el desarrollo del software.

Por ejemplo.

Un código EPSG.

```python
epsg = 32719
```

Debe representarse mediante un entero.

Una distancia.

```python
distance = 125.85
```

Debe representarse mediante un número real.

Un nombre de capa.

```python
layer_name = "Red de Agua Potable"
```

Debe representarse mediante una cadena.

---

## Evitar conversiones innecesarias

Convertir continuamente un mismo dato afecta la legibilidad del código.

Incorrecto.

```python
value = "25"

print(int(value))

print(int(value))

print(int(value))
```

Correcto.

```python
value = int(value)

print(value)

print(value)
```

---

## Utilizar f-strings

Para construir mensajes se recomienda utilizar cadenas formateadas.

```python
layer_name = "Water Network"

features = 15425

print(f"La capa {layer_name} contiene {features} entidades.")
```

Este formato es más claro que la concatenación mediante el operador `+`.

---

## Validar antes de convertir

Cuando los datos provienen de fuentes externas es recomendable verificar su contenido antes de realizar conversiones.

Por ejemplo.

```python
value = "125"
```

Antes de convertir:

```python
print(type(value))
```

Después.

```python
number = int(value)
```

Esta práctica facilita la detección de errores durante el desarrollo.

---

# Errores Frecuentes

## Error 1

Intentar sumar texto con números.

```python
"100" + 20
```

Produce un error de tipo.

La solución consiste en convertir previamente uno de los operandos.

---

## Error 2

Comparar números reales utilizando igualdad exacta.

```python
0.1 + 0.2 == 0.3
```

Este tipo de comparación puede producir resultados inesperados debido a la representación interna de los números de punto flotante.

---

## Error 3

Confundir `None` con una cadena vacía.

```python
value = None
```

No representa un texto vacío.

Representa la ausencia de un valor.

---

## Error 4

Utilizar un tipo de dato inadecuado.

Por ejemplo.

Guardar un código EPSG como texto cuando será utilizado posteriormente en operaciones numéricas.

---

## Error 5

No validar datos provenientes de archivos externos.

Los datos leídos desde un CSV, una base de datos o un servicio web pueden no tener el tipo esperado.

Siempre deben verificarse antes de utilizarlos.

---

# Conceptos Clave

Al finalizar este capítulo deberías dominar los siguientes conceptos.

- `int`
- `float`
- `complex`
- `bool`
- `str`
- `None`
- Conversión implícita
- Conversión explícita
- Funciones de conversión
- Validación de tipos
- Operadores aritméticos
- Operadores de comparación
- Operadores lógicos
- f-strings

Estos conceptos constituyen la base para trabajar con estructuras de datos más complejas.

---

# Resumen

En este capítulo estudiamos los tipos de datos fundamentales incorporados en Python.

Analizamos las características de los números enteros, los números reales, los números complejos, los valores booleanos, las cadenas de texto y el objeto especial `None`.

También aprendimos a convertir datos entre distintos tipos, comprendimos la diferencia entre conversiones implícitas y explícitas y analizamos situaciones habituales que aparecen durante el desarrollo de aplicaciones geoespaciales.

El conocimiento de estos tipos resulta indispensable para construir programas robustos, claros y fáciles de mantener.

---

# Lo aprendido hoy

Ahora sabes que:

- Python incorpora múltiples tipos de datos fundamentales.
- Cada tipo posee características y aplicaciones específicas.
- Las conversiones permiten adaptar los datos a diferentes contextos.
- `None` representa la ausencia de un valor.
- Las f-strings constituyen la forma recomendada para construir mensajes.
- La validación de tipos reduce errores durante el desarrollo.

---

# Lo que construiremos mañana

Hasta este momento hemos trabajado con objetos individuales.

En el siguiente capítulo aprenderemos a agrupar objetos utilizando las principales colecciones de Python.

Estudiaremos en profundidad:

- `list`
- `tuple`
- `dict`
- `set`

Estas estructuras constituyen el núcleo de prácticamente todas las aplicaciones desarrolladas en Python y serán fundamentales para construir el proyecto AQUA-SIG.

---

# Bibliografía recomendada

## Documentación oficial

- Python Software Foundation. *Built-in Types*.
- Python Software Foundation. *Standard Types*.
- Python Software Foundation. *Numeric Types*.
- Python Software Foundation. *Text Sequence Type — str*.

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

> *"Elegir correctamente un tipo de dato es una decisión de diseño. Un buen modelo de datos simplifica el código, reduce errores y facilita la evolución del software."*

---

