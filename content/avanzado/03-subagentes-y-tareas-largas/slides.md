# Subagentes y tareas largas

Delegar, conservar evidencia y continuar.

Avanzado · 3 de 6 · 15 min

---

## Otra ejecución, otro contexto

Un subagente recibe un encargo y devuelve un resultado.

Comprueba qué contexto y herramientas hereda.

Menos contexto en el principal no implica menos tokens totales.

---

## Un encargo completo

Objetivo · entradas · permisos · formato de salida · terminado

«Revisa duplicados, importes y estados.
No edites. Devuelve id, evidencia y efecto.»

---

## ¿Delegar?

Sí: exploración extensa, tareas independientes, revisión separada.

Cuidado: mismos archivos, dependencias continuas,
traspasos que pierden información.

---

## Review independiente

Requisitos + diff + acceso a pruebas.

Cada hallazgo necesita evidencia.

Otro contexto reduce anclaje; otro modelo aporta diversidad.
Ninguno garantiza ausencia de sesgos.

---

## Goal, plan y estado

**Goal:** resultado esperado.

**Plan:** pasos propuestos.

**Estado:** lo comprobado, lo pendiente y la evidencia.

Añade presupuesto y condición de bloqueo.

---

## Qué debe sobrevivir

Exactos: objetivo, restricciones, identificadores.

Resumidos: decisiones y progreso.

Recuperables: fuentes y logs.

Prueba: ¿una sesión nueva continúa correctamente?
