---
title: "3. GitHub en el flujo agéntico"
weight: 3
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

## Del tema 2 a este

En el tema 2 vimos que **la memoria del agente son archivos**. Lo que no quedó
escrito, se pierde al cerrar la sesión.

Ahora la otra cara: ¿qué pasa cuando el agente cambia diez archivos en un
minuto y uno quedó mal? ¿Cómo sabes cuál fue? ¿Cómo vuelves a como estaba?

- **Git** guarda la historia de esos archivos: cada versión, con una nota.
- **GitHub** pone esa historia en internet, donde otros (personas o agentes) pueden
  verla y revisarla.

## Por qué importa más con agentes

- **Velocidad.** El agente cambia mucho y rápido. Los errores se esparcen igual de
  rápido.
- **Se equivoca con total seguridad.** No te avisa "aquí no estoy seguro". Necesitas
  puntos a los que puedas regresar.
- **Revisas qué cambió, no todo el proyecto.** Leer cinco líneas nuevas es posible.
  Releer todo el proyecto después de cada pedido, no.

En el tema 1 vimos que la **autonomía** es parte de lo que hace a un agente: tú das el
objetivo y él decide los pasos. Entre más autonomía le das, más necesitas una red.
Git es esa red.

## La historia de un proyecto

Así se ve la historia de un proyecto pequeño, una página de gastos:

```text
main  ●─────────●─────────●───────────────────────────●
      inicio    página    datos                       unión
                          │                           ↑
                          └──●─────────●─────────●────┘
                             gráfica   estilo    arreglo
                                       ╲
                                        ✗ rompió (sin commit: se tira)
```

Cada **●** es un commit: una foto del proyecto más una nota que el siguiente agente
puede leer. El **✗** son cambios sin guardar que rompieron algo. Los tiras, regresas al
último commit (*estilo*) y desde ahí el agente hace *arreglo*. Al final, la rama se une
de vuelta a `main`.

Con este dibujo se explican todas las palabras que siguen.

> **Para quien presenta:** dibuja la historia en el pizarrón poco a poco, un ● a la
> vez, mientras cuentas la historia: "empecé, hice la página, cargué los datos…".
> Deja el ✗ para el final y pregunta: "¿a dónde regreso?".

## Vocabulario

### Repo: la carpeta con memoria

Un **repositorio** (repo) es una carpeta normal donde Git guarda la historia. Por
fuera se ve igual. Por dentro recuerda cada versión.

### Commit: una foto con nota

Un **commit** es una foto de todos los archivos en un momento, con una nota:
"agregué la gráfica de gastos".

**La nota es memoria para el siguiente agente.** En el tema 2 vimos que una sesión
nueva es una mesa vacía. Pero el historial está escrito, así que el agente lo puede
leer:

```text
Tú: Lee el historial de commits y dime dónde nos quedamos.
```

Por eso importa que las notas sean claras. "cambios" no le dice nada a nadie.
"Agrega gráfica de gastos por categoría" sí.

### Diff: lo que cambió

Un **diff** muestra la diferencia entre dos fotos. Lo que se agregó aparece en
**verde** (con `+`); lo que se quitó, en **rojo** (con `-`).

```diff
  Total del mes: $4,320
- Moneda: USD
+ Moneda: MXN
+ Categoría más alta: super
```

Se cambió la moneda y se agregó una línea. Lo demás quedó igual. Cambiar una línea =
quitar la vieja (`-`) y agregar la nueva (`+`).

El diff es **la** forma de supervisar al agente. En el tema 1 leíamos la traza para
ver qué pidió y qué le devolvieron. El diff es lo mismo para los archivos: qué dejó
cambiado al final.

Si no lo entiendes, pídelo:

```text
Tú: Explícame este diff en palabras simples.
```

### Rama: un experimento seguro

Una **rama** es una línea paralela de la historia. Pruebas algo sin tocar la versión
buena (`main`). Si sale bien, la unes. Si sale mal, la tiras y `main` sigue intacta.

### Push y GitHub: respaldo y compartir

**Push** es subir tus commits a GitHub. Sirve para dos cosas:

- **Respaldo:** si tu computadora falla, la historia sigue en internet.
- **Compartir:** otras personas (y otros agentes) pueden verla.

### Pull request: revisar antes de unir

Un **pull request** (PR) es una propuesta: "quiero unir esta rama a `main`". Es el
espacio para revisar el diff, comentar y corregir **antes** de que el cambio llegue a
la versión buena.

No necesitas memorizar comandos: el agente sabe usar `git` y `gh` (la herramienta de
GitHub para la terminal). Tú le pides el qué; él escribe el cómo.

## GitHub: donde el agente recibe tareas y lo revisan

GitHub no solo guarda archivos. Es un lugar donde el agente puede leer tareas,
proponer cambios y ser revisado.

### Issues: la lista de tareas

Un **issue** es una tarea o un problema escrito en GitHub, con número. El agente lo
puede leer como cualquier archivo:

```text
Tú: Resuelve el issue #3.
```

El agente lee la descripción, hace el cambio y te dice qué hizo. La tarea ya está
escrita: no tienes que volver a explicarla.

### Pull requests: el agente propone, alguien revisa

El agente puede abrir el PR y escribir su descripción: qué cambió y por qué. Luego
alguien revisa:

- **Tú**, leyendo el diff.
- **Otro agente o un subagente**, con la mesa limpia (tema 2). No carga los supuestos
  de quien hizo el cambio, así que ve cosas que el primero no vio.

### Revisiones automáticas: GitHub Actions

**GitHub Actions** son procesos que corren solos cuando algo cambia: pruebas, revisiones,
publicar algo. Nadie tiene que acordarse de correrlos.

La idea clave: **el agente no se califica solo.** Si dice "ya funciona", una revisión
automática lo comprueba; en este sitio, al menos que compile: si no compila, no se
publica.

**Ejemplo real: este mismo sitio.** El curso que estás leyendo vive en un repo de
GitHub. Tiene un archivo de instrucciones para GitHub Actions
(`.github/workflows/hugo.yaml`) que dice:

1. En cada pull request (cuando se abre o se actualiza) y en cada cambio en `main`,
   prepara una computadora en internet.
2. Instala el programa que arma el sitio y **compila** (arma todas las páginas).
3. Si compila bien, las **publica** en GitHub Pages.

En este curso cada PR se publica para poder verlo en línea; en muchos proyectos solo
se publica lo que entra a `main`.

Si un cambio rompe el sitio, el paso 2 falla y no se publica nada roto. Nadie tuvo que
revisarlo a mano.

### GitHub Pages: tu proyecto como página web

**GitHub Pages** publica los archivos de un repo como una página web, gratis. Si tu
proyecto de la práctica es una página web, sirve directo: el agente hace la página, la
sube a GitHub y cualquiera la puede abrir con un enlace. Pídelo así:

```text
Tú: Publícalo en GitHub Pages y dame el enlace.
```

La página que publiques la puede ver cualquiera. Si tu proyecto tiene datos
personales, usa datos de ejemplo.

### El espectro otra vez

En el tema 1 vimos que agente es un espectro. Hay agentes que viven **dentro de
GitHub**: le asignas un issue y, sin que abras la terminal, te regresa un pull request
listo para revisar. Por ejemplo, Copilot, Claude o Codex tienen versiones que trabajan
así.

Ahí los agentes dan todavía más pasos sin ti. Por eso todo lo anterior (ramas, PRs,
revisiones automáticas) se vuelve indispensable: es la forma de revisarlo.

## Seguridad

- **Nunca subas contraseñas ni API keys** (llaves de acceso a servicios, a veces de
  pago). El agente puede hacerlo por accidente si
  están en un archivo de la carpeta. Una vez en GitHub, considéralas comprometidas:
  cámbialas, aunque las borres después. La historia las recuerda.
- **`.gitignore`** es la lista de lo que Git no guarda. Por ejemplo, el archivo `.env`,
  donde suelen vivir las llaves:

  ```text
  .env
  ```

  Tiene que existir antes del primer commit: `.gitignore` no borra lo que ya se subió.

- **Repos privados** cuando el proyecto tenga datos personales o algo que no quieras
  mostrar. Público, cualquiera lo ve. Ojo: en una cuenta gratis, un repo privado no se
  puede publicar con GitHub Pages.

> **Para quien presenta:** pregunta "¿qué pasa si borro la contraseña en el siguiente
> commit?". La respuesta (sigue en la historia) es lo que hace que la regla se quede.

## Tu sección de Git en AGENTS.md

En el tema 2 vimos **dónde va cada cosa**. Apliquémoslo a frases de Git:

| Frase | ¿Qué es? | Va en |
|---|---|---|
| "Haz commit antes de un cambio grande" | Regla de siempre | `AGENTS.md` |
| "Trabaja en una rama nueva, nunca directo en main" | Regla de siempre | `AGENTS.md` |
| "Nunca subas contraseñas ni API keys" | Regla de siempre | `AGENTS.md` |
| "Escribe notas de commit claras: son la memoria del siguiente agente" | Regla de siempre | `AGENTS.md` |
| "Muéstrame qué cambió" | Pedido de ahora | Tu mensaje |
| "Regresa al último commit" | Pedido de ahora | Tu mensaje |
| "Abre un PR con nuestro formato: por qué y qué cambió" | Procedimiento con pasos | Skill |

Lo de una sola vez va en tu mensaje, igual que el pedido del tema 1.

El bloque listo para copiar (en `AGENTS.md`, o `CLAUDE.md`/`GEMINI.md` según tu
agente; ver tema 2):

```markdown
## Git
- Antes de un cambio grande, haz commit de lo que funciona.
- Trabaja en una rama nueva; nunca directo en main.
- Escribe notas de commit claras: qué cambió y por qué.
- Nunca subas contraseñas, API keys ni archivos .env.
- Agrega .env a .gitignore antes del primer commit.
- Cuando algo funcione, abre un PR y únelo a main cuando yo lo apruebe.
```

Por qué funciona:

- **Acota la autonomía** (tema 1): el agente sigue decidiendo los pasos, pero dentro
  de una red.
- **La memoria son archivos** (tema 2): estas reglas viven en `AGENTS.md`, así que
  sobreviven a cada sesión nueva.
- **Lo vas a usar en el tema 4:** el paso 0 del flujo es "crea un `AGENTS.md`". Este
  bloque va ahí.

> **Para quien presenta:** antes de mostrar la columna "Va en", lee cada frase y que
> el grupo vote: ¿`AGENTS.md`, mensaje o skill?
