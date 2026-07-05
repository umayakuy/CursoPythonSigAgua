---
title: "Capítulo 2 - Todo es un Objeto"
book: "Python Moderno para Desarrolladores SIG"
subtitle: "Fundamentos, Arquitectura y Desarrollo Profesional con QGIS, PostGIS, PyQt e Inteligencia Artificial"
edition: "Primera Edición"
version: "2.0"
module: "Módulo I - Fundamentos"
chapter: 2
status: "En desarrollo"
authors:
  - Jorge Ayala Niño de Guzmán
  - ChatGPT (OpenAI)
license: "CC BY-SA 4.0"
last_update: "2026-07-04"
---

# Capítulo 2

# Todo es un Objeto

---

# Ruta del Conocimiento

```text
                     PYTHON MODERNO PARA DESARROLLADORES SIG

MÓDULO I — FUNDAMENTOS

✅ Capítulo 1  La Filosofía de Python

✅ Capítulo 2  Todo es un Objeto     ← Usted está aquí

⬜ Capítulo 3  Variables, Memoria y Referencias

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
| Duración | 5 horas |
| Dificultad | ⭐⭐☆☆☆ |
| Laboratorios | 4 |
| Ejercicios | 10 |
| Proyecto AQUA-SIG | Primer modelo de objetos |


---

# Bitácora del Ingeniero

Durante muchos años programé pensando que una variable era una caja donde se guardaban datos.

Python me obligó a abandonar esa idea.

Aquí descubriremos que una variable no contiene un objeto; únicamente conoce dónde encontrarlo.

Comprender este concepto evitará muchos errores cuando trabajemos con listas, diccionarios, clases y objetos de QGIS.

---

# 🎯 ¿Por qué aprender esto?

Porque toda la API de Python está construida sobre objetos.

QGIS está formado por objetos.

PyQt está formado por objetos.

PostGIS devuelve objetos.

GeoPandas trabaja con objetos.

Si comprendes este capítulo, comprenderás el resto del libro.

---

# ¿Qué significa "Todo es un objeto"?

En Python prácticamente todo es un objeto.

Por ejemplo:

```python
10
```

es un objeto.

```python
3.1416
```

también es un objeto.

Una cadena de texto:

```python
"Hola"
```

es un objeto.

Una lista:

```python
[1,2,3]
```

también es un objeto.

Incluso una función.

```python
print
```

es un objeto.

Y una clase también.

---

# Primer experimento

Escribamos:

```python
x = 25
```

¿Qué ocurrió?

Muchos pensarán:

> Se guardó el número 25 dentro de x.

En realidad ocurrió algo diferente.

```
Nombre

x
│
│
▼

Objeto entero

+------+
|  25  |
+------+
```

`x` no contiene el número.

`x` apunta al objeto.

---

# Comprobándolo

Python posee una función llamada `id()`.

```python
x = 25

print(id(x))
```

Resultado aproximado:

```
140218513668400
```

Ese número identifica al objeto en memoria durante la ejecución del programa.

---

# Todo tiene un tipo

```python
x = 25

print(type(x))
```

Resultado:

```text
<class 'int'>
```

El objeto sabe de qué tipo es.

---

# Un objeto tiene tres características

Todo objeto posee:

- una identidad;
- un tipo;
- un valor.

Podemos representarlo así:

```
Objeto

+-----------------------+
| Tipo      int         |
| Valor      25         |
| ID      140218...     |
+-----------------------+
```

---

# 🔬 Internamente (CPython)

CPython representa todos los objetos mediante una estructura interna denominada `PyObject`.

De forma simplificada:

```text
PyObject

+----------------------+
| Reference Count      |
| Pointer al Tipo      |
+----------------------+
```

A partir de esta estructura básica se construyen enteros, cadenas, listas, diccionarios y cualquier otro objeto del lenguaje.

Comprender este diseño nos ayudará más adelante a entender el manejo de memoria y el recolector de basura.

---

# Métodos

Como los objetos conocen su tipo, también conocen las operaciones que pueden realizar.

Por ejemplo:

```python
texto = "python"

