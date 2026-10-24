# Coding agents

Del pedido al cambio comprobado.

Avanzado · 4 de 6 · 25 min

---

## Una spec breve

Problema · entradas · resultado · restricciones · aceptación

Reporte: septiembre **1500**, octubre **2000 MXN**.

Completadas, sin duplicados. Conflictos: detener.

Datos sintéticos del caso normal.

---

## Localizar → editar → verificar

Encuentra el comportamiento y reproduce el fallo.

Haz un cambio pequeño; revisa el diff.

Comprueba la reparación y las regresiones.

---

## TDD

Prueba de comportamiento → falla → implementación → pasa.

El fallo debe ocurrir por la razón esperada.

Los resultados esperados vienen de la spec.

---

## Cero es un valor

Ejemplo ilustrativo:

```python
importe = valor or importe_por_defecto
```

¿Qué sucede si `valor` es `0`?

---

## Pruebas en distintas capas

Unidad → una regla.

Integración → piezas conectadas.

Extremo a extremo → resultado de la tarea.

Interfaz → comportamiento y render, si existe.

---

## Dos comprobaciones

**Fallaba → pasa:** se reparó el problema.

**Pasaba → sigue pasando:** conservamos comportamiento.

Código y pruebas pueden compartir una suposición equivocada.

---

## Reviewer adversarial

Requisitos + diff + acceso a pruebas.

Hallazgo = condición + efecto + evidencia.

Una hipótesis se marca como hipótesis.

No pidas una cuota de errores.

---

## ¿Aceptamos el hallazgo?

El reviewer propone cambiar la fórmula.

Primero: contrastar la regla y reproducir el fallo.

Después: corregir y volver a probar.
