---
title: "6. Evaluar el sistema"
weight: 6
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

**Duración:** 20 min. **Al terminar:** puedes diseñar una comparación pequeña,
definir qué mide y localizar un fallo en la traza.

## ¿Qué significa que funcionó? · 4 min

Una eval ejecuta casos con entradas y criterios de aceptación definidos. Cada
ejecución es un intento; varias ejecuciones ayudan a observar variabilidad.

| Nivel | Pregunta | En el reporte |
|---|---|---|
| Selección | ¿Eligió la herramienta adecuada? | Consultar ventas, no inventar el total. |
| Argumentos | ¿Pasó los valores correctos? | Octubre de 2026, en la fuente indicada. |
| Secuencia | ¿Respetó dependencias? | Validar antes de aceptar o publicar. |
| Resultado | ¿Cumplió el objetivo? | Total correcto, unidad, fuente y límites. |

Una evaluación de tool calls puede pasar aunque la respuesta final sea incorrecta.
El [evaluador del taller de MCP](https://github.com/danteese/claude-mcp-ibero-2026/blob/main/evaluar.py)
mide elección y argumentos; su alcance no incluye la veracidad de toda la respuesta.

## Construir los casos antes del cambio · 4 min

Para el caso de ventas usamos seis situaciones:

1. Duplicado exacto y cancelación: calcular sin contarlos de más.
2. Duplicado con distinto importe: detener y señalar el conflicto.
3. Importe inválido: rechazarlo, sin convertirlo silenciosamente en cero.
4. Ventas válidas de importe cero: conservar el cero.
5. Mes ausente: distinguir «sin datos» de «cero ventas».
6. Pregunta causal: reconocer que el archivo no explica por qué cambió el total.

Las entradas y expectativas están en la [práctica](../07-practica/). Son un conjunto
pequeño de enseñanza, no una estimación de confiabilidad en producción.

## Quién califica · 4 min

| Evaluador | Útil para | Límite |
|---|---|---|
| Código | Totales, tipos, reglas y efectos observables. | Solo comprueba lo que implementaste. |
| Modelo con rúbrica | Claridad, fidelidad de una explicación o hallazgos difíciles de enumerar. | Puede equivocarse y necesita calibración. |
| Persona con conocimiento del caso | Requisitos ambiguos y decisiones del dominio. | Tiempo y variación entre revisores. |

No uses un juez de lenguaje para sumar lo que puedes calcular. Para evaluar prosa,
dale fuentes, una rúbrica y ejemplos calibrados; revisa una muestra de sus juicios.
Exige evidencia y permite «no se puede determinar». Un JSON del juez facilita
procesar su respuesta, pero no convierte el juicio en verdadero.

## Comparar antes y después · 5 min

1. Guarda el estado inicial del proyecto y la configuración.
2. Ejecuta los mismos casos con el mismo modelo y entorno.
3. Cambia **una intervención principal**: por ejemplo, el contrato de una tool.
4. Repite los casos; conserva entradas, resultados y trazas de ambas versiones.
5. Si el presupuesto alcanza, repite algunos casos para observar variabilidad.

Registra éxito, fallos, tiempo, intervención humana y consumo cuando esté disponible.
Si no conoces el costo, anota «no medido»; no lo infieras solo del número de llamadas.

Ejemplo **ficticio** para practicar la lectura de una comparación:

| Versión | Casos aprobados | Tiempo total | Intervenciones |
|---|---|---|---|
| Inicial | 3/6 | 2 min | 2 |
| Con validación | 5/6 | 3 min | 1 |

La segunda versión resuelve más de estos casos, pero tarda más. Una corrida pequeña
no demuestra superioridad general. Mantén el denominador: si una herramienta no
existe y omites un caso, regístralo como no ejecutado; no lo conviertas en un aprobado.

Cuando pases del taller a un proyecto real, añade casos representativos y un conjunto
de comprobación que no uses para ajustar continuamente la solución.

## Diagnosticar antes de añadir complejidad · 3 min

Busca el primer punto donde se pierde la evidencia o se toma una decisión incorrecta:

- No encontró el archivo → recuperación.
- Lo encontró pero perdió una restricción → contexto o compactación.
- Envió un mes equivocado → argumentos o interpretación.
- La herramienta calculó mal → código o datos.
- El dato era correcto pero la explicación inventó una causa → respuesta final.
- Repite una acción tras un timeout → estado y recuperación de la ejecución.

Pregunta al grupo: **«¿Qué cambiarías primero si llamó bien a la herramienta y luego
inventó una causa?»** La respuesta final y su evaluación; instalar otro MCP no
resuelve por sí mismo ese fallo.

**Transición:** en la práctica escogerás una tarea, observarás un fallo y medirás
una mejora. El resultado puede ser que tu cambio no ayudó: eso también es evidencia.

Fuentes: [CMU, Tool Use, pp. 54–56](https://www.cmu-agents.com/slides/lecture-02-tool-use.pdf),
[Demystifying evals for AI agents](https://www.anthropic.com/research/demystifying-evals-for-ai-agents)
y [Jésica Tapia, evals.py](https://github.com/JTapiaR/Evalmultiagente/blob/main/evals.py).
