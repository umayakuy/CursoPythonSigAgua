---
title: "Capítulo 1 - La Filosofía de Python"
book: "Python Moderno para Desarrolladores SIG"
chapter: 1
version: 1.0
status: Finalizado
author:
  - Jorge Ayala Niño de Guzmán
  - ChatGPT (OpenAI)
last_update: 2026-07-04
level: Fundamentos
estimated_time: "2 horas"
---

# Capítulo 1
# La Filosofía de Python

---

# Objetivos

Al finalizar este capítulo el lector será capaz de comprender:

- Por qué nació Python.
- Por qué QGIS utiliza Python como lenguaje de scripting.
- La filosofía del lenguaje.
- Qué es el Zen de Python.
- La diferencia entre lenguaje, intérprete y ecosistema.
- Qué ocurre cuando se ejecuta un programa Python.
- Qué es el bytecode.
- Cómo obtener información del intérprete instalado en QGIS.

---

# Conocimientos previos

Se recomienda tener conocimientos básicos de programación
(BASIC, Pascal, C, PHP u otro lenguaje).

No es necesario tener experiencia previa en Python.

---

# 1.1 ¿Por qué Python?

Python fue creado por Guido van Rossum en 1991 con un objetivo muy claro:

> Incrementar la productividad del programador.

Python no fue diseñado para ser el lenguaje más rápido.

Fue diseñado para que el código sea:

- legible
- sencillo
- mantenible
- expresivo

Estas características explican por qué fue adoptado por proyectos como:

- QGIS
- Blender
- FreeCAD
- Django
- Flask
- TensorFlow
- PyTorch

---

# 1.2 ¿Por qué QGIS utiliza Python?

QGIS está desarrollado principalmente en C++.

Sin embargo, escribir extensiones en C++ implica:

- mayor complejidad
- tiempos de desarrollo más largos
- recompilación

Python permite desarrollar herramientas y complementos de forma mucho más rápida.

La combinación C++ + Python ofrece un excelente equilibrio entre rendimiento y productividad.

---

# 1.3 El Zen de Python

Ejecute:

```python
import this
```

Aparecerá el Zen de Python.

Algunos principios fundamentales son:

- Beautiful is better than ugly.
- Explicit is better than implicit.
- Simple is better than complex.
- Readability counts.

Estos principios estarán presentes durante todo este curso.

---

# 1.4 Python es un ecosistema

Python no es únicamente un lenguaje.

Está compuesto por:

- Lenguaje
- Intérprete
- Biblioteca estándar
- Gestor de paquetes
- Miles de librerías externas

---

# 1.5 ¿Qué ocurre al ejecutar un programa?

Cuando escribimos:

```python
print("Hola")
```

Python no ejecuta directamente esa línea.

El proceso simplificado es:

```
Código fuente

↓

Intérprete Python

↓

Bytecode

↓

Máquina Virtual Python

↓

Sistema Operativo

↓

Hardware
```

Este proceso será estudiado con mayor profundidad en capítulos posteriores.

---

# 1.6 El intérprete de QGIS

QGIS incorpora su propia instalación de Python.

Esto permite ejecutar scripts sin necesidad de instalar Python por separado.

Para conocer la versión instalada:

```python
import sys

print(sys.version)
```

Para conocer el ejecutable utilizado:

```python
print(sys.executable)
```

Para conocer dónde busca módulos Python:

```python
print(sys.path)
```

---

# Aplicación al proyecto INFO-SIPEB

El script analizado durante este curso se ejecuta completamente sobre el intérprete Python incluido en QGIS.

Por esta razón puede utilizar simultáneamente:

- Biblioteca estándar
- Librerías externas (requests)
- API de QGIS
- PyQt

---

# Laboratorio

Ejecutar en la consola Python de QGIS:

```python
import this
```

```python
import sys

print(sys.version)
```

```python
print(sys.executable)
```

```python
print(sys.path)
```

Analizar la salida obtenida.

---

# Ideas clave

- Python fue creado para aumentar la productividad.
- QGIS utiliza Python porque permite desarrollar herramientas rápidamente.
- Python es un ecosistema completo.
- El código fuente se transforma en bytecode antes de ejecutarse.
- QGIS incorpora su propio intérprete Python.

---

# Errores frecuentes

❌ Creer que Python es únicamente un programa.

❌ Pensar que QGIS utiliza el Python instalado por el usuario.

❌ Memorizar funciones sin comprender los objetos que las implementan.

---

# Resumen

En este capítulo se presentó la filosofía de Python y el motivo por el cual constituye el lenguaje de automatización de QGIS.

También se introdujo el concepto de ecosistema Python, el papel del intérprete y el flujo general de ejecución de un programa.

Estos conceptos servirán como base para comprender la programación orientada a objetos y la arquitectura interna de Python.

---

# Frase para recordar

> **"En Python, una línea de código nunca es solo una línea; detrás de ella existe un intérprete, objetos y un ecosistema completo trabajando para ti."**

---

# Próximo capítulo

**Capítulo 2 — El Universo de los Objetos**

Comprenderemos qué es realmente un objeto, qué ocurre en memoria cuando escribimos:

```python
x = 10
```

Este capítulo marcará el cambio de paradigma entre la programación tradicional y Python moderno.
