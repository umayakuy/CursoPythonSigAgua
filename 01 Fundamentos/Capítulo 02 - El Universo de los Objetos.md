---
title: "Capítulo 2 - El Universo de los Objetos"
book: "Python Moderno para Desarrolladores SIG"
chapter: 2
version: 1.0
status: En desarrollo
author:
  - Jorge Ayala Niño de Guzmán
  - ChatGPT (OpenAI)
last_update: 2026-07-04
level: Fundamentos
estimated_time: "5 horas"
prerequisites:
  - Capítulo 1 - La Filosofía de Python
---

# Capítulo 2
# El Universo de los Objetos

> **"Todo en Python es un objeto."**

Esta es probablemente la frase más repetida cuando se habla de Python. Sin embargo, también es una de las menos comprendidas.

En este capítulo construiremos una comprensión sólida de este concepto, ya que será la base para entender todo el lenguaje, desde un número entero hasta una capa de QGIS (`QgsVectorLayer`).

---

# Objetivos

Al finalizar este capítulo serás capaz de:

- Comprender qué es un objeto.
- Diferenciar una clase de una instancia.
- Comprender qué es una referencia.
- Identificar la identidad de un objeto.
- Explorar cualquier objeto mediante introspección.
- Comprender por qué Python se considera un lenguaje orientado a objetos.

---

# Conocimientos previos

Se recomienda haber estudiado:

- Capítulo 1 – La Filosofía de Python

No se requieren conocimientos previos de programación orientada a objetos.

---

# 2.1 ¿Qué es un objeto?

Antes de escribir una sola línea de código debemos responder una pregunta fundamental.

> **¿Qué es un objeto?**

Una definición frecuente es:

> "Un objeto es una instancia de una clase."

Aunque técnicamente es correcta, resulta poco útil para quien está comenzando.

Veamos una analogía.

## Ejemplo: una estación meteorológica

Supongamos que una empresa fabrica estaciones meteorológicas.

Existe un plano de fabricación.

Ese plano especifica:

- sensores
- pantalla
- memoria
- batería
- comunicaciones

Ese plano **no mide temperatura**.

Simplemente describe cómo construir una estación.

Ese plano representa una **clase**.

Cuando fabricamos una estación física obtenemos un objeto real.

Cada estación tendrá:

- número de serie
- temperatura
- humedad
- presión

Cada una será diferente de las demás.

Cada estación será una **instancia** de esa clase.

---

# 2.2 En Python ocurre exactamente lo mismo

Cuando escribimos:

```python
x = 10
```

Python crea un objeto de tipo entero.

Podemos comprobarlo.

```python
x = 10

print(type(x))
```

Resultado:

```text
<class 'int'>
```

El objeto pertenece a la clase `int`.

---

# 2.3 Todo objeto posee tres propiedades fundamentales

Todo objeto en Python posee:

1. Identidad
2. Tipo
3. Valor

## Identidad

Cada objeto posee una identidad única.

Podemos consultarla mediante:

```python
id(x)
```

El valor obtenido representa la identidad del objeto durante su existencia.

---

## Tipo

El tipo indica la clase a la que pertenece el objeto.

```python
type(x)
```

Resultado:

```text
<class 'int'>
```

---

## Valor

En este caso:

```text
10
```

Podemos representar gráficamente un objeto como:

```text
┌─────────────────────────────┐
│ Tipo : int                  │
│ Valor: 10                   │
│ ID   : 140298472...         │
└─────────────────────────────┘
```

---

# 2.4 Variables y referencias

Aquí aparece uno de los conceptos más importantes del lenguaje.

Escribamos:

```python
x = 10
y = x
```

Muchos programadores imaginan:

```text
x = 10

y = 10
```

Sin embargo, Python funciona de otra manera.

```text
        x
         │
         │
         ▼

   ┌──────────────┐
   │     int      │
   │--------------│
   │ Valor: 10    │
   └──────────────┘
         ▲
         │
         │
        y
```

