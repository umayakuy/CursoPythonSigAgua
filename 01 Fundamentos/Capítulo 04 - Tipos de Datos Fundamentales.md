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
