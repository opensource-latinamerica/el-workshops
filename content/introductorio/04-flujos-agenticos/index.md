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

La solución no es un mejor pedido: es un mejor **flujo**.

## Plugins

Un **plugin** es un paquete de piezas del tema 2 que alguien ya armó: skills y, a
veces, subagentes, tools o MCPs. Lo instalas una vez.

La diferencia con instalar una pieza suelta: con un plugin no instalas una función,
instalas un **flujo de trabajo completo**. Las piezas vienen pensadas para usarse
juntas y en orden.

[Superpowers](https://github.com/obra/superpowers) es un plugin que le enseña al agente
a trabajar como un buen equipo: preguntar antes de construir, escribir lo acordado,
planear, revisar y comprobar. Funciona en varios agentes: Claude Code, Codex y otros.
Lo instalaste en los requisitos.

### Cómo se activa

Recuerda la mesa del tema 2: de cada skill, en la mesa solo están el nombre y la
descripción. El resto se queda en el cajón hasta que hace falta.

Superpowers aprovecha eso. Al iniciar la sesión carga una skill (`using-superpowers`)
que le dice al agente: **"antes de actuar, revisa si alguna de tus skills aplica"**.

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

```text
Tú:      Quiero una app para mis gastos.
Agente:  ¿Qué es lo que te molesta hoy de llevar tus gastos?
Tú:      Que no sé en qué se me va el dinero a fin de mes.
Agente:  ¿Te serviría más ver categorías o ver cómo cambia mes a mes?
Tú:      Categorías.
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
> 1. Detente en la segunda pregunta: el agente ofrece dos caminos en lugar de elegir
> uno por ti.

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

- **Tu papel:** supervisas. Revisa que los pasos sean pequeños y que cada uno se
  pueda comprobar.

### 4. Ejecución

Cada paso del plan va a un **subagente** con la mesa limpia (tema 2): lee la spec y
su paso, lo hace y regresa el resultado. Tu mesa no se llena con el desorden de cada
paso. Todo pasa en una **rama** aparte (tema 3), así que `main` sigue intacta.

- **Tu papel:** supervisas. Lee la **traza** para ver qué pide y qué le devuelven
  (tema 1), y acepta los **permisos** con cuidado: lee antes de aceptar.

### 5. Revisión

Otro subagente revisa el trabajo con una **segunda opinión limpia** (tema 2): no
carga los supuestos de quien lo hizo. Y nada se declara terminado sin comprobarlo:
**el agente no se califica solo** (tema 3).

- **Tu papel:** supervisas. Prueba tú mismo el resultado; si no sabes cómo, pídele
  "muéstrame cómo probarlo".

### 6. Cierre

El agente te pregunta qué hacer con la rama: abrir un **PR** y unirlo a `main`, o
descartarla (tema 3). Si tu proyecto es una página, se puede publicar en **GitHub
Pages**.

- **Tu papel:** apruebas. Revisa el **diff** antes de unir.

### Los nombres de las skills

En la práctica vas a ver al agente decir los nombres de las skills que usa. Así se
corresponden:

| Etapa | Skill de superpowers | Qué pasa | Pieza que reutiliza |
|---|---|---|---|
| 1. Brainstorming | `brainstorming` | Preguntas una a la vez hasta entender la idea | Skill (tema 2) |
| 2. Spec | `brainstorming` (la escribe al final) | Lo acordado queda en un archivo | La memoria son archivos (tema 2) |
| 3. Plan | `writing-plans` | Pasos pequeños, cada uno con su "terminado" | Cómo pedir (tema 1) |
| 4. Ejecución | `subagent-driven-development` | Un subagente por paso, en una rama | Subagente (tema 2), rama (tema 3) |
| 5. Revisión | `requesting-code-review` + `verification-before-completion` | Otro subagente revisa; nada se da por terminado sin comprobarlo | Segunda opinión limpia (tema 2), el agente no se califica solo (tema 3) |
| 6. Cierre | `finishing-a-development-branch` | PR y unión a `main`, o descartar | PR, `main` y GitHub Pages (tema 3) |

Estos nombres corresponden a superpowers 7. Pueden cambiar entre versiones; la idea
de cada etapa se mantiene.

## Mapa del flujo

Tu guía para las 2 horas de práctica.

| Paso | Qué haces tú | Qué le dices al agente |
|---|---|---|
| 0. Preparar | Carpeta nueva, repo de Git y un `AGENTS.md` corto con el bloque de Git del tema 3 (o `CLAUDE.md`/`GEMINI.md` según tu agente; ver tema 2) | "Inicia un repo de Git aquí y crea un `AGENTS.md` con…" |
| 1. Idea | Describe tu problema real, no la solución | "Quiero hacer brainstorming sobre…" |
| 2. Spec | Lee la spec completa; corrige lo que no sea tuyo | "Esto no es lo que quiero: …" |
| 3. Plan | Revisa que los pasos sean pequeños y comprobables | "Escribe el plan." |
| 4. Ejecución | Lee la traza; acepta permisos leyendo | "Ejecuta el plan." |
| 5. Revisión | Prueba tú mismo el resultado | "Muéstrame cómo probarlo." |
| 6. Cierre | Revisa el diff, abre un PR y únelo a `main`; si es una página, publícala en GitHub Pages | "Haz commit, abre un PR y, cuando lo apruebe, únelo a main y publícalo en GitHub Pages." |

### Si te atoras

- **El agente se confunde o se repite:** inicia una sesión nueva y dile "Lee la spec
  y el plan, y continúa desde el paso N." La memoria del agente son archivos: no
  pierdes nada.
- **Algo falla:** "No adivines: encuentra la causa antes de cambiar algo." Superpowers
  tiene una skill para esto (`systematic-debugging`): primero entiende por qué falla,
  después arregla.
- **Rompió algo:** "Regresa al último commit."
- **No entiendes qué hizo:** "Explícame en lenguaje sencillo qué cambiaste y por qué."
- **El proyecto creció demasiado:** "Ayúdame a recortar esto a lo mínimo que funcione."

> **Para quien presenta:** deja esta slide a la vista al empezar la práctica. Es lo
> que más van a consultar.
