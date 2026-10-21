# Contexto y herramientas

Curso introductorio · Tema 2

---

## El agente olvida

- Su memoria es el **contexto** de la conversación
- **Se llena:** se confunde o resume y pierde detalles
- **Se borra:** cada sesión nueva empieza de cero

---

## Uso (tokens)

Cada mensaje y cada archivo leído gasta de tu plan.

**Regla:** una tarea, una sesión.

---

## Cuatro piezas

1. `AGENTS.md`
2. Skills
3. Tools
4. MCP

---

## `AGENTS.md`

Reglas permanentes del proyecto. Se lee **al empezar cada sesión**.

```markdown
- Responde siempre en español.
- Explícame los cambios antes de hacerlos.
- Nunca borres la carpeta datos/.
```

Usa uno cuando te descubras **repitiendo lo mismo**.

---

## Skills

Recetas guardadas que el agente carga **solo cuando aplican**.

Úsalas para tareas que **siempre se hacen igual**.

---

## Tools

Las manos del agente: leer, escribir, ejecutar, buscar.

Conocerlas te dice **qué puedes pedirle**.

---

## MCP

Un enchufe estándar para conectar servicios de afuera: calendario, Notion, bases de datos.

Úsalo cuando el agente necesita algo **fuera de tu computadora**.

---

## ¿Cuál uso?

| Si… | Usa |
|---|---|
| repites la misma instrucción | `AGENTS.md` |
| repites el mismo procedimiento | Skill |
| quieres saber qué puede hacer | Tools |
| necesita un servicio externo | MCP |

---

## Ejercicio (10 min)

1. Pide un `AGENTS.md` con 2–3 reglas tuyas
2. Cierra y abre el agente
3. "¿Qué reglas tienes en este proyecto?"
