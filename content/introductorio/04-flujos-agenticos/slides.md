# Flujos agénticos y superpowers

Curso introductorio · Tema 4

---

## Donde todo se junta

Ya tienes las piezas de los temas 1 a 3. Falta el **orden**.

---

## El error más común

"Hazme una app de X" → el agente adivina → construye mucho y rápido → no era lo que querías

Mucha **autonomía**, poco **contexto**.

No basta con un mejor pedido: hace falta un mejor **flujo**.

---

## Plugins

Un paquete de piezas del tema 2: skills y, a veces, subagentes, tools o MCPs.

No instalas una función: instalas un **flujo de trabajo completo**.

**Superpowers** (github.com/obra/superpowers): preguntar, escribir lo acordado, planear, revisar, comprobar.

Funciona en Claude Code, Codex, Gemini CLI y otros.

--

## Cómo se activa

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

La regla corta (`using-superpowers`) va **siempre** en la mesa. Cada receta se queda en el cajón **hasta que aplica**.

---

## Spec-driven development

Primero **qué** y **por qué**. Después el **cómo**. Corregir temprano es barato:

```text
Si corriges en…    Te cuesta
Brainstorming      █                  cambiar una respuesta
Spec               ██                 cambiar una frase
Plan               ████               reordenar pasos
Ejecución          ████████           rehacer código
Ya terminado       ████████████████   deshacer y volver a empezar
```

--

## Qué lleva una spec

- **Intención:** el porqué
- **Objetivos:** qué tiene que hacer
- **Lo que NO entra**
- **Lo que la haría un fracaso**, aunque "funcione"

```text
Intención:  No sé en qué se me va el dinero a fin de mes.
Objetivos:  Registrar un gasto con monto y categoría.
            Ver el total por categoría del mes.
No entra:   Cuentas de banco, varias monedas, usuarios.
Fracaso si: Registrar un gasto toma más de 10 segundos.
```

---

## El flujo

```text
   ETAPA           PIEZA QUE USA                   TU PAPEL
1  Brainstorming   skill (tema 2)                  ┐
2  Spec            archivo (tema 2)                ┘ decides
3  Plan            archivo (tema 2)                ┐
4  Ejecución       subagentes + rama (temas 2, 3)  │ supervisas
5  Revisión        subagente limpio (tema 2)       ┘
6  Cierre          rama + PR (tema 3)                apruebas
```

--

## 1. Brainstorming

```text
Tú:      Quiero una app para mis gastos.
Agente:  ¿Qué es lo que te molesta hoy de llevar tus gastos?
Tú:      Que no sé en qué se me va el dinero a fin de mes.
Agente:  Cuéntame la última vez que te pasó.
Tú:      No supe cuánto fue de súper y cuánto de salidas.
Agente:  Entiendo esto: … ¿Qué falta o qué está mal?
```

--

## Lo que acaba de pasar

- **Una pregunta a la vez**
- Pregunta por el **problema**, no por la solución
- **Te devuelve lo que entendió** para que lo corrijas

**No construye nada hasta que apruebes.**

Te va a ofrecer saltarte las preguntas: **di que no**.

Pieza: una **skill** (tema 2) · Tú: **decides**

--

## 2. Spec

- Lo acordado queda en un **archivo**: la memoria del agente son archivos (tema 2)
- La spec, en `docs/superpowers/specs/` (con commit); el plan, en `docs/superpowers/plans/`
- Sobreviven a una sesión nueva, y un subagente con la mesa vacía los puede leer
- Léela completa y corrige lo que no sea tuyo: aquí corregir es más barato

Tú: **decides**

--

## 3. Plan

Pasos pequeños, cada uno con su **terminado** que el agente pueda comprobar.

```text
Paso 2:     Sumar los gastos por categoría.
Terminado:  Con el archivo de prueba, "super" suma 850.
```

"Resúmeme el plan en lenguaje sencillo, un paso por línea, con su 'terminado'"

