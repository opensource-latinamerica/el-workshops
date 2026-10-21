# Flujos agénticos y superpowers

Curso introductorio · Tema 4

---

## Donde todo se junta

- **Tema 1:** qué es un agente y cómo pedirle las cosas
- **Tema 2:** la mesa y las cinco piezas
- **Tema 3:** Git y GitHub como red

Ya tienes las piezas. Falta el **orden**.

---

## El error más común

"Hazme una app de X" → el agente adivina → construye mucho y rápido → no era lo que querías

Mucha **autonomía**, poco **contexto**.

La solución no es un mejor pedido: es un mejor **flujo**.

---

## Plugins

Un paquete de piezas del tema 2: skills y, a veces, subagentes, tools o MCPs.

No instalas una función: instalas un **flujo de trabajo completo**.

**Superpowers** (github.com/obra/superpowers): preguntar, escribir lo acordado, planear, revisar, comprobar.

Funciona en Claude Code, Codex y otros.

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

Cada receta sale del cajón **cuando hace falta**.

---

## Spec-driven development

Primero **qué** y **por qué**. Después el **cómo**.

--

## Corregir temprano es barato

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

--

## La spec es un archivo

**La memoria del agente son archivos** (tema 2).

La spec y el plan sobreviven a una sesión nueva, y un subagente con la mesa vacía los puede leer.

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
Agente:  ¿Te serviría más ver categorías o ver cómo cambia mes a mes?
Tú:      Categorías.
Agente:  Entiendo esto: … ¿Qué falta o qué está mal?
```

--

## Lo que acaba de pasar

- **Una pregunta a la vez**
- Pregunta por el **problema**, no por la solución
- **Te devuelve lo que entendió** para que lo corrijas

**No construye nada hasta que apruebes.**

Pieza: una **skill** (tema 2) · Tú: **decides**

--

## 2. Spec

- Lo acordado queda en un **archivo**
- Léela completa; corrige lo que no sea tuyo
- Aquí corregir es más barato

Pieza: la memoria son archivos (tema 2) · Tú: **decides**

--

## 3. Plan

Pasos pequeños, cada uno con su **terminado** que el agente pueda comprobar.

```text
Paso 2:     Sumar los gastos por categoría.
Terminado:  Con el archivo de prueba, "super" suma 850.
```

Pieza: cómo pedir (tema 1) · Tú: **supervisas**

--

## 4. Ejecución

- Cada paso va a un **subagente** con la mesa limpia (tema 2)
- Todo en una **rama** aparte (tema 3): `main` sigue intacta
- Lee la **traza** y acepta los **permisos** con cuidado (tema 1)

Tú: **supervisas**

--

## 5. Revisión

- Otro subagente revisa: **segunda opinión limpia** (tema 2)
- Nada se declara terminado sin comprobarlo: **el agente no se califica solo** (tema 3)
- Prueba tú el resultado: "muéstrame cómo probarlo"

Tú: **supervisas**

--

## 6. Cierre

- **PR** y unión a `main`, o descartar la rama (tema 3)
- Si es una página: publícala en **GitHub Pages**
- Revisa el **diff** antes de unir

Tú: **apruebas**

---

## Mapa del flujo

0. Preparar: carpeta, repo, `AGENTS.md` con el bloque de Git (o `CLAUDE.md`/`GEMINI.md`; ver tema 2)
1. Idea: describe tu **problema**, no la solución
2. Spec: léela completa y corrige
3. Plan: pasos pequeños y comprobables
4. Ejecución: lee la traza y los permisos
5. Revisión: pruébalo tú
6. Cierre: revisa el diff, abre un PR y únelo a `main`; si es una página, publícala en GitHub Pages

---

## Si te atoras

- Se confunde → sesión nueva: "Lee la spec y el plan, y continúa desde el paso N"
- Algo falla → "No adivines: encuentra la causa antes de cambiar algo"
- Rompió algo → "Regresa al último commit"
- No entiendes → "Explícame en sencillo"
- Creció mucho → "Recórtalo a lo mínimo"

---

# A construir

2 horas · tu proyecto · tu flujo
