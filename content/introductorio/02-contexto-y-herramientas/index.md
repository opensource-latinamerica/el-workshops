---
title: "2. Contexto y herramientas"
weight: 2
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

## Lo que el modelo lee

En el tema 1 vimos que **toda la conversación se reenvía cada vez**. El modelo no
recuerda la llamada anterior: la vuelve a leer completa.

Entonces, ¿qué hay exactamente en lo que el modelo lee? Este tema responde eso. Y la
idea que te vas a llevar es esta:

**Dirigir bien a un agente es, en gran parte, decidir qué entra en su mesa.**

## La ventana de contexto es una mesa

Todo lo que el modelo ve en una llamada se llama **ventana de contexto**. Piénsala
como una mesa de trabajo con espacio limitado. Lo que está en la mesa, el modelo lo
ve. Lo que no está, no existe para él.

En el tema 1 dijimos que la carpeta donde abres el agente es su lugar de trabajo. La
carpeta es todo lo que **puede alcanzar**. La mesa es lo que **tiene enfrente** en
este momento. Un archivo de tu carpeta solo llega a la mesa cuando el agente lo lee.

### Qué hay en la mesa en cada llamada

```text
┌─ La mesa (ventana de contexto) ─────────────────────────┐
│                                                         │
│  SIEMPRE                                                │
│    Instrucciones del harness                            │
│    AGENTS.md                                            │
│    Lista de herramientas (+ las de cada MCP)            │
│    Nombre y descripción de cada skill                   │
│                                                         │
│  CRECE                                                  │
│    La conversación: tus mensajes y sus respuestas       │
│    Resultados de herramientas: archivos leídos, …       │
│                                                         │
│  SI APLICA                                              │
│    Una skill completa, solo si se usó                   │
│    (y desde ahí se queda)                               │
│                                                         │
│  ESPACIO LIBRE  ← se acaba                              │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

Las *instrucciones del harness* son lo que el programa le dice al modelo sobre cómo
comportarse.

Lo de arriba ocupa espacio antes de que escribas tu primer mensaje. Lo de en medio
crece con cada paso del ciclo.

### Tres consecuencias

- **Se llena.** La mesa tiene un límite. Cuando se acerca, el harness *compacta*:
  resume la conversación para hacer espacio. Al resumir, se pierden detalles.
- **Se degrada antes de llenarse.** Con mucho encima, lo importante se pierde entre
  lo demás. El agente empieza a olvidar instrucciones o a confundir cosas, aunque
  todavía quede espacio.
- **Se borra.** Una sesión nueva es una mesa vacía. Solo vuelve lo de "siempre"; la
  conversación anterior desaparece.

> **Para quien presenta:** dibuja la mesa en el pizarrón y ve "poniendo" cosas
> encima mientras explicas el diagrama. Luego pregunta: "si leo un archivo de 500
> páginas, ¿qué le pasa a la mesa?". Que lo respondan antes de pasar a tokens.

## Uso y tokens

El modelo no lee palabras, lee **tokens**: pedazos de palabra. "Agente" puede ser uno
o dos tokens. El tamaño de la mesa y lo que gastas de tu plan se miden en tokens.

Como cada llamada reenvía toda la mesa, **el costo crece con cada paso**:

```text
Paso 1:  instrucciones + tu mensaje        → pide el archivo
Paso 2:  instrucciones + tu mensaje + respuesta del paso 1
Paso 3:  instrucciones + tu mensaje + respuesta del paso 1 + paso 2
…
```

La respuesta del paso 1 es el archivo enorme, que llega como resultado. No se paga una
vez: se vuelve a pagar en todos los pasos siguientes.

**Regla práctica: una tarea, una sesión.** Cuando cambies de tema, empieza una sesión
nueva. Mesa limpia, menos costo, menos confusión.

## Las cinco piezas

Hay cinco piezas que cambian lo que el agente puede hacer. Cada una agrega algo
distinto y ocupa la mesa de forma distinta.

### Tool: una mano

Una tool (herramienta) agrega una **acción**. Es lo que vimos en el tema 1: una línea
en la lista de herramientas.

Por dentro, es una llamada estructurada a código: tiene un nombre, unas entradas
definidas y devuelve un resultado. El agente no sabe cómo funciona por dentro; para
él es una caja negra. Solo sabe qué entra y qué sale.

```text
leer_archivo(ruta)   → lo que dice el archivo
ejecutar(comando)    → el resultado del comando
buscar_web(consulta) → páginas encontradas
```

- **Qué ocupa en la mesa:** su descripción, **siempre**; y lo que devuelve, cada vez
  que se usa.
- **Error común:** pedirle algo para lo que no tiene tool (y que lo invente), o aceptar
  su uso sin leer el permiso.

### MCP: un enchufe que trae manos de otro lado

MCP es un protocolo: una forma estándar de conectar el agente a un servidor externo
que le ofrece tools. Un *protocolo* son reglas comunes para que dos programas se
entiendan; un *servidor* es un programa (en tu computadora o en internet) que
atiende pedidos. Se escribe una vez y sirve en Claude Code, Codex, Gemini CLI y
otros.

Ejemplo: conectas tu calendario por MCP y aparecen dos tools nuevas en la lista:

```text
crear_evento(título, fecha)
listar_eventos(desde, hasta)
```

Un MCP no es algo distinto a una tool. Es una forma de **traer tools** de afuera.

- **Qué ocupa en la mesa:** todas sus tools van a la lista, en la mayoría de los
  agentes **siempre**, las uses o no; y lo que devuelven, cada vez que se usan.
- **Error común:** instalar 10 MCPs "por si acaso". Cada uno llena la mesa en cada
  llamada.

### Skill: una receta que sacas del cajón

Una skill agrega **saber hacer**. Es un archivo `SKILL.md` con un procedimiento: los
pasos, el formato del resultado y el criterio para decidir. Puede incluir scripts.

Clave: **una skill no agrega acciones.** Enseña a usar bien las que ya hay. Si la
skill dice "corre este script", el agente lo corre con la tool `ejecutar`.

Ejemplo: una skill "reporte mensual".

```text
reporte-mensual/
  SKILL.md          ← pasos, formato del reporte, qué revisar
  limpiar_datos.py  ← script que limpia el archivo de gastos
