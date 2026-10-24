---
title: "3. Subagentes y tareas largas"
weight: 3
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

**Duración:** 15 min. **Al terminar:** puedes formular una delegación verificable
y dejar el estado necesario para continuar una tarea.

## Qué es un subagente · 3 min

Un subagente es una ejecución delegada con su propio contexto de trabajo. Según el
harness puede usar el mismo modelo u otro, tener otras herramientas y recibir una
selección del contexto del principal. No asumas que empieza sin información heredada:
hay que mirar qué le entrega el sistema.

Sirve para explorar muchos archivos sin incorporar todo su contenido a la conversación
principal, resolver subtareas independientes o revisar un resultado con menos anclaje
a las decisiones de quien lo produjo.

Mantener pequeña la conversación principal **no garantiza menos tokens en total**:
también pagas el trabajo de los subagentes. Una revisión separada tampoco queda libre
de sesgos. Otro modelo añade diversidad, pero puede compartir errores.

## El contrato de delegación · 4 min

Ejemplo de encargo que puedes adaptar:

```text
Revisa la calidad de ventas.csv con las reglas de reglas.txt.
Puedes leer archivos; no modifiques los datos ni el programa.
Busca duplicados, importes inválidos y estados desconocidos.
Devuelve: problema, id o fila, evidencia y efecto en el reporte.
Si no encuentras problemas, dilo; no inventes una cuota de hallazgos.
Termina cuando hayas comprobado esas tres categorías.
```

El principal conserva la tarea global. Si delega por mes, debe comunicar a ambos
agentes las reglas comunes de moneda y deduplicación. Hay restricciones que cruzan
las subtareas: dos resultados correctos por separado pueden ser incompatibles al juntarlos.

| Delegación útil | Señal para trabajar en una sola ejecución |
|---|---|
| Investigar fuentes independientes | Un paso necesita inmediatamente lo que descubre el anterior. |
| Revisar un diff y reproducir un fallo | El traspaso requiere explicar casi toda la conversación. |
| Explorar una parte grande del repo | Los agentes editarían los mismos archivos sin coordinación. |

> **Para quien presenta:** pide que alguien añada al encargo una condición de
> terminado. Comprueba que no sea «revísalo bien», sino algo observable.

## Goals, plan y estado · 4 min

Un **goal** expresa qué resultado buscamos. El **plan** propone pasos. El **estado**
registra qué pasó realmente, qué falta y dónde está la evidencia. Algunos harnesses
ofrecen funciones específicas de goals; el nombre y la persistencia no son universales.

Para una tarea larga, necesitamos:

- Resultado esperado y evidencia de aceptación.
- Presupuesto de tiempo, pasos o consumo, según lo que puedas controlar.
- Condición de bloqueo: falta información, permiso o un servicio imprescindible.
- Punto de reanudación y referencias a archivos o resultados.

«Sigue hasta terminar» no define qué hacer si el agente se repite o no progresa.
Un goal debe poder acabar en **logrado**, **bloqueado** o **límite alcanzado**, según
las reglas del sistema. Una declaración de logrado necesita comprobación.

Un registro breve para retomar nuestro reporte:

```text
Objetivo: comparar septiembre y octubre en MXN.
Reglas: solo completadas; deduplicar por id; conflicto = detener.
Hecho: revisados los datos; detectada una copia exacta de V004.
Evidencia: ventas.csv y reglas.txt.
Pendiente: calcular, probar y redactar.
Siguiente paso: ejecutar el cálculo; no atribuir causas al aumento.
```

Este registro es un ejemplo didáctico. En una ejecución real añade rutas concretas,
resultados de comprobación y versión del trabajo. Un archivo de estado no reanuda
automáticamente el programa: el harness tiene que recuperarlo y saber cómo continuar.

## Compactar y continuar · 2 min

Conserva exactos el objetivo, restricciones e identificadores. Resume decisiones y
progreso. Deja fuera los logs extensos con una referencia que permita recuperarlos.
Mantén los resultados recientes necesarios para el siguiente paso.

La prueba de un buen resumen es **continuar correctamente**, no que suene completo.
Los resúmenes sucesivos pueden perder detalles: «Python 3.10» → «Python 3» → «Python».

## Comprobación · 2 min

Pregunta: **«El reviewer recibe el resumen del implementador que dice que todo pasa.
¿Tiene suficiente para una revisión independiente?»**

No. Dale requisitos, diff, archivos relevantes y forma de ejecutar las pruebas.
Puede consultar las explicaciones del implementador, pero debe verificar las afirmaciones.

**Transición:** vamos a aplicar esa separación al desarrollo de código.

Fuentes: [CMU, Planning, pp. 19–21, 34 y 46](https://www.cmu-agents.com/slides/lecture-05-planning.pdf)
y [Long Context, pp. 47–51](https://www.cmu-agents.com/slides/lecture-03-long-context.pdf).
