---
title: "Antes de la sesión: requisitos"
weight: 0
---

Haz esto **antes** de llegar. En el salón solo verificamos que funcione.

## 1. Abre una terminal

- **macOS:** app *Terminal* (Cmd + Espacio, escribe "Terminal").
- **Windows:** instala [WSL](https://learn.microsoft.com/es-mx/windows/wsl/install) y abre *Ubuntu*.
- **Linux:** tu terminal de siempre.

Tres comandos que basta con conocer:

```sh
pwd        # ¿en qué carpeta estoy?
ls         # ¿qué hay aquí?
cd carpeta # entrar a una carpeta (cd .. para salir)
```

## 2. Git y GitHub

1. Crea una cuenta en [github.com](https://github.com).
2. Instala [Git](https://git-scm.com/downloads) y la CLI de GitHub, [`gh`](https://cli.github.com).
3. Inicia sesión:

```sh
gh auth login
```

## 3. Un agente en la terminal

Elige **uno**. Todo lo del curso aplica a cualquiera de ellos.

| Agente | Costo | Instalación |
|---|---|---|
| [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) | Requiere plan de pago de Claude o API key | Ver documentación oficial |
| [Codex CLI](https://github.com/openai/codex) | Incluido en planes de ChatGPT o con API key | Ver documentación oficial |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | Tiene capa gratuita con cuenta de Google | Ver documentación oficial |

Después de instalarlo, ábrelo una vez desde la terminal e inicia sesión.

## 4. Superpowers

Instala el plugin [superpowers](https://github.com/obra/superpowers) siguiendo las
instrucciones de su README para tu agente.

## Verifica que todo funciona

- [ ] `git --version` muestra una versión.
- [ ] `gh auth status` dice que iniciaste sesión.
- [ ] Abres tu agente en una carpeta vacía y responde a "¿qué hay en esta carpeta?".
- [ ] Le preguntas a tu agente "¿qué skills de superpowers tienes?" y las enumera.
