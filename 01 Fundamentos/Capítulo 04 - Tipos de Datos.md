---
title: "Capítulo 4 - Tipos de Datos"
book: "Python Moderno para Desarrolladores SIG"
chapter: 4
version: 1.0
status: En desarrollo
author:
  - Jorge Ayala Niño de Guzmán
  - ChatGPT (OpenAI)
last_update: 2026-07-04
level: Fundamentos
estimated_time: "8 horas"
prerequisites:
  - Capítulo 3 - Variables, Memoria y Referencias
---

# Capítulo 4

# Tipos de Datos

> *"Los datos son el lenguaje con el que un programa describe el mundo."*

---

# Bitácora del Ingeniero

Una de las preguntas más frecuentes en cursos de programación es:

> ¿Por qué existen tantos tipos de datos?

¿No bastaría con almacenar números y texto?

La respuesta aparece cuando desarrollamos aplicaciones reales.

En un proyecto SIG podemos encontrar:

- Coordenadas
- Elevaciones
- Fechas
- Imágenes
- Geometrías
- Capas
- Archivos
- Servicios WMS
- Objetos de QGIS

Cada uno representa información diferente y requiere comportamientos distintos.

Por ello Python dispone de una rica colección de tipos de datos.

---

# Objetivos

Al finalizar este capítulo serás capaz de:

- Comprender qué es un tipo de dato.
- Identificar los tipos fundamentales de Python.
- Comprender la diferencia entre mutables e inmutables.
- Utilizar correctamente cada tipo.
- Descubrir métodos mediante introspección.

---

# ¿Qué es un tipo de dato?

Un tipo de dato define:

- qué información puede almacenar un objeto;
- qué operaciones pueden realizarse sobre él;
- cómo se representa internamente.

En otras palabras:

> Un tipo define el comportamiento de un objeto.

---

# Ejemplo

```python
x = 15
```

Pregunta:

¿Qué puede hacer un entero?

```python
print(dir(x))
```

Encontraremos métodos como:

```text
bit_length()

to_bytes()

as_integer_ratio()
```

Un entero posee operaciones específicas.

---

Ahora observemos un texto.

```python
nombre = "Python"
```

```python
dir(nombre)
```

Encontraremos:

```text
upper()

lower()

replace()

find()

split()

strip()
```

Los textos poseen un comportamiento completamente diferente.

---

# Los tipos fundamentales

Python incorpora numerosos tipos.

Los más utilizados son:

| Tipo | Clase | Mutable |
|-------|--------|----------|
| Entero | int | No |
| Decimal | float | No |
| Complejo | complex | No |
| Booleano | bool | No |
| Texto | str | No |
| Bytes | bytes | No |
| Lista | list | Sí |
| Tupla | tuple | No |
| Diccionario | dict | Sí |
| Conjunto | set | Sí |

---

# 4.1 Enteros

```python
edad = 25
```

Consultar tipo.

```python
type(edad)
```

Resultado.

```text
<class 'int'>
```

---

## Operaciones

```python
print(edad + 10)

print(edad * 5)

print(edad ** 2)

print(edad // 3)

print(edad % 3)
```

---

> [!TIP]
> Python puede manejar enteros extremadamente grandes.

```python
numero = 10**100
```

No existe un límite práctico como ocurre en muchos otros lenguajes.

---

# 4.2 Números de punto flotante

```python
temperatura = 23.75
```

Tipo.

```python
type(temperatura)
```

Resultado.

```text
<class 'float'>
```

---

## Atención

Los números decimales no siempre pueden representarse exactamente.

Ejemplo.

```python
0.1 + 0.2
```

Resultado.

```text
0.30000000000000004
```

Esto no es un error de Python.

Es consecuencia del estándar IEEE-754 utilizado por prácticamente todos los lenguajes modernos.

---

> [!IMPORTANT]
> Nunca compares números decimales usando `==`.

Utiliza:

```python
import math

math.isclose(a, b)
```

---

# 4.3 Booleanos

Solo existen dos valores.

```python
True

False
```

Ejemplo.

```python
llueve = True

print(type(llueve))
```

---

## Curiosidad

```python
True + True
```

Resultado.

```text
2
```

¿Por qué?

Porque internamente:

