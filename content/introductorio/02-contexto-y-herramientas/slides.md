# Contexto y herramientas

Curso introductorio · Tema 2

---

## Lo que el modelo lee

En el tema 1: **toda la conversación se reenvía cada vez**.

**¿Qué hay exactamente en lo que lee?**

---

## La ventana de contexto es una mesa

- Todo lo que el modelo ve en una llamada, **y nada más**
- Espacio limitado
- La carpeta es lo que **puede alcanzar**; la mesa, lo que **tiene enfrente**

---

## Qué hay en la mesa

```text
SIEMPRE
  Instrucciones del harness
  AGENTS.md
  Lista de herramientas (+ las de cada MCP)
  Nombre y descripción de cada skill

CRECE
  La conversación: tus mensajes y sus respuestas
  Resultados de herramientas: archivos leídos, …

SI APLICA
  Una skill completa, solo si se usó

ESPACIO LIBRE  ← se acaba
```

---

## Tres consecuencias

- **Se llena:** el harness *compacta* (resume) y pierde detalles
- **Se degrada antes de llenarse:** con mucho encima, lo importante se pierde
- **Se borra:** sesión nueva = mesa vacía, salvo lo de "siempre"

---

## Tokens

Token = un pedazo de palabra. La mesa y tu plan se miden en tokens.

```text
Paso 1:  instrucciones + mensaje + archivo enorme
Paso 2:  instrucciones + mensaje + archivo enorme + paso 1
Paso 3:  instrucciones + mensaje + archivo enorme + paso 1 + paso 2
```

El archivo enorme se **vuelve a pagar** en cada paso.

---

## Regla

**Una tarea, una sesión.**

Mesa limpia, menos costo, menos confusión.

---

## Cinco piezas

1. Tool
2. MCP
3. Skill
4. Subagente
5. `AGENTS.md`

Para cada una: **¿qué ocupa en la mesa?**

---

## Tool = una mano

Agrega una **acción**. Nombre, entradas, resultado. Para el agente: caja negra.

```text
leer_archivo(ruta)
ejecutar(comando)
buscar_web(consulta)
```

- **En la mesa:** su descripción, en cada llamada
- **Error común:** ninguno; ya vienen. Conocerlas te dice qué pedir

---

## MCP = un enchufe que trae manos

Protocolo para conectar un servidor externo que ofrece **tools**. Sirve en Claude Code, Codex, Gemini…

```text
Calendario por MCP → crear_evento, listar_eventos
```

- **En la mesa:** todas sus tools, **siempre**
- **Error común:** instalar 10 "por si acaso"

---

## Skill = una receta del cajón

Agrega **saber hacer**: un `SKILL.md` con pasos, formato y criterio. Puede traer scripts.

```text
reporte-mensual/
  SKILL.md          ← pasos y formato
  limpiar_datos.py  ← los pasos fijos
```

- **No agrega acciones:** usa las que ya hay
- **En la mesa:** solo nombre y descripción
- **Error común:** meter el procedimiento en `AGENTS.md`

--

## Texto o script

- **Determinista y repetible** → código (script)
- **Requiere criterio** → texto de la skill

Si "corre este script", lo corre con la tool `ejecutar`.

---

## Subagente = otra persona con su mesa

Otro ciclo con la **mesa vacía**. Le delegas; regresa el resultado, no el desorden.

```text
Tú:        Revisa estos 200 archivos y dime dónde se calcula el IVA.
Subagente: ventas.py, factura.py y reportes/iva.py.
```

- **En la mesa:** tu encargo y su respuesta
- **Error común:** delegar sin contexto (no ve tu mesa)

En el tema 4, superpowers los usa.

---

## `AGENTS.md` = la nota pegada en la mesa

Reglas que aplican **siempre**. Se lee en cada llamada.

```markdown
- Responde en español.
- Nunca borres la carpeta `datos/`.
```

Claude Code: `CLAUDE.md` · Gemini CLI: `GEMINI.md`

- **Error común:** hacerlo largo (se paga siempre)

---

## Resumen

| Pieza | Agrega | En la mesa |
|---|---|---|
| Tool | Una acción | Descripción, siempre |
| MCP | Tools de afuera | Todas sus tools, siempre |
| Skill | Saber hacer | Nombre y descripción |
| Subagente | Una mesa aparte | Encargo y resultado |
| `AGENTS.md` | Reglas | Todo, siempre |

---

## Cómo elegir

```text
¿Le falta una acción?             → Tool (de afuera: vía MCP)
¿Le falta saber cómo hacerlo?     → Skill (pasos fijos: script adentro)
¿La tarea llenaría la mesa?       → Subagente
¿Es una regla que aplica siempre? → AGENTS.md
```

---

## La memoria del agente son archivos

- El modelo no recuerda nada entre sesiones
- Sobrevive lo que quedó **escrito**: `AGENTS.md`, skills, specs
- Tema 4: la spec y el plan viven en archivos

---

## Para llevar

**Dirigir bien a un agente es, en gran parte, decidir qué entra en su mesa.**