```

¿Qué va en texto y qué va en script?

- Lo **determinista y repetible** (limpiar columnas, sumar, cambiar formatos) → código.
  *Determinista* quiere decir que da siempre el mismo resultado: un script hace lo mismo
  siempre.
- Lo que **requiere criterio** (qué destacar, cómo explicar una variación) → texto de
  la skill.

Si lo harías igual cada vez, va en un script.

- **Qué ocupa en la mesa:** solo el nombre y la descripción. El resto se carga solo
  si aplica. Por eso puede ser larga.
- **Error común:** meter ese procedimiento en `AGENTS.md`, donde se paga en cada
  llamada aunque no lo uses.

### Subagente: otra persona con su propia mesa

Un subagente es otro ciclo del agente que empieza con la mesa vacía. Le delegas una
tarea completa y solo te regresa el resultado, no el desorden que hizo para
obtenerlo.

Sirve cuando la tarea llenaría tu mesa, o para hacer varias cosas en paralelo.

```text
Tú → subagente:  Revisa estos 200 archivos y dime dónde se calcula el IVA.
                 (lee 200 archivos en SU mesa)
Subagente → tú:  Se calcula en ventas.py, factura.py y reportes/iva.py.
```

Tu mesa solo recibe esas tres líneas.

**Regla central: si solo te importa la conclusión, no el camino → delégalo.**

Compara las dos mesas con la misma pregunta:

```text
SIN SUBAGENTE                   CON SUBAGENTE
Tu mesa:                        Tu mesa:
  siempre                         siempre
  archivo 1 leído                 encargo (2 líneas)
  archivo 2 leído                 respuesta (3 líneas)
  …                               ESPACIO LIBRE
  archivo 200 leído
  respuesta (3 líneas)

→ mesa llena, y apenas          → mesa limpia para seguir
  empiezas
