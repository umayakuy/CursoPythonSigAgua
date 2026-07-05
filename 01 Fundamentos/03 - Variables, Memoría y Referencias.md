---
title: "Capítulo 3 - Variables, Memoria y Referencias"
book: "Python Moderno para Desarrolladores SIG"
chapter: 3
version: 1.0
status: En desarrollo
author:
  - Jorge Ayala Niño de Guzmán
  - ChatGPT (OpenAI)
last_update: 2026-07-04
level: Fundamentos
estimated_time: "6 horas"
prerequisites:
  - Capítulo 2 - El Universo de los Objetos
---

# Capítulo 3

# Variables, Memoria y Referencias

---

# Bitácora del Ingeniero

Durante años observé el mismo error en cursos de programación.

Muchos estudiantes pensaban que una variable "guardaba" un dato.

En Python esa idea no es correcta.

Las variables simplemente mantienen una referencia hacia un objeto existente.

Comprender esta diferencia evitará muchos errores cuando trabajemos con listas, diccionarios, objetos de QGIS y estructuras complejas.

---

# Objetivos

Al finalizar este capítulo serás capaz de:

- Comprender cómo administra la memoria Python.
- Diferenciar objeto y referencia.
- Comprender el concepto de mutabilidad.
- Comprender la identidad de un objeto.
- Entender el contador de referencias.
- Comprender el funcionamiento básico del recolector de basura.

---

# 3.1 ¿Qué es una variable?

En muchos lenguajes tradicionales se enseña que una variable es "una caja donde se guarda información".

Esta idea resulta útil para comenzar, pero en Python no describe correctamente lo que ocurre.

Una definición más precisa sería:

> Una variable es un nombre que referencia un objeto existente en memoria.

---

# Veamos un ejemplo

```python
x = 25
```

Muchos imaginan:

```text
┌───────┐
│   x   │
├───────┤
│  25   │
└───────┘
```

Python realmente hace algo más parecido a esto.

```text
          x
          │
          ▼

   ┌───────────────┐
   │     int       │
   │---------------│
   │ Valor : 25    │
   └───────────────┘
```

La variable únicamente apunta al objeto.

---

# 3.2 Referencias

Ahora escribamos:

```python
a = 25
b = a
```

En memoria ocurre:

```text
        a
         │
         │
         ▼

   ┌───────────────┐
   │     int       │
   │---------------│
   │ Valor : 25    │
   └───────────────┘
         ▲
         │
         │
        b
```

Existe un único objeto.

Dos variables lo referencian.

---

# Laboratorio 1

Ejecute:

```python
a = 25
b = a

print(id(a))
print(id(b))
```

Ambos muestran la misma identidad.

---

# 3.3 Cambiando una referencia

Ahora escriba:

```python
a = 100

print(a)
print(b)

print(id(a))
print(id(b))
```

Resultado esperado:

```text
100
25
```

Python creó un objeto nuevo.

```text
a ─────────► 100

b ─────────► 25
```

No modificó el objeto anterior.

---

# 3.4 Objetos mutables e inmutables

Aquí aparece un concepto extremadamente importante.

Existen dos grandes categorías.

## Objetos inmutables

Nunca cambian.

Ejemplos:

- int
- float
- bool
- str
- tuple

Cuando parecen cambiar, Python crea un objeto nuevo.

---

## Objetos mutables

Sí pueden modificarse.

Ejemplos:

- list
- dict
- set

Aquí comienzan muchos errores de programación.

---

# Ejemplo

```python
lista1 = [10,20,30]

lista2 = lista1
```

En memoria.

```text
            lista1
               │
               ▼

      ┌────────────────┐
      │ 10 │20 │30 │
      └────────────────┘
               ▲
               │
            lista2
```

Ahora:

```python
lista2.append(40)
```

¿Qué ocurre?

Muchos esperan:

```text
lista1

10 20 30
```

Pero realmente obtenemos:

```text
lista1

10 20 30 40
```

¿Por qué?

Porque ambas variables apuntan exactamente al mismo objeto.

---

# Laboratorio 2

Ejecute.

```python
lista1 = [10,20,30]

lista2 = lista1

lista2.append(40)

print(lista1)

print(lista2)
```

Analice cuidadosamente el resultado.

---

# 3.5 ¿Cómo copiar correctamente una lista?

Si realmente queremos una copia.

```python
lista2 = lista1.copy()
```

Ahora existen dos objetos diferentes.

```text
lista1 ─────► [10 20 30]

lista2 ─────► [10 20 30]
```

Cada uno puede modificarse independientemente.

---

# 3.6 Contador de referencias

Python mantiene internamente un contador.

Cada vez que una variable apunta hacia un objeto.

El contador aumenta.

Cuando una variable deja de apuntar.

El contador disminuye.

Cuando llega a cero.

El objeto puede eliminarse de memoria.

Este mecanismo recibe el nombre de:

**Reference Counting**

---

# 3.7 Recolector de basura

Algunos objetos forman ciclos de referencias.

En estos casos el contador no es suficiente.

Python incorpora un segundo mecanismo.

El **Garbage Collector**.

Su objetivo es detectar objetos que ya no pueden utilizarse y liberar la memoria.

En capítulos posteriores estudiaremos el módulo `gc`.

---

# Aplicación SIG

Supongamos.

```python
layer = iface.activeLayer()

otra = layer
```

Ambas variables apuntan exactamente a la misma capa.

Si modificamos propiedades mediante una referencia.

La otra también observará los cambios.

Este comportamiento resulta fundamental cuando trabajemos con la API de QGIS.

---

# Buenas prácticas

> [!TIP]
> Antes de copiar una lista pregúntese si necesita una referencia o una copia independiente.

> [!IMPORTANT]
> Comprender referencias evita algunos de los errores más frecuentes en Python.

---

# Errores frecuentes

❌ Pensar que `=` siempre crea una copia.

❌ Modificar listas creyendo que son independientes.

❌ Confundir identidad con igualdad.

---

# Laboratorio

1. Comparar `id()` de enteros.

2. Comparar `id()` de listas.

3. Crear dos referencias a un diccionario.

4. Modificar una referencia.

5. Analizar el resultado.

6. Repetir utilizando `.copy()`.

---

# Ideas clave

- Una variable no almacena un objeto.
- Una variable referencia un objeto.
- `=` no significa copiar.
- Existen objetos mutables e inmutables.
- Las listas son mutables.
- Los enteros son inmutables.
- Python utiliza un contador de referencias.
- Python incorpora un recolector de basura.

---

# Resumen

En este capítulo aprendimos cómo administra Python las referencias a los objetos.

Comprendimos la diferencia entre crear una nueva referencia y crear una copia independiente.

También introdujimos los conceptos de mutabilidad, contador de referencias y recolección de basura.

Estos conceptos serán esenciales para comprender el comportamiento de listas, diccionarios y objetos complejos utilizados por QGIS.

---

# Próximo capítulo

**Capítulo 4 — Tipos de Datos**

Estudiaremos en profundidad los tipos fundamentales de Python:

- int
- float
- bool
- str
- bytes

Comprenderemos cómo están implementados, por qué existen y cómo utilizarlos eficientemente.
