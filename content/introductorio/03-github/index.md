---
title: "3. GitHub en el flujo agéntico"
weight: 3
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

## Por qué importa más con agentes

Un agente puede cambiar diez archivos en un minuto. Eso es poderoso y también
peligroso: si algo sale mal, ¿cómo vuelves a como estaba?

**Git** guarda fotos de tu proyecto. **GitHub** guarda esas fotos en internet.
Juntos son tu botón de deshacer.

## Cuatro palabras

| Palabra | Qué significa |
|---|---|
| **Commit** | Una foto del proyecto con una nota: "agregué la gráfica de gastos". |
| **Branch** (rama) | Una copia paralela para probar algo sin tocar la versión buena. |
| **Push** | Subir tus fotos a GitHub. |
| **Pull request (PR)** | Proponer que una rama se una a la versión principal, con espacio para revisar. |

## El flujo con un agente

1. Antes de un cambio grande: **commit** de lo que funciona.
2. El agente trabaja en una **rama**.
3. Revisas lo que cambió (*diff*): no confíes a ciegas.
4. Si te gusta, **commit** y **push**. Si no, regresas a la foto anterior.

No necesitas memorizar comandos: el agente sabe usar `git` y `gh`. Tu trabajo es
**pedirlo en el momento correcto**:

- "Haz commit de lo que tenemos antes de empezar."
- "Muéstrame qué cambió desde el último commit."
- "Esto no me gustó, regresa al último commit."
- "Sube esto a un repositorio nuevo en mi GitHub."

## Cuándo te sirve

Siempre que el agente vaya a cambiar algo que ya funciona. Commit seguido, commit barato.

## Ejercicio (10 min)

En tu carpeta de los temas anteriores:

1. "Convierte esta carpeta en un repositorio de Git y haz el primer commit."
2. "Crea un repositorio privado en mi GitHub y sube esto."
3. Abre github.com y encuentra tu repositorio.
