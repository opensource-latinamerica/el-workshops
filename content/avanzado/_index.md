---
title: Avanzado
outputs: [html, rss, slides]
cascade:
  type: docs
---

**Harnesses: contexto, herramientas y control del trabajo de un agente.**

Aprende a reconocer por qué falla un agente, elegir qué cambiar alrededor del modelo
y comprobar si ese cambio mejora el resultado.

Este curso es **independiente del introductorio**: ambos se imparten al mismo tiempo.
Empezamos con un vocabulario común y lo aplicamos a decisiones de diseño. Necesitas
poder abrir un proyecto, usar una terminal y trabajar con un agente sobre archivos;
revisa los [requisitos](00-requisitos/).

## Qué vas a aprender

- Distinguir modelo, agente, flujo agéntico y harness.
- Elegir entre instrucciones, skills, scripts, CLI y MCP.
- Gestionar contexto y delegar con un encargo y un resultado claros.
- Usar specs, pruebas y revisión independiente al desarrollar con agentes.
- Separar lo que pides al modelo de lo que el sistema comprueba o impide.
- Comparar dos configuraciones con los mismos casos y evidencia del resultado.

## Agenda propuesta · 4 h 15 min

La distribución es provisional para el ensayo: **2 h de explicación y demostraciones,
15 min de descanso y 2 h de práctica**.

| Tema | Tiempo | Pregunta que resuelve |
|---|---|---|
| [1. Anatomía del harness](01-harness/) | 15 min | ¿Quién decide y quién ejecuta? |
| [2. Contexto y herramientas](02-contexto-y-herramientas/) | 25 min | ¿Qué necesita ver y poder hacer? |
| [3. Subagentes y tareas largas](03-subagentes-y-tareas-largas/) | 15 min | ¿Qué delego y cómo continúo después? |
| [4. Coding agents](04-coding-agents/) | 25 min | ¿Cómo convierto un pedido en un cambio comprobado? |
| [5. De instrucciones a controles](05-controles/) | 20 min | ¿Qué no debe depender de que el modelo lo recuerde? |
| [6. Evaluar el sistema](06-evaluacion/) | 20 min | ¿Cómo sé si mejoró? |
| Descanso | 15 min | |
| [Práctica: mejorar un flujo y medirlo](07-practica/) | 120 min | Tu proyecto, una mejora, evidencia antes y después. |

[Abrir la presentación completa](slides.html) · [Fuentes y demos para preparar la clase](08-fuentes/)

## Un caso para conectar las ideas

Durante la explicación usamos un **reporte de ventas**: leer un archivo, comprobar
su calidad, calcular importes y explicar el resultado con sus fuentes. Los datos son
sintéticos. En la práctica puedes usar ese [caso de arranque](07-practica/#archivos-del-caso-de-ventas)
o tu propio proyecto de datos, documentación o código.

No hace falta programar un harness completo. Vamos a configurar y extender uno
existente, y a mirar por dentro lo necesario para entender sus decisiones.

## Qué te llevas

Un flujo ejecutable o procedimiento repetible, una mejora concreta y un registro de
casos que muestra qué funcionó, qué falló y qué falta. Una demo exitosa es el comienzo
de esa comprobación.

[RAG, búsqueda híbrida y reranking](complementos/rag/) quedan como complemento para
proyectos que necesitan recuperar documentos. No forman parte del recorrido principal.