Pieza: cómo pedir (tema 1) · Tú: **supervisas**

--

## ¿Subagent-driven o Native?

Al terminar el plan te pide revisarlo y te pregunta el modo de ejecución:

- ***Subagent-driven*:** un subagente nuevo por paso, revisado antes de seguir. **Elige este.**
- ***Native*:** el mismo agente hace todo en esta sesión; una sola revisión al final

--

## 4. Ejecución

- Cada paso va a un **subagente** con la mesa limpia (tema 2)
- Todo en una **rama** aparte (tema 3): `main` sigue intacta
- ¿Un *worktree* aislado? **No**: "No, trabaja en una rama nueva en esta carpeta." Ves los cambios en tu carpeta; es la rama del tema 3
- El *worktree* (una copia en `.worktrees/`) sirve si varias personas o agentes trabajan a la vez
- Lee lo que reporta después de cada paso, y los **permisos** (tema 1)

Tú: **supervisas**

--

## 5. Revisión

- Otro subagente revisa: **segunda opinión limpia** (tema 2)
- Nada se declara terminado sin comprobarlo: **el agente no se califica solo** (tema 3)
- Prueba tú el resultado: "muéstrame cómo probarlo"

Tú: **supervisas**

--

## 6. Cierre

Tres opciones: 1. unir a la rama base en local · 2. push y abrir un **PR** · 3. dejar la rama como está

- Elige la **2**: no une nada a `main`. Revisa el **diff** en GitHub y luego pide "une el PR a main"
- Al final: "Cámbiate a main y trae los cambios", para que tu carpeta quede igual que GitHub
- El PR es la forma estándar de colaborar: acostúmbrate desde un proyecto personal
- Página y repo público: publícala en **GitHub Pages**, con datos de ejemplo
- Descartar no es una opción: solo pasa si lo pides

Tú: **apruebas**

---

## Mapa del flujo (0–3)

- **0. Preparar:** `mkdir mi-proyecto`, `cd mi-proyecto` y abre ahí el agente. "Inicia un repo de Git aquí, crea el repo en mi GitHub (público si lo voy a publicar en Pages; ver tema 3), súbelo y crea un `AGENTS.md` con…" el bloque de Git del tema 3 (o `CLAUDE.md`/`GEMINI.md`)
- **1. Idea:** tu **problema**, no la solución. "Quiero hacer brainstorming sobre…" ¿Saltarte las preguntas? **No**
- **2. Spec:** léela completa. "Esto no es lo que quiero: …"
- **3. Plan:** "Resúmeme el plan en lenguaje sencillo, un paso por línea, con su 'terminado'". Modo: **Subagent-driven**

--

## Mapa del flujo (4–6)

- **4. Ejecución:** ¿worktree? "No, trabaja en una rama nueva en esta carpeta." Lee lo que reporta y los permisos
- **5. Revisión:** pruébalo tú. "Muéstrame cómo probarlo."
- **6. Cierre:** "La 2" (PR) → revisa el diff en GitHub → "Une el PR a main." → "Cámbiate a main y trae los cambios." Si es página: "Publícalo en GitHub Pages y dame el enlace."

---

## Si te atoras

- Se confunde → sesión nueva: "Lee la spec y el plan en docs/superpowers/ y continúa desde el paso N"
- No pregunta antes de construir → "¿Qué skills de superpowers tienes?" Si no las enumera, reinicia o revisa la instalación; si sí: "Usa la skill brainstorming de superpowers"
- ¿No ves los cambios? → "¿En qué rama estás?"
- Algo falla → "No adivines: encuentra la causa antes de cambiar algo"
- Rompió algo → "Regresa a la última versión que funcionaba; dime qué commit es"
- No entiendes → "Explícame en sencillo"
- Creció mucho → "Recórtalo a lo mínimo"

---

# A construir

2 horas · tu proyecto · tu flujo

Guía completa: página del tema 4, sección **Mapa del flujo**
