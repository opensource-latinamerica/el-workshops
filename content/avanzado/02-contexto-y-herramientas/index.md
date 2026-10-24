---
title: "2. Contexto y herramientas"
weight: 2
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

**Duración:** 25 min. **Al terminar:** eliges la pieza adecuada para una necesidad
y distingues qué parte del contexto puedes reducir.

## Qué le falta al agente · 5 min

| Necesidad | Pieza | Ejemplo |
|---|---|---|
| Una convención general del proyecto | Instrucciones persistentes | Moneda y formato usados por el equipo. |
| Un procedimiento reutilizable | Skill | Pasos y criterios de un reporte mensual. |
| Un cálculo o transformación repetible | Script, función o CLI | Sumar ventas válidas de un mes. |
| Conectar capacidades de un servicio | API o MCP, según el cliente | Consultar una fuente desde el agente. |
| Encontrar evidencia | Herramientas de recuperación | Buscar una definición en los documentos. |

Una **skill** es un paquete de conocimiento procedimental: instrucciones y, a veces,
scripts o referencias. Describe cuándo usarlo y cómo realizar la tarea. Una **tool**
es una operación que el harness puede ejecutar. Leer una skill no crea por sí solo
los permisos o herramientas que necesita.

El soporte y el nombre de los archivos de instrucciones cambian entre productos.
Revisa qué carga tu harness. Evita asumir que todo archivo del proyecto se lee siempre
o que todas las herramientas se cargan completas en cada llamada.

## CLI, API y MCP · 4 min

Una CLI permite invocar operaciones con comandos. Una API ofrece una interfaz de
programación. MCP estandariza la comunicación entre un cliente y servidores que
ofrecen capacidades, incluidas herramientas.

En MCP, el **host** es la aplicación; un **cliente** mantiene la conexión con un
**servidor** que expone las capacidades. Un servidor puede correr localmente o en
otro equipo. MCP no implica por sí mismo un servicio remoto.

No son opciones excluyentes: una función del negocio puede ofrecerse por CLI y MCP.
El modelo puede decidir dinámicamente tanto una llamada MCP como un comando.
Elige según clientes, autenticación, entorno y mantenimiento; no añadas una capa
si una herramienta que ya tienes resuelve el trabajo.

## Diseñar una herramienta que se pueda usar bien · 5 min

Ejemplo conceptual:

```text
ventas_del_mes(mes="2026-10")
→ estado: ok
  total_mxn: "2000.00"
  registros_validos: 3
  fuente: ventas.csv
  regla: completadas; deduplicadas por id
```

Tres criterios para el contrato:

1. **Intención clara.** Nombre, descripción y parámetros dicen cuándo usarla.
2. **Resultado acotado.** Devuelve datos suficientes, unidad, fuente y advertencias;
   evita volcar una tabla enorme cuando solo necesitas el total.
3. **Error accionable.** «El id V004 tiene dos importes distintos; corrige el archivo»
   permite actuar. «Algo falló» obliga a adivinar.

Una tool de consulta genérica puede servir para explorar; una operación acotada puede
ser mejor para un flujo estable. Ambas necesitan controles acordes a su alcance.

## Cuatro formas de gestionar contexto · 7 min

| Problema | Intervención | Lo que debes comprobar |
|---|---|---|
| Historial demasiado largo | Compactar o resumir | Conserva objetivo, restricciones y decisiones necesarias. |
| Documentos o logs enormes | Guardar fuera y recuperar fragmentos | Las referencias permiten volver a la evidencia. |
| Demasiadas definiciones de tools | Descubrimiento bajo demanda, si existe | Encuentra la herramienta que necesita. |
| Investigación que llena la conversación | Delegación con contexto delimitado | Devuelve conclusiones con evidencia suficiente. |

**Recuperar** y **compactar** resuelven problemas distintos. Buscar con `rg` es
recuperación textual; consultar un índice semántico es otra estrategia. RAG genera
con información recuperada y no exige embeddings. Una CLI puede acceder a ambos.

Para importes, usa cálculo sobre datos estructurados. Para un identificador exacto,
empieza por búsqueda textual. Considera búsqueda semántica cuando la pregunta y la
fuente usan expresiones distintas. Evalúa antes de añadir [RRF o reranking](../complementos/rag/).

> **Demo opcional:** en el [taller de Alejandro Martínez](https://github.com/alexMtzRivero/context-engineering-workshop),
> alterna todas las tools y tools bajo demanda; después activa compactación. Señala
> qué segmento de contexto cambia. Ensaya antes con tu modelo; no prometas que una
> pregunta vaya a fallar. Usa una conversación pequeña para controlar el consumo.
>
> **Sin API o sin demo preparada:** dibuja cuatro cajas —instrucciones, herramientas,
> historial, evidencia— y pide al grupo que marque cuál cambia con cada intervención.
> Es un ejercicio conceptual, no una medición de rendimiento.

## Comprobación · 4 min

Reparte estas necesidades entre las piezas:

- «Cómo redactar el reporte cada mes» → skill.
- «El total debe calcularse con la misma fórmula» → código.
- «Encontrar la política de cancelaciones» → recuperación.
- «Las definiciones de 80 herramientas llenan el contexto» → descubrimiento, si lo soporta el harness.

Pregunta final: **«¿Una skill que dice que nunca publique garantiza que no publique?»**
No: las instrucciones orientan; los permisos y controles se ejecutan fuera del criterio
del modelo. Tema 5.

**Transición:** una de las formas de controlar el contexto es delegar. El siguiente
tema enseña qué encargo mandar y qué información debe regresar.

Fuentes: [CMU, Memory and Skills, pp. 8–11](https://www.cmu-agents.com/slides/lecture-04-memory-and-skills.pdf),
[Dante Bazaldúa, pp. 15 y 24](https://stdout.mx/claude4aieng/datos-mcp-ibero.pdf),
[MCP: herramientas](https://modelcontextprotocol.io/specification/2025-11-25/server/tools).
