---
title: "4. Flujos agénticos y superpowers"
weight: 4
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

## Donde todo se junta

Ya tienes las piezas. En el tema 1 viste qué es un agente y cómo pedirle las cosas.
En el tema 2, qué hay en su mesa y las cinco piezas. En el tema 3, cómo Git y GitHub
le dan una red.

Lo que falta es el **orden**: qué va primero, qué después y cuándo te toca a ti.
Superpowers pone ese orden. Cada etapa de su flujo usa algo que ya viste.

## El error más común

Pedirle al agente "hazme una app de X" y dejarlo correr. El agente adivina lo que
quieres, construye mucho y rápido, y al final no es lo que tenías en mente.

Le diste mucha **autonomía** (tema 1) y muy poco **contexto**. El agente no tenía
cómo saber lo que querías, así que lo inventó.

No basta con un mejor pedido: hace falta un mejor **flujo**.

## Plugins

Un **plugin** es un paquete de piezas del tema 2 que alguien ya armó: skills y, a
veces, subagentes, tools o MCPs. Lo instalas una vez.

La diferencia con instalar una pieza suelta: con un plugin no instalas una función,
instalas un **flujo de trabajo completo**. Las piezas vienen pensadas para usarse
juntas y en orden.

[Superpowers](https://github.com/obra/superpowers) es un plugin que le enseña al agente
a trabajar como un buen equipo: preguntar antes de construir, escribir lo acordado,
planear, revisar y comprobar. Funciona en varios agentes: Claude Code, Codex, Gemini CLI y otros.
Lo instalaste en los requisitos.

### Cómo se activa

Recuerda la mesa del tema 2: de cada skill, en la mesa solo están el nombre y la
descripción. El resto se queda en el cajón hasta que hace falta.

Superpowers aprovecha eso. Al iniciar la sesión carga una skill (`using-superpowers`)
que le dice al agente: **"antes de actuar, revisa si alguna de tus skills aplica"**.
Esa regla corta sí va **siempre** en la mesa. Las recetas de cada etapa, no: se quedan
en el cajón hasta que aplican.

```text
┌─ La mesa, al iniciar la sesión ──────────────────────┐
│                                                      │
│  SIEMPRE                                             │
│    "Antes de actuar, revisa si alguna skill aplica"  │
│    Nombre y descripción de cada skill                │
│                                                      │
│  SI APLICA                                           │
│    La skill de la etapa en la que vas                │
│                                                      │
└──────────────────────────────────────────────────────┘
```

Así, cuando dices "quiero hacer una app", el agente no se pone a programar: revisa
el cajón, ve que hay una skill para entender la idea primero y la saca. Cada receta
llega a la mesa justo cuando hace falta.

> **Para quien presenta:** pregunta "¿por qué no meter todo el flujo en
> `AGENTS.md`?". La respuesta viene del tema 2: se pagaría en cada llamada, aunque
> no lo uses.

## Spec-driven development

La idea detrás del flujo tiene nombre: *spec-driven development* (desarrollo guiado
por la spec). Primero se acuerda **qué** y **por qué**; después el **cómo**.

### Corregir temprano es barato

Un error cuesta más entre más tarde lo encuentras:

```text
Si corriges en…    Te cuesta
Brainstorming      █                  cambiar una respuesta
Spec               ██                 cambiar una frase
Plan               ████               reordenar pasos
Ejecución          ████████           rehacer código
Ya terminado       ████████████████   deshacer y volver a empezar
```

Cambiar una frase de la spec toma un minuto. Rehacer el código que ya se construyó
sobre esa frase puede tomar una hora, y gastar mucha mesa.

### Qué lleva una spec

La **spec** (especificación) es un documento corto que dice qué se va a construir. Una
buena spec responde cuatro cosas:

- **La intención:** el porqué. Qué problema tuyo resuelve.
- **Los objetivos:** qué tiene que hacer.
- **Lo que NO entra:** lo que queda fuera, aunque suene bien. Esto evita que el agente
  crezca el proyecto por su cuenta.
- **Lo que la haría un fracaso**, aunque "funcione": por ejemplo, "si para registrar
  un gasto tengo que llenar cinco campos, no la voy a usar".

Ejemplo corto:

```text
Intención:  No sé en qué se me va el dinero a fin de mes.
Objetivos:  Registrar un gasto con monto y categoría.
            Ver el total por categoría del mes.
No entra:   Cuentas de banco, varias monedas, usuarios.
Fracaso si: Registrar un gasto toma más de 10 segundos.
```

### La spec es un archivo

En el tema 2 vimos que **la memoria del agente son archivos**. La spec no se queda en
la conversación: se guarda en un archivo del proyecto. Lo mismo el plan.

Por eso sobreviven a una sesión nueva, y por eso un subagente con la mesa vacía puede
leerlos y saber qué hacer.

Superpowers guarda la spec en `docs/superpowers/specs/` (y hace commit) y el plan en
`docs/superpowers/plans/`.

## El flujo, etapa por etapa

```text
   ETAPA           PIEZA QUE USA                   TU PAPEL
1  Brainstorming   skill (tema 2)                  ┐
2  Spec            archivo (tema 2)                ┘ decides
3  Plan            archivo (tema 2)                ┐
4  Ejecución       subagentes + rama (temas 2, 3)  │ supervisas
5  Revisión        subagente limpio (tema 2)       ┘
6  Cierre          rama + PR (tema 3)                apruebas
```

Tu papel cambia: en 1 y 2 **decides** qué se construye; en 3 a 5 **supervisas** cómo
se construye; en 6 **apruebas** si entra.

### 1. Brainstorming

El agente usa una **skill** (tema 2) para entender tu idea antes de construir nada.
Te hace preguntas hasta entender lo que quieres.

En su primer mensaje te ofrece saltarte las preguntas y empezar de una vez. Si
aceptas, se acaba el flujo. **Te va a ofrecer saltarte las preguntas: di que no.**

```text
Tú:      Quiero una app para mis gastos.
Agente:  ¿Qué es lo que te molesta hoy de llevar tus gastos?
Tú:      Que no sé en qué se me va el dinero a fin de mes.
Agente:  Cuéntame la última vez que te pasó.
Tú:      No supe cuánto fue de súper y cuánto de salidas.
Agente:  Entiendo esto: … ¿Qué falta o qué está mal?
```

Fíjate en tres cosas:

- **Una pregunta a la vez.** No te avienta un cuestionario.
- **Pregunta por el problema, no por la solución.** No empieza con "¿qué botones
  quieres?", sino con "¿qué te molesta?".
- **Te devuelve lo que entendió** para que lo corrijas.

Y lo más importante: **no construye nada hasta que apruebes.**

- **Tu papel:** decides. Contesta con tu problema real, no con lo que crees que el
  agente quiere oír.

> **Para quien presenta:** lee el diálogo en voz alta, como leíste la traza del tema
> 1. Detente en la primera pregunta: es abierta y es sobre el problema. No ofrece
> opciones para escoger: te pide que lo describas con tus palabras, porque las
> opciones empujan hacia lo que el agente imagina.

### 2. Spec

Con lo acordado, el agente escribe la spec en un **archivo** (tema 2).

- **Tu papel:** decides. Léela completa. Si algo no es tuyo (una función que no
  pediste, una suposición que no es cierta), corrígelo ahora: aquí es donde corregir
  es más barato.

### 3. Plan

El agente divide la spec en **pasos pequeños**, también en un archivo. Cada paso
tiene su propio criterio de **terminado**, algo que el agente pueda comprobar. Es la
fórmula del tema 1 (objetivo + contexto + terminado), aplicada a cada paso.

```text
Paso 2:     Sumar los gastos por categoría.
Terminado:  Con el archivo de prueba, "super" suma 850.
```

- **Tu papel:** supervisas. Pídele "Resúmeme el plan en lenguaje sencillo, un paso
  por línea, con su 'terminado'" y revisa que cada paso se pueda comprobar.

Al terminar, el agente te pide revisar el plan y te pregunta qué modo de ejecución
prefieres:

- ***Subagent-driven*:** un subagente nuevo hace cada paso y otro lo revisa antes de
  seguir. Es el que describe este tema. **Elige este.**
- ***Native*:** el mismo agente hace todos los pasos en esta sesión
  (`executing-plans`) y deja una sola revisión al final.

### 4. Ejecución

Cada paso del plan va a un **subagente** con la mesa limpia (tema 2): lee la spec y
su paso, lo hace y regresa el resultado. Tu mesa no se llena con el desorden de cada
paso. Todo pasa en una **rama** aparte (tema 3), así que `main` sigue intacta.

Superpowers puede preguntarte si quieres un *worktree* aislado. Responde: **"No,
trabaja en una rama nueva en esta carpeta."** Así ves los cambios en tu misma carpeta,
y es la rama del tema 3.

El *worktree* (una copia de tu carpeta en otra rama, dentro de `.worktrees/`) sirve
cuando varias personas o varios agentes trabajan a la vez en el mismo proyecto y no
quieres que se pisen. En la práctica no hace falta.

- **Tu papel:** supervisas. Con subagentes solo ves el encargo y el resultado (tema
  2): lee lo que reporta después de cada paso, y los **permisos** (tema 1): lee antes
  de aceptar.

### 5. Revisión

Otro subagente revisa el trabajo con una **segunda opinión limpia** (tema 2): no
carga los supuestos de quien lo hizo. Y nada se declara terminado sin comprobarlo:
**el agente no se califica solo** (tema 3).

- **Tu papel:** supervisas. Prueba tú mismo el resultado; si no sabes cómo, pídele
  "muéstrame cómo probarlo".

### 6. Cierre

El agente te pregunta qué hacer con la rama (tema 3) y te da tres opciones:

1. Unirla a la rama base en tu computadora (en local).
2. Hacer push y abrir un **PR**.
3. Dejar la rama como está.

Elige la 2 (PR). Ojo: la opción 2 no une nada a `main`. Revisa el **diff** en GitHub
y luego pide "une el PR a main". Al final, pide **"Cámbiate a main y trae los
cambios"**, para que tu carpeta quede igual que GitHub. Si tu proyecto es una página
y el repo es público, publícala en **GitHub Pages**, con datos de ejemplo.

El PR es la forma estándar de trabajar cuando colaboras con otras personas; conviene
acostumbrarse desde un proyecto personal.

Descartar el trabajo no aparece en las opciones: solo pasa si lo pides tú.

- **Tu papel:** apruebas. Revisa el **diff** antes de unir.

### Los nombres de las skills

En la práctica vas a ver al agente decir los nombres de las skills que usa. Así se
corresponden:

| Etapa | Skill de superpowers | Qué pasa | Pieza que reutiliza |
|---|---|---|---|
| 1. Brainstorming | `brainstorming` | Preguntas una a la vez hasta entender la idea | Skill (tema 2) |
| 2. Spec | `brainstorming` (la escribe al final) | Lo acordado queda en un archivo | La memoria son archivos (tema 2) |
| 3. Plan | `writing-plans` | Pasos pequeños, cada uno con su "terminado"; al final te pregunta el modo de ejecución | Cómo pedir (tema 1) |
| 4. Ejecución | `subagent-driven-development` (*Subagent-driven*) o `executing-plans` (*Native*) | Un subagente por paso, en una rama | Subagente (tema 2), rama (tema 3) |
| 5. Revisión | `requesting-code-review` + `verification-before-completion` | Otro subagente revisa; nada se da por terminado sin comprobarlo | Segunda opinión limpia (tema 2), el agente no se califica solo (tema 3) |
| 6. Cierre | `finishing-a-development-branch` | Tres opciones: unir en local, push y PR, o dejar la rama como está | PR, `main` y GitHub Pages (tema 3) |

También puedes ver:

- `using-git-worktrees`: pregunta si quieres un *worktree*, una copia de tu carpeta
  en otra rama. En la práctica respondes que no: usas una rama en tu carpeta.
- `test-driven-development`: primero escribe la prueba de "terminado" y luego el
  código.
- `executing-plans`: el modo *Native*; hace todos los pasos en la misma sesión y deja
  una sola revisión al final.

Estos nombres corresponden a superpowers 7. Pueden cambiar entre versiones; la idea
de cada etapa se mantiene.

## Mapa del flujo

Tu guía para las 2 horas de práctica.

| Paso | Qué haces tú | Qué le dices al agente |
|---|---|---|
| 0. Preparar | En la terminal, crea la carpeta (`mkdir mi-proyecto`), entra con `cd mi-proyecto` y abre ahí tu agente. Luego, repo de Git y un `AGENTS.md` corto con el bloque de Git del tema 3 (o `CLAUDE.md`/`GEMINI.md` según tu agente; ver tema 2) | "Inicia un repo de Git aquí, crea el repo en mi GitHub (público si lo voy a publicar en Pages; ver tema 3), súbelo y crea un `AGENTS.md` con…" |
| 1. Idea | Describe tu problema real, no la solución. Te va a ofrecer saltarte las preguntas: di que no | "Quiero hacer brainstorming sobre…" |
| 2. Spec | Lee la spec completa (queda en `docs/superpowers/specs/`); corrige lo que no sea tuyo | "Esto no es lo que quiero: …" |
| 3. Plan | Revisa que cada paso tenga un "terminado" comprobable. Cuando te pregunte el modo de ejecución, elige *Subagent-driven* | "Resúmeme el plan en lenguaje sencillo, un paso por línea, con su 'terminado'." Luego: "Subagent-driven." |
| 4. Ejecución | Si te pregunta por un worktree, di que no: trabaja en una rama nueva en tu carpeta. Lee lo que reporta después de cada paso, y los permisos antes de aceptar | "No, trabaja en una rama nueva en esta carpeta." |
| 5. Revisión | Prueba tú mismo el resultado | "Muéstrame cómo probarlo." |
| 6. Cierre | De las 3 opciones (unir en local, PR, dejar la rama), elige la 2 (PR); revisa el diff en GitHub, pide que lo una y luego que traiga los cambios a tu carpeta. Si es una página y el repo es público, publícala en GitHub Pages con datos de ejemplo. Descartar solo pasa si lo pides | "La 2." Después de revisar: "Une el PR a main." Luego: "Cámbiate a main y trae los cambios." Si es página: "Publícalo en GitHub Pages y dame el enlace." |

### Si te atoras

- **El agente se confunde o se repite:** inicia una sesión nueva y dile "Lee la spec
  y el plan en docs/superpowers/ y continúa desde el paso N." La memoria del agente
  son archivos: no pierdes nada.
- **No hace preguntas antes de construir:** pregúntale "¿Qué skills de superpowers
  tienes?" (como en los requisitos). Si no las enumera, reinicia el agente o revisa la
  instalación. Si las enumera, dile "Usa la skill brainstorming de superpowers."
  Para entender después qué salió mal en una sesión, superpowers tiene otra skill:
  `diagnosing-superpowers`.
- **No ves los cambios:** pregúntale "¿En qué rama estás?" Si sigue en una rama sin
  unir, los cambios aún no están en `main`.
- **Algo falla:** "No adivines: encuentra la causa antes de cambiar algo." Superpowers
  tiene una skill para esto (`systematic-debugging`): primero entiende por qué falla,
  después arregla.
- **Rompió algo:** "Regresa a la última versión que funcionaba; dime qué commit es."
- **No entiendes qué hizo:** "Explícame en lenguaje sencillo qué cambiaste y por qué."
- **El proyecto creció demasiado:** "Ayúdame a recortar esto a lo mínimo que funcione."

> **Para quien presenta:** deja esta slide a la vista al empezar la práctica. Es lo
> que más van a consultar.
