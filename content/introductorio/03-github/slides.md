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
main  ●─────────●─────────●───────────────────────────────────●
      inicio    página    datos                               unión
                          │                                   ↑
                          └──●─────────●─────────✗─────────●──┘
                             gráfica   estilo    rompió    arreglo
                                       ↑
                                       aquí regresas
```

Cada **●** = un commit: una foto + una nota que el siguiente agente puede leer.

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
+ Categoría más alta: renta
```

Verde (`+`): se agregó · Rojo (`-`): se quitó

- Es **la** forma de supervisar al agente, como leer la traza en el tema 1
- ¿No lo entiendes? "**Explícame este diff**"

--

## Rama, push y pull request

- **Rama:** un experimento seguro; si sale mal, se tira
- **Push / GitHub:** respaldo en internet + compartir
- **Pull request:** el espacio para revisar antes de unir a `main`

No memorices comandos: el agente sabe usar `git` y `gh`.

---

## GitHub: lugar de trabajo del agente

- **Issues:** lista de tareas que el agente lee → "Resuelve el issue #3"
- **Pull requests:** el agente escribe la descripción; tú (u otro agente con mesa limpia) revisas

--

## Revisiones automáticas

**GitHub Actions:** procesos que corren solos en cada cambio.

**El agente no se califica solo.**

Ejemplo real, este sitio (`.github/workflows/hugo.yaml`). En cada pull request:

1. Prepara una computadora en internet
2. **Compila** todas las páginas
3. Si compiló, las **publica** en GitHub Pages

Si algo se rompe, no se publica nada roto.

--

## GitHub Pages

Publica tu proyecto como página web, **gratis**.

Para tu proyecto de la práctica: el agente hace la página, la sube y la compartes con un enlace.

--

## El espectro otra vez

Hay agentes que viven **dentro de GitHub**:

le asignas un issue → te regresa un pull request.

Más autonomía → ramas, PRs y revisiones automáticas se vuelven indispensables.

---

## Seguridad

- **Nunca subas contraseñas ni API keys.** Una vez en GitHub, considéralas comprometidas (la historia las recuerda)
- **`.gitignore`:** la lista de lo que Git no guarda

```text
.env
```

- **Repo privado** cuando hay datos personales

---

## Tu sección de Git en AGENTS.md

| Frase | ¿Siempre? | Va en |
|---|---|---|
| "Haz commit antes de un cambio grande" | Sí | `AGENTS.md` |
| "Rama nueva, nunca directo en main" | Sí | `AGENTS.md` |
| "Nunca subas contraseñas ni API keys" | Sí | `AGENTS.md` |
| "Notas de commit claras" | Sí | `AGENTS.md` |
| "Muéstrame qué cambió" | No, en el momento | Tu mensaje |
| "Regresa al último commit" | No, en el momento | Tu mensaje |
| "Abre un PR con nuestro formato" | A veces | Skill |

--

## Listo para copiar

```markdown
## Git
- Antes de un cambio grande, haz commit de lo que funciona.
- Trabaja en una rama nueva; nunca directo en main.
- Escribe notas de commit claras: qué cambió y por qué.
- Nunca subas contraseñas, API keys ni archivos .env.
```

- Acota la **autonomía** (tema 1)
- **La memoria son archivos** (tema 2): sobrevive a cada sesión
- Tema 4, paso 0: "crea un `AGENTS.md`" → este bloque va ahí