```python
bool
```

hereda de

```python
int
```

Lo estudiaremos más adelante.

---

# 4.4 Texto

```python
nombre = "QGIS Bolivia"
```

Los textos son objetos de tipo:

```python
str
```

---

## Algunos métodos

```python
nombre.upper()

nombre.lower()

nombre.title()

nombre.replace()

nombre.split()
```

---

## Muy importante

Los textos son inmutables.

```python
texto = "agua"

texto.upper()
```

No modifica el texto original.

Devuelve un objeto nuevo.

---

# 4.5 Bytes

Cuando trabajemos con imágenes, archivos o redes veremos objetos:

```python
bytes
```

Ejemplo.

```python
b"Hola"
```

Más adelante veremos cómo QGIS utiliza bytes para almacenar imágenes y geometrías binarias (WKB).

---

# 🔬 Internamente (CPython)

Cada tipo de dato está implementado mediante una estructura escrita en C.

Por ejemplo:

```text
PyLongObject
```

implementa los enteros.

```text
PyFloatObject
```

implementa los flotantes.

```text
PyUnicodeObject
```

implementa las cadenas de texto.

No necesitamos conocer su implementación todavía, pero es importante saber que los tipos fundamentales no están escritos en Python, sino en C para ofrecer un alto rendimiento.

---

# 🌎 Aplicación SIG

Supongamos una estación hidrométrica.

```python
estacion = {
    "codigo": "HB-001",
    "rio": "Rocha",
    "caudal": 18.5,
    "activa": True
}
```

Cada dato tiene un tipo distinto.

```python
type(estacion["codigo"])

type(estacion["caudal"])

type(estacion["activa"])
```

Comprender estos tipos facilitará el manejo de atributos en capas vectoriales de QGIS.

---

# 🧠 ¿Sabías que...?

Python no limita el tamaño de un entero como C o Java.

Puedes escribir:

```python
10**1000
```

y Python seguirá funcionando correctamente.

---

# Rendimiento

Los tipos inmutables presentan varias ventajas:

- Mayor seguridad.
- Posibilidad de reutilización interna.
- Mejor optimización.

Por eso:

- `str`
- `int`
- `tuple`

son inmutables.

---

# Buenas prácticas

> [!TIP]
> Utiliza el tipo adecuado para representar cada dato.

> [!IMPORTANT]
> Comprender el tipo de un objeto permite descubrir automáticamente sus métodos.

---

# Laboratorio

## Ejercicio 1

Crear una variable de cada tipo fundamental.

Consultar:

```python
type(variable)
```

---

## Ejercicio 2

Utilizar:

```python
dir(variable)
```

para descubrir métodos.

---

## Ejercicio 3

Investigar:

```python
help(str.replace)
```

---

## Ejercicio 4

Crear un diccionario con información de una capa SIG.

Ejemplo.

```python
capa = {
    "EPSG": 32719,
    "Nombre": "Cuenca",
    "Area": 158.73,
    "Activa": True
}
```

Consultar el tipo de cada valor.

---

# Ideas clave

- Todo objeto posee un tipo.
- El tipo determina su comportamiento.
- Los enteros son inmutables.
- Los textos son inmutables.
- Las listas son mutables.
- Los diccionarios son mutables.
- `type()` permite identificar cualquier objeto.

---

# Errores frecuentes

❌ Comparar números flotantes utilizando `==`.

❌ Pensar que `upper()` modifica un texto.

❌ Confundir tipo con valor.

---

# Resumen

En este capítulo estudiamos los principales tipos de datos de Python.

Comprendimos que cada tipo define un comportamiento específico y que el conocimiento de estos tipos constituye la base para manipular información de forma segura y eficiente.

Estos conceptos serán utilizados continuamente al trabajar con listas, diccionarios, atributos de capas, geometrías y objetos de la API de QGIS.

---

# Próximo capítulo

**Capítulo 5 – Colecciones**

Aprenderemos a trabajar con:

- Listas
- Tuplas
- Diccionarios
- Conjuntos

También estudiaremos:

- Complejidad computacional.
- Rendimiento.
- Uso de memoria.
- Cuándo utilizar cada estructura.
- Aplicaciones prácticas en QGIS y PostGIS.
