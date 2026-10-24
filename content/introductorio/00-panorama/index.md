---
title: "0. Panorama: del chat al agente"
weight: 1
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

Un resumen de lo que veremos y por qué. Si te llevas una sola idea, que sea esta:
**el problema de fondo es el contexto.** Hoy vamos a aprender sobre cómo darle al agente la información que necesita para decidir como tú lo harías.

## Hoy cada vez es más fácil usar agentes

Claude Desktop, ChatGPT con Codex han ayudado a más personas a superar la etapa del chatbot en la página web.

Leen archivos de tu computadora, se conectan a Google Drive, a tu correo o a tu
calendario. La distancia entre "platicar con la IA" y "que trabaje con tus cosas" es
cada vez más corta (en el tema 1 lo veremos como un espectro).

Pero la pregunta importante no es qué app usar. Queremos que sean ***model agnostic***, es decir, que conozcan los fundamentales para que puedan moverse entre los diferentes proveedores como mejor les convenga: la más barata, o la que tenga el modelo más capaz, o la que vaya más acorde a sus principios.

El fundamental más importante es el **contexto**: qué información le das al agente para que decida como tú lo harías.

## Cambió el idioma, no la forma de pensar

A quienes programaban antes de la IA se les hizo más fácil usar agentes. No por saber
un lenguaje de programación, sino por algo que aprendieron a la mala: **la computadora
no hace nada que no le pidas de forma explícita.** Si tu lógica tenía un hueco, la
computadora lo ejecutaba tal cual. Eso es un *bug*, y aprender a encontrarlos es
aprender a pensar en pasos.

- **Antes:** había que hablar el idioma de la computadora (una sintaxis de lenguaje de programación; dígase Python, JavaScript, C++).
- **Ahora:** le puedes hablar en español.
- **Lo que no cambió:** pensar en sistemas, en orden, en pasos, en qué depende de qué.

Por algún tiempo a esta última práctica se le comenzó a llamar *prompt engineering*. Hoy en día el término está cayendo en desuso porque nos dimos cuesta que básicamente se trata de lo mismo de siempre:
pensar con estructura: qué quiero, en qué orden, qué cuenta como terminado y qué
puede salir mal.

## Hay que cerrar la brecha entre lo que vive en nuestra cabeza y lo que el agente ve

Los modelos se han vuelto tan buenos que olvidamos la **asimetría de información**. Tú sabes
tu caso de uso específico qué es, quién lo va a usar, qué ya intentaste y qué te importa. El agente solo sabe lo que le escribiste o lo que encuentra.

La habilidad que vamos a desarrollar: bajar lo que tienes en la cabeza a descripciones
ricas, para que el agente tome las decisiones que tú habrías tomado.

## Darle contexto…

Entonces parece que la respuesta a todos los males es darle el mejor contexto posible. Es parte de lo
que vas a aprender, y hoy es un campo de investigación activo. 

Un ejemplo son los
*knowledge graphs* (grafos de conocimiento): la hipótesis de que el agente encuentra
mejor lo que necesita si la información está organizada como nodos conectados, y él
se mueve de un dato a los que se relacionan con él.

Para manejar el contexto existen piezas concretas:
- tools
- skills
- MCP
- subagentes 
- AGENTS.md (o MEMORY.md)

Las estudiaremos

## …pero no podemos meter todo como licuadora

La ventana de contexto tiene un límite natural: así como nos quedamos sin espacio de memoria en el celular, a los agentes les pasa lo mismo con los tokens (tema 2). E incluso antes de llegar a ese límite, hay 2 problemas principales:

1. **Context rot** Entre más carga la conversación, peor
   piensa y actúa el agente. No espera a que se llene: hay quien lo nota desde un 20% del contexto (~200k tokens con los límites actuales de 1M tokens).
2. **Costo.** Cada mensaje reenvía toda la conversación, así que cada mensaje nuevo
   cuesta más que el anterior. En una suscripción lo ves como uso: seguir escribiendo mensaje en una conversación larga hace que llegues al límite de uso más rápido.

```text
Poco contexto         Punto óptimo              Demasiado contexto
adivina lo que   →    decide como tú lo    →    se confunde
quieres               harías, a buen costo      y cuesta más
```

Usar bien un agente es desarrollar **criterio** sobre ese equilibrio: el contexto
suficiente para que decida bien, sin pasarte al punto en que se degrada o se
encarece.

## La memoria son archivos

El agente no recuerda nada entre sesiones. Lo que sobrevive es lo que quedó escrito
en archivos. Por eso necesitas dos herramientas (tema 3):

- **Git** guarda versiones de esos archivos. Si algo sale mal, regresas. Si algo sale
  bien y pasa tus revisiones, lo guardas y sabes que puedes usarlo sin rehacerlo.
- **GitHub** pone esa historia en la nube. Es como un Google Drive, pero hecho para
  código y para los archivos que usa el agente.

## El mapa del curso

| Tema | La pregunta que responde |
|---|---|
| [1. ¿Qué es un agente?](../01-agentes/) | ¿Qué cambia cuando la IA puede actuar? |
| [2. Contexto y herramientas](../02-contexto-y-herramientas/) | ¿Qué ve el agente y cómo lo controlo? |
| [3. GitHub](../03-github/) | ¿Cómo guardo, deshago y comparto lo que hace? |
| [4. Flujos agénticos](../04-flujos-agenticos/) | ¿Cómo junto todo para construir algo? |

