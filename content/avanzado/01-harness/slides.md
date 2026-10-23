# Anatomía del harness

Mismo modelo, distinto sistema, distinto resultado.

Avanzado · 1 de 6 · 15 min

---

## ¿Qué cambia alrededor del modelo?

- Lo que recibe como contexto.
- Las herramientas que puede solicitar.
- Los permisos y controles.
- Cómo conserva estado y cuándo termina.

Nos enfocamos en los **harnesses**.

---

## Modelo, agente, harness

**Modelo:** produce respuestas o solicitudes.

**Agente:** modelo + herramientas + ciclo orientado a un objetivo.

**Harness:** prepara, ejecuta, conserva estado y controla el ciclo.

---

## Flujo agéntico

Leer → validar → calcular → explicar → revisar

Algunos pasos los decide el modelo.

Otros quedan fijados en código.

---

## Quién hace qué

Traza didáctica:

```text
Modelo   → solicita leer ventas.csv
Harness  → ejecuta y devuelve datos
Modelo   → solicita calcular totales
Harness  → ejecuta y devuelve 1500, 2000
Modelo   → redacta la comparación
```

---

## Disponible no significa leído

La carpeta contiene lo que puede consultar.

El contexto contiene lo que recibe en esta llamada.

El harness conecta ambos.

---

## Construir y ejecutar

Un coding agent puede escribir el programa del reporte.

El programa puede calcular sin un modelo.

Elige dónde necesitas criterio y dónde un procedimiento fijo.

---

## «Ya guardé el reporte»

El archivo no existe.

¿Qué revisarías en la traza?

Solicitud → ejecución → resultado → ruta.
