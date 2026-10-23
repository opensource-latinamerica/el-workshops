# Contexto y herramientas

¿Qué necesita ver y poder hacer?

Avanzado · 2 de 6 · 25 min

---

## ¿Qué le falta?

| Necesita | Pieza |
|---|---|
| Convenciones | Instrucciones persistentes |
| Procedimiento | Skill |
| Cálculo repetible | Script / CLI |
| Capacidades de un servicio | API / MCP |
| Evidencia | Recuperación |

---

## Skill y tool

**Skill:** enseña un procedimiento.

**Tool:** permite ejecutar una operación.

La skill puede incluir un script.
El harness necesita una herramienta para ejecutarlo.

---

## CLI, API y MCP

CLI: comandos.

API: interfaz de programación.

MCP: comunicación estándar entre cliente y servidor.

Pueden exponer la misma capacidad.

---

## Un contrato útil

```text
ventas_del_mes("2026-10")
→ total_mxn: "2000.00"
  fuente: ventas.csv
  regla: completadas; sin duplicados
```

Intención clara · resultado acotado · error accionable.

---

## ¿Qué llena el contexto?

Instrucciones · herramientas · historial · evidencia

Compactar el historial no elimina
las definiciones de herramientas.

---

## Cuatro intervenciones

- Compactar historial.
- Guardar fuera y recuperar fragmentos.
- Descubrir herramientas bajo demanda.
- Delegar una investigación acotada.

Cada una cambia una parte distinta.

---

## Recuperación

Identificador exacto → búsqueda textual.

Importes y fechas → consultas y cálculo.

Conceptos con otras palabras → evaluar búsqueda semántica.

RAG no exige una base vectorial.

---

## Decide dónde resolverlo

«Cómo redactar el reporte cada mes»

«Qué fórmula calcula las ventas»

«Dónde está la política de cancelaciones»

¿Skill, código o recuperación?
