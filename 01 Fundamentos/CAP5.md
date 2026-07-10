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
- Conserva las unidades cuando aporten claridad.
- Modela primero el problema y luego elige la colección adecuada.
