---
title: "Fuentes y preparación de demos"
weight: 8
---

Las notas y diapositivas de este taller son una síntesis didáctica propia. Estos
materiales permiten profundizar y reconocer las ideas y ejemplos de referencia.
Las páginas indicadas corresponden al orden de páginas del PDF.

## Lecturas seleccionadas de CMU

El curso [Building AI Agents](https://www.cmu-agents.com/#/) tiene más profundidad
que la que cabe en este taller. Esta selección acompaña los seis temas:

| Material | Qué retomamos |
|---|---|
| [Agents](https://www.cmu-agents.com/slides/lecture-01-agents.pdf) | Anatomía del agente y del harness. |
| [Tool Use](https://www.cmu-agents.com/slides/lecture-02-tool-use.pdf), pp. 28–30 y 54–56 | Validez de argumentos frente a corrección; evaluación por capas. |
| [Long Context](https://www.cmu-agents.com/slides/lecture-03-long-context.pdf), pp. 47–51 | Compactación y conservación de restricciones y evidencia. |
| [Memory and Skills](https://www.cmu-agents.com/slides/lecture-04-memory-and-skills.pdf), pp. 8–15 y 41 | Carga gradual de instrucciones, mantenimiento y exceso de recuperación. |
| [Planning](https://www.cmu-agents.com/slides/lecture-05-planning.pdf), pp. 19–21, 34 y 46 | Límites de roles fijos, restricciones globales y criterios de avance. |
| [Coding Agents](https://www.cmu-agents.com/slides/lecture-06-coding-agents.pdf), pp. 23–24, 33–36 y 47 | Localizar, editar y verificar; pruebas nuevas y regresiones. |
| [Orchestration and Monitoring](https://www.cmu-agents.com/slides/lecture-15-orchestration-and-monitoring.pdf) | Lectura opcional sobre estado, recuperación y supervisión. |

No hace falta recorrer todas las presentaciones durante la clase. Usa una idea
relevante, aplícala al caso y comprueba si se entendió antes de añadir otro mecanismo.

## Materiales del evento Claude for AI Engineering

| Material | Aplicación en este taller |
|---|---|
| [Carlos, tool use: presentación](https://h1sort.com/claude4aieng/) y [repositorio](https://github.com/h1sort/claude4aieng) | Separar solicitud de herramienta y ejecución; seguir una traza. |
| [Dante Bazaldúa, Datos + MCP: diapositivas](https://stdout.mx/claude4aieng/datos-mcp-ibero.pdf) y [repositorio](https://github.com/danteese/claude-mcp-ibero-2026) | Diseño de herramientas, controles y evaluación de elección y argumentos. |
| [Alejandro Martínez, Context Engineering](https://github.com/alexMtzRivero/context-engineering-workshop) | Comparar intervenciones de contexto de forma visible. |
| [Jésica Tapia, Evalmultiagente](https://github.com/JTapiaR/Evalmultiagente) | Leer evaluadores y discutir qué miden y qué dejan fuera. |
| [Physical AI Workshop](https://github.com/hiveflowai/physical-ai-workshop) | Extensión fuera del alcance central: añade hardware y configuración. |

Para Carlos y Dante hay presentaciones web o PDF identificadas. Para contexto y
evaluación, el repositorio es el material práctico de referencia; no se presupone
que exista un deck separado. Los resultados simulados de una demo sirven para
explicar el mecanismo, no para demostrar rendimiento de un modelo.

## Demos opcionales y alternativa local

| Demo | Preparación necesaria | Si no está lista |
|---|---|---|
| Traza de tool use del evento | Revisar modo de ejecución y distinguir simulación de llamada real. | Usar la traza ilustrativa del tema 1. |
| Herramientas MCP del evento | Instalar dependencias indicadas por el repo y preparar credenciales si usa un proveedor. | Discutir el contrato de `ventas_del_mes` del tema 2. |
| Intervenciones de contexto | Revisar dependencias de Python, Pydantic AI y acceso a OpenRouter; ensayar con datos pequeños. | Comparar qué contexto entregaría cada intervención, sin afirmar resultados medidos. |
| Evaluadores multiagente | Revisar proveedor, credenciales, casos y criterios antes de ejecutar. | Examinar una rúbrica sobre el reporte de ventas. |
| Hook del harness elegido | Consultar su documentación, comprobar el evento y su efecto real ante fallo. | Usar la traza de rechazo del tema 5. |

Estas demos externas **no son requisito de la práctica**. Una suscripción a una
aplicación no implica tener crédito o credenciales para las APIs utilizadas por un
repositorio. Comprueba ese acceso antes de la clase, sin mostrar llaves en pantalla.

En el taller de contexto, `main` es material de ejercicios con funciones por
completar; para mostrar la implementación terminada, revisa la rama `solucion`
indicada en su README. Fija la revisión ensayada antes de presentarla.

## Otras referencias

- [Especificación MCP: arquitectura](https://modelcontextprotocol.io/specification/latest/architecture).
- [Claude Code: hooks](https://code.claude.com/docs/en/hooks), para verificar eventos y capacidades del producto elegido.
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/research/demystifying-evals-for-ai-agents).
- [Elastic: RRF](https://www.elastic.co/docs/reference/elasticsearch/rest-apis/reciprocal-rank-fusion) y [ranking](https://www.elastic.co/docs/solutions/search/ranking), para el complemento de recuperación.
- [Hermes Agent](https://github.com/NousResearch/hermes-agent), como lectura opcional de una implementación. Para explicarlo con código, fija la revisión que inspeccionaste y sigue un turno concreto; no hace falta añadirlo como otro bloque del curso.

## Ensayo de quien facilita

Antes de impartir, abre el deck completo en el proyector, ejecuta la práctica en
una carpeta limpia y ensaya la única demo externa que vayas a usar. Comprueba
cuentas, permisos, tiempo y una alternativa sin red. La compilación del sitio no
demuestra que una API o un repositorio externo funcionen en el equipo del salón.

Los tiempos publicados son una primera propuesta. Ajusta después del ensayo,
conservando la evaluación y el cierre de la práctica.