Las variables **no contienen** el objeto.

Las variables simplemente **apuntan** al objeto.

---

# Laboratorio 1

Ejecute el siguiente código.

```python
x = 10
y = x

print(id(x))
print(id(y))
```

Observe que ambos muestran la misma identidad.

---

# 2.5 Cambiando una referencia

Ahora ejecutemos:

```python
x = 99

print(x)
print(y)

print(id(x))
print(id(y))
```

Resultado esperado:

```text
99
10
```

Python no modificó el objeto anterior.

Creó un nuevo objeto y cambió la referencia de `x`.

```text
x ─────────► 99

y ─────────► 10
```

---

# 2.6 Descubriendo objetos

Una de las mayores fortalezas de Python es la introspección.

Supongamos:

```python
texto = "QGIS Bolivia"
```

Podemos preguntar:

```python
type(texto)
```

Después:

```python
dir(texto)
```

Y finalmente:

```python
help(texto.replace)
```

Estas tres funciones serán utilizadas durante todo el libro.

---

# 2.7 La regla del desarrollador profesional

Cuando conozcas una librería nueva sigue siempre estos pasos.

## Paso 1

¿Qué es?

```python
type(objeto)
```

---

## Paso 2

¿Qué sabe hacer?

```python
dir(objeto)
```

---

## Paso 3

¿Cómo funciona?

```python
help(objeto.metodo)
```

Con estas tres herramientas podrás explorar cualquier biblioteca Python.

---

# Aplicación SIG

Supongamos que existe una capa activa.

```python
layer = iface.activeLayer()
```

Podemos inspeccionarla.

```python
print(type(layer))
```

Luego:

```python
print(dir(layer))
```

Y finalmente:

```python
help(layer.featureCount)
```

De esta forma descubrimos la API de QGIS sin memorizar documentación.

---

# Buenas prácticas

> [!TIP]
> Acostúmbrate a ejecutar `type()`, `dir()` y `help()` cada vez que trabajes con una nueva biblioteca.

> [!IMPORTANT]
> Comprender los objetos es mucho más importante que memorizar funciones.

---

# Errores frecuentes

❌ Pensar que una variable almacena un objeto.

❌ Confundir clase con objeto.

❌ Memorizar métodos sin comprender qué objeto los implementa.

---

# Laboratorio

1. Crear un entero y consultar su tipo.
2. Crear un texto y listar sus métodos.
3. Crear una lista y explorar sus métodos.
4. Obtener la capa activa de QGIS e inspeccionarla.
5. Investigar qué métodos públicos posee `QgsVectorLayer`.

---

# Ideas clave

- Todo en Python es un objeto.
- Todo objeto posee identidad.
- Todo objeto posee tipo.
- Todo objeto posee valor.
- Las variables apuntan a objetos.
- `type()` responde qué es un objeto.
- `dir()` muestra sus métodos.
- `help()` explica cómo funciona.

---

# Resumen

En este capítulo aprendimos que Python está completamente construido alrededor del concepto de objeto.

Comprendimos que una variable no almacena directamente un valor, sino que referencia un objeto en memoria.

También conocimos las herramientas de introspección (`type()`, `dir()` y `help()`), que nos permitirán explorar cualquier API, incluida la de QGIS.

Este conocimiento será esencial para comprender el comportamiento de listas, diccionarios, funciones, módulos y todas las clases que utilizaremos a lo largo del libro.

---

# Próximo capítulo

**Capítulo 3 – Variables, Memoria y Referencias**

En el siguiente capítulo estudiaremos qué ocurre realmente en memoria cuando dos variables apuntan al mismo objeto.

Comprenderemos conceptos como:

- memoria
- referencias
- mutabilidad
- inmutabilidad
- contador de referencias
- recolector de basura

Estos conceptos explican muchos de los errores más comunes al trabajar con listas, diccionarios y objetos de QGIS.
