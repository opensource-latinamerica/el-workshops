# GitHub en el flujo agéntico

Curso introductorio · Tema 3

---

## Del tema 2 a este

**La memoria del agente son archivos.**

¿Y si cambia diez archivos en un minuto y uno quedó mal?

- **Git:** guarda la historia de esos archivos
- **GitHub:** la pone en internet para que otros (personas o agentes) la revisen

---

## Por qué importa más con agentes

- **Velocidad:** cambia mucho y rápido; los errores también
- **Se equivoca con total seguridad:** necesitas puntos de regreso
- **Revisas qué cambió**, no todo el proyecto

Más **autonomía** (tema 1) → más necesitas una red.

---

## La historia de un proyecto

```text
main  ●─────────●─────────●───────────────────────────●
      inicio    página    datos                       unión
                          │                           ↑
                          └──●─────────●─────────●────┘
                             gráfica   estilo    arreglo
```

Cada **●** = un commit: una foto + una nota que el siguiente agente puede leer.

--

## La historia de un proyecto

```text
main  ●─────────●─────────●───────────────────────────●
      inicio    página    datos                       unión
                          │                           ↑
                          └──●─────────●─────────●────┘
                             gráfica   estilo    arreglo
                                       ╲
                                        ✗ rompió (sin commit: se tira)
```

El **✗** son cambios sin guardar que rompieron algo. Los tiras, regresas al último commit (*estilo*) y desde ahí el agente hace *arreglo*.

---

## Repo y commit

- **Repo:** la carpeta con memoria
- **Commit:** una foto con nota

**La nota es memoria para el siguiente agente.** Sesión nueva = mesa vacía, pero el historial está escrito:

```text
Tú: Lee el historial y dime dónde nos quedamos.
```

--

## Diff: lo que cambió

```diff
  Total del mes: $4,320
- Moneda: USD
+ Moneda: MXN
+ Categoría más alta: super
```

Verde (`+`): se agregó · Rojo (`-`): se quitó

Cambiar una línea = quitar la vieja (`-`) y agregar la nueva (`+`)

- Es **la** forma de supervisar al agente, como leer la traza en el tema 1
- ¿No lo entiendes? "**Explícame este diff**"

--

## Rama, push y pull request

- **Rama:** un experimento seguro; si sale mal, se tira
- **Push / GitHub:** respaldo en internet + compartir
- **Pull request:** el espacio para revisar antes de unir a `main`

No memorices comandos: el agente sabe usar `git` y `gh`.

---

## GitHub: donde recibe tareas y lo revisan

- **Issues:** lista de tareas que el agente lee → "Resuelve el issue #3"
- **Pull requests:** el agente escribe la descripción; tú (u otro agente con mesa limpia) revisas

--

## Revisiones automáticas

**GitHub Actions:** procesos que corren solos cuando algo cambia.

**El agente no se califica solo:** una revisión automática lo comprueba. Aquí, al menos que compile.

Ejemplo real, este sitio (`.github/workflows/hugo.yaml`). En cada pull request y en cada cambio en `main`:

1. Prepara una computadora en internet
2. **Compila** (arma todas las páginas)
3. Si compiló, las **publica** en GitHub Pages

Si no compila, no se publica. En este curso cada PR se publica para verlo en línea; en muchos proyectos solo lo que entra a `main`.

--

## GitHub Pages

Publica tu proyecto como página web, **gratis**.

Si tu proyecto es una página web: "**Publícalo en GitHub Pages y dame el enlace**"

La página que publiques la puede ver cualquiera. Si tu proyecto tiene datos personales, usa datos de ejemplo.

--

## El espectro otra vez

Hay agentes que viven **dentro de GitHub**:

le asignas un issue → te regresa un pull request.

Dan todavía más pasos sin ti → ramas, PRs y revisiones automáticas se vuelven indispensables.

---

## Seguridad

- **Nunca subas contraseñas ni API keys** (llaves de acceso a servicios). Una vez en GitHub, considéralas comprometidas (la historia las recuerda)
- **`.gitignore`:** la lista de lo que Git no guarda. Créalo antes del primer commit: no borra lo que ya se subió

```text
.env
```

- **Repo privado** cuando hay datos personales (en cuenta gratis, no se puede publicar con Pages)

---

## Tu sección de Git en AGENTS.md

¿`AGENTS.md`, tu mensaje o skill?

| Frase | ¿Qué es? |
|---|---|
| "Haz commit antes de un cambio grande" | Regla de siempre |
| "Rama nueva, nunca directo en main" | Regla de siempre |
| "Nunca subas contraseñas ni API keys" | Regla de siempre |
| "Notas de commit claras" | Regla de siempre |
| "Muéstrame qué cambió" | Pedido de ahora |
| "Regresa al último commit" | Pedido de ahora |
| "Abre un PR con nuestro formato" | Procedimiento con pasos |

--

## Tu sección de Git en AGENTS.md

| Frase | ¿Qué es? | Va en |
|---|---|---|
| "Haz commit antes de un cambio grande" | Regla de siempre | `AGENTS.md` |
| "Rama nueva, nunca directo en main" | Regla de siempre | `AGENTS.md` |
| "Nunca subas contraseñas ni API keys" | Regla de siempre | `AGENTS.md` |
| "Notas de commit claras" | Regla de siempre | `AGENTS.md` |
| "Muéstrame qué cambió" | Pedido de ahora | Tu mensaje |
| "Regresa al último commit" | Pedido de ahora | Tu mensaje |
| "Abre un PR con nuestro formato" | Procedimiento con pasos | Skill |

Lo de una sola vez va en tu mensaje, igual que el pedido del tema 1.

--

## Listo para copiar

```markdown
## Git
- Antes de un cambio grande, haz commit de lo que funciona.
- Trabaja en una rama nueva; nunca directo en main.
- Escribe notas de commit claras: qué cambió y por qué.
- Nunca subas contraseñas, API keys ni archivos .env.
- Agrega .env a .gitignore antes del primer commit.
- Cuando algo funcione, abre un PR y únelo a main cuando yo lo apruebe.
```

En `AGENTS.md`, o `CLAUDE.md`/`GEMINI.md` según tu agente (ver tema 2).

- Acota la **autonomía** (tema 1)
- **La memoria son archivos** (tema 2): sobrevive a cada sesión
- Tema 4, paso 0: "crea un `AGENTS.md`" → este bloque va ahí
