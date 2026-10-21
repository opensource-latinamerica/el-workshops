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

**Si solo te importa la conclusión, no el camino → delégalo.**

--

## Tu mesa, antes y después

```text
SIN SUBAGENTE              CON SUBAGENTE
  siempre                    siempre
  archivo 1 leído            encargo (2 líneas)
  archivo 2 leído            respuesta (3 líneas)
  …                          ESPACIO LIBRE
  archivo 200 leído
  respuesta (3 líneas)

→ mesa llena,              → mesa limpia
  y apenas empiezas          para seguir
```

--

## ¿Delegar o no?

**Sí, cuando…**

- La respuesta es corta, pero buscarla es largo
- Hay mucha lectura que no vas a necesitar (logs, PDFs)
- Son tareas independientes → en paralelo
- Quieres una segunda opinión limpia (no ve tus supuestos)

**No, cuando…**

- La tarea es pequeña (armar su mesa cuesta)
- Vas a necesitar los detalles después
- Los pasos dependen de lo que van platicando

--

## Cómo pedirlo

"**Usa un subagente para…**" — no cuentes con que decida solo.

Objetivo + contexto + **qué te regrese y en qué forma**

❌ "Usa un subagente para revisar el IVA."

✅ "Usa un subagente para buscar en `src/` dónde se calcula el IVA (16 % en facturas). Regrésame solo las rutas y una línea por cada una."

**Ojo:** no ahorra tokens en total; ahorra **tu** mesa. En el tema 4, superpowers los usa.

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
¿Solo te importa la conclusión?   → Subagente
¿Es una regla que aplica siempre? → AGENTS.md
```

---

## La memoria del agente son archivos

- El modelo no recuerda nada entre sesiones
- Sobrevive lo que quedó **escrito**: `AGENTS.md`, skills, specs
- Tema 4: la spec y el plan viven en archivos
