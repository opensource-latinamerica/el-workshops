---
title: "2. Contexto y herramientas"
weight: 2
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

## El agente olvida

Todo lo que el agente sabe en una conversación vive en su **contexto**: lo que le
dijiste, los archivos que leyó, lo que respondió. Dos problemas:

- **Se llena.** El contexto tiene un límite. Conversaciones muy largas hacen que el
  agente se confunda o que tenga que resumir (*compactar*) y pierda detalles.
- **Se borra.** Al abrir una sesión nueva, empieza de cero.

Y cada mensaje consume **uso** (tokens): conversaciones largas y archivos enormes
gastan más de tu plan.

**Regla práctica:** una tarea, una sesión. Cuando cambies de tema, empieza una nueva.

## Cuatro formas de darle contexto y capacidades

| Pieza | Qué es | Cuándo te ayuda |
|---|---|---|
| `AGENTS.md` | Archivo en tu proyecto con reglas permanentes. El agente lo lee al empezar cada sesión. | Cuando te descubres repitiendo lo mismo en cada sesión ("responde en español", "usa Python"). |
| Skills | Recetas guardadas (`SKILL.md`) que el agente carga solo cuando aplican. | Cuando hay una tarea que se hace siempre igual (revisar código, escribir un reporte). |
| Tools | Las acciones que el agente puede hacer: leer, escribir, ejecutar, buscar en la web. | Ya vienen incluidas; conocerlas te dice qué puedes pedirle. |
| MCP | Un enchufe estándar para conectar el agente a servicios externos (calendario, Notion, una base de datos). | Cuando el agente necesita información o acciones fuera de tu computadora. |

`AGENTS.md` es el nombre común. Algunos agentes usan su propio nombre: Claude Code lee
`CLAUDE.md` y Gemini CLI lee `GEMINI.md`. La idea es la misma.

### Diferencia clave

- `AGENTS.md` está **siempre** cargado. Mantenlo corto.
- Una skill se carga **solo cuando hace falta**. Puede ser larga.
- Una tool es una **acción**; un MCP es un **conjunto de tools** que viene de afuera.

## Ejemplo de `AGENTS.md`

```markdown
# Mi proyecto

- Responde siempre en español.
- Explícame los cambios en lenguaje sencillo antes de hacerlos.
- Los datos están en la carpeta `datos/`; nunca los borres.
```

## Ejercicio (10 min)

1. En tu carpeta del tema 1, pide al agente: "Crea un `AGENTS.md` con estas reglas: …"
   (escoge 2 o 3 tuyas).
2. Cierra el agente y ábrelo de nuevo.
3. Pregúntale "¿qué reglas tienes en este proyecto?" y confirma que las recuerda.