```

La respuesta es la misma. Lo que cambia es qué quedó en **tu** mesa.

#### Cuándo delegar: cuatro señales

- **La respuesta es corta, pero buscarla es largo.** "¿Dónde…?", "¿qué dice…?",
  "resume estos documentos".
- **Mucha lectura que no vas a necesitar después.** Logs (registros de lo que pasó),
  30 PDFs, documentación.
- **Tareas independientes.** "Investiga estas 3 opciones": un subagente por opción, en
  paralelo.
- **Una segunda opinión limpia.** "Revisa lo que hicimos". No carga tus supuestos
  porque no ve tu mesa.

#### Cuándo NO delegar

- **Tareas pequeñas.** El subagente arma su mesa desde cero, y eso cuesta.
- **Vas a necesitar los detalles.** Si después vas a editar esos mismos archivos, mejor
  que estén en tu mesa.
- **Pasos encadenados que dependen de lo que van platicando.** El subagente no oyó esa
  conversación.

#### Cómo pedirlo

Dilo explícito: **"Usa un subagente para…"**. Algunos agentes deciden solos cuándo
delegar, pero no cuentes con eso.

Un buen encargo es la fórmula del tema 1 (objetivo + contexto + terminado), aplicada a
delegar:

- **Objetivo:** qué tiene que averiguar o hacer.
- **Contexto:** lo que no ve. No conoce tu mesa: dile todo lo que necesita saber.
- **Terminado:** para un subagente, "terminado" es **qué te regresa y en qué forma**
  ("solo las rutas y una línea por cada una").

Esa última parte es la que protege tu mesa. Si no la pides, te puede regresar un
reporte de dos páginas y volviste a llenarla.

❌ "Usa un subagente para revisar el IVA."

✅ "Usa un subagente para buscar en `src/` (la carpeta del proyecto) dónde se calcula el
IVA. Es el impuesto de 16 % que se suma en las facturas. Regrésame solo las rutas de
los archivos y una línea por cada una que diga qué hace."

#### Un matiz honesto

No siempre ahorra tokens: la búsqueda se paga igual y armar su mesa cuesta. Lo que
seguro ahorra es **tu** mesa. A veces pagas un poco más para que la conversación
principal siga clara.

- **Qué ocupa en la mesa:** tu encargo y su respuesta final.
- **Error común:** delegar sin decir qué contexto necesita ni qué te debe regresar.

> **Para quien presenta:** antes de mostrar las señales, pregunta "¿cuándo NO
> conviene delegar?".

En el tema 4 verás que superpowers usa subagentes para repartir el trabajo.

### `AGENTS.md`: la nota pegada en la mesa

`AGENTS.md` es un archivo en tu proyecto con reglas que aplican **siempre**. Se lee
en cada llamada.

```markdown
- Responde en español.
- Nunca borres la carpeta `datos/`.
```

`AGENTS.md` es el nombre común, pero no todos los agentes lo leen. Crea el archivo
según tu agente:

- **Codex:** `AGENTS.md`.
- **Claude Code:** `CLAUDE.md`. Truco: si ya tienes un `AGENTS.md`, tu `CLAUDE.md`
  puede tener solo la línea `@AGENTS.md`, y Claude Code lo importa.
- **Gemini CLI:** `GEMINI.md`.

La idea es la misma. En el curso le decimos `AGENTS.md` a cualquiera de ellos.

- **Qué ocupa en la mesa:** todo su contenido, en **cada** llamada.
- **Error común:** hacerlo largo. Cada línea se paga siempre.

### Resumen

| Pieza | En la metáfora | Agrega | Qué ocupa en la mesa | Error común |
|---|---|---|---|---|
| Tool | Una mano | Una acción | Su descripción, siempre; y lo que devuelve, cada vez que se usa | Pedirle algo sin tool (y que lo invente) o aceptar sin leer el permiso |
| MCP | Un enchufe que trae manos | Tools de un servicio externo | Todas sus tools, siempre; y lo que devuelven, cada vez que se usan | Instalar muchos "por si acaso" |
| Skill | Una receta en el cajón | Saber hacer | Nombre y descripción; el resto si aplica (y se queda) | Meter el procedimiento en `AGENTS.md` |
| Subagente | Otra persona con su mesa | Una mesa aparte | Tu encargo y su resultado | Delegar sin dar contexto ni decir qué regresar |
| `AGENTS.md` | La nota pegada en la mesa | Reglas que aplican siempre | Todo, siempre | Hacerlo largo |

> **Para quien presenta:** para cada pieza, pregunta "¿qué ocupa en la mesa?" antes
> de mostrar la respuesta. Es la pregunta que conecta las cinco.

## ¿Dónde va cada cosa?

Cuando el agente no hace lo que quieres, pregúntate qué le falta y dónde ponerlo:

```text
¿Le falta una acción?             → Tool
                                    (de un servicio externo: vía MCP)
¿Le falta saber cómo hacerlo?     → Skill
                                    (los pasos fijos, en un script)
¿Llenaría tu mesa y solo te       → Subagente
 importa la conclusión?
¿Es una regla que aplica siempre? → AGENTS.md
¿Es solo para esta vez?           → Dilo en tu mensaje
```

## La memoria del agente son archivos

El modelo no recuerda nada entre sesiones. Cada sesión empieza con la mesa vacía.

Lo que sobrevive es lo que quedó **escrito**: `AGENTS.md`, las skills, las specs
(documentos que dicen qué se va a construir; las verás en el tema 4) y el historial de
commits (tema 3). Si quieres que el agente sepa algo la próxima vez, tiene que estar en
un archivo.

En el tema 4 lo vas a usar: la spec y el plan de un proyecto viven en archivos, y por
eso el trabajo puede seguir de una sesión a otra.