texto.upper()
```

Resultado:

```text
PYTHON
```

No estamos llamando a una función cualquiera.

Estamos pidiendo al objeto `texto` que ejecute uno de sus métodos.

---

# 🌎 Aplicación SIG

En QGIS una capa vectorial también es un objeto.

```python
capa = iface.activeLayer()
```

La variable `capa` no contiene la capa.

Contiene una referencia a un objeto de tipo:

```python
QgsVectorLayer
```

Ese objeto ofrece métodos como:

```python
capa.name()

capa.featureCount()

capa.isEditable()

capa.geometryType()
```

Observa que la forma de trabajar es exactamente igual que con una cadena de texto.

---

# 🏗️ Diseño de Software

Comenzaremos a construir el proyecto AQUA-SIG utilizando objetos.

Por ahora representaremos una capa mediante un diccionario.

```python
capa = {
    "nombre": "Red de Agua",
    "tipo": "Vector",
    "epsg": 32719
}
```

Más adelante este diccionario evolucionará hasta convertirse en una clase.

Finalmente será reemplazado por un objeto real de la API de QGIS.

Esta evolución permitirá comprender cómo un modelo simple puede transformarse en una arquitectura profesional.

---

# Laboratorio 1

Crear objetos de diferentes tipos.

```python
numero = 25
temperatura = 18.7
nombre = "Rocha"
activo = True
```

Mostrar para cada uno:

- tipo;
- identidad (`id()`);
- representación (`print()`).

---

# Laboratorio 2

Crear una lista con nombres de ríos.

Comprobar:

```python
type()

id()

len()
```

---

# Laboratorio 3

Crear un diccionario que represente una estación hidrométrica.

---

# Laboratorio 4

En la consola de Python de QGIS:

```python
iface.activeLayer()
```

Consultar:

```python
type(capa)
```

Explorar los métodos disponibles utilizando:

```python
dir(capa)
```

---

# 💡 Consejo del Ingeniero

Cuando aprendas un nuevo objeto, no memorices únicamente sus métodos.

Pregúntate siempre:

- ¿Qué representa?
- ¿Qué información almacena?
- ¿Qué operaciones puede realizar?
- ¿Cómo se relaciona con otros objetos?

Pensar en objetos significa modelar correctamente el problema antes de escribir una sola línea de código.

---

# Errores frecuentes

❌ Creer que una variable almacena un objeto.

❌ Confundir identidad con valor.

❌ Pensar que todos los objetos poseen los mismos métodos.

❌ Modificar un objeto sin comprender que otras variables pueden estar apuntando al mismo lugar de memoria.

---

# Resumen

En este capítulo descubrimos una de las ideas fundamentales de Python:

> Todo es un objeto.

Comprendimos que una variable es simplemente un nombre asociado a un objeto, y que cada objeto posee una identidad, un tipo y un valor.

Este modelo será la base para entender la memoria, las referencias, la orientación a objetos y el funcionamiento interno de bibliotecas como QGIS, PyQt y GeoPandas.

---

# Lo aprendido hoy

Ahora sabes que:

- una variable no contiene el objeto;
- un objeto tiene identidad, tipo y valor;
- los métodos pertenecen a los objetos;
- la API de QGIS está formada por objetos;
- este concepto acompañará todo el desarrollo del proyecto AQUA-SIG.

---

# Lo que construiremos mañana

En el siguiente capítulo responderemos una pregunta que genera mucha confusión entre quienes vienen de otros lenguajes:

> **¿Qué ocurre realmente cuando escribimos `a = b`?**

Analizaremos la memoria, las referencias y el ciclo de vida de los objetos para comprender cómo Python gestiona la información.

---

# Bibliografía recomendada

## Documentación oficial

- Python Software Foundation. *Data Model*.
- Python Software Foundation. *Built-in Types*.

## Libros

- Luciano Ramalho. *Fluent Python*.
- Brett Slatkin. *Effective Python*.
- David Beazley. *Python Cookbook*.
- Mark Lutz. *Learning Python*.

---

> **"En Python no programamos manipulando variables; programamos estableciendo relaciones entre objetos. Comprender esa diferencia cambia por completo la forma de desarrollar software."**
