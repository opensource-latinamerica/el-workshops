---
title: "1. Anatomía del harness"
weight: 1
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

**Duración:** 15 min. **Al terminar:** puedes distinguir una decisión del modelo
de una acción del programa que lo rodea.

## Apertura · 2 min

Pregunta al grupo: **«Si uso el mismo modelo en dos herramientas, ¿por qué puede
resolver una tarea en una y fallar en la otra?»** Recoge dos respuestas: quizá
recibe información distinta, tiene otras herramientas o cuenta con controles diferentes.

Nos vamos a enfocar en los **harnesses**: cómo configurar y extender lo que organiza
el trabajo alrededor del modelo. No asumimos que tomaste el introductorio.

## Vocabulario compartido · 4 min

| Pieza | Qué significa aquí | En nuestro reporte |
|---|---|---|
| Modelo | Recibe contexto y produce una respuesta o solicitudes de herramientas. | Propone consultar las ventas. |
| Agente | Sistema que combina modelo, herramientas y un ciclo para perseguir un objetivo. | Consulta, observa y decide el siguiente paso. |
| Harness | Software que prepara el contexto, ejecuta herramientas y administra estado, límites y finalización. | Abre el archivo, devuelve resultados y registra el trabajo. |
| Flujo agéntico | Organización de pasos con modelos, herramientas y personas; parte del orden puede estar fijada por código. | Leer → validar → calcular → explicar → revisar. |
| Coding agent | Agente orientado a trabajar con código sobre un harness con herramientas para ese entorno. | Implementa y prueba el programa del reporte. |

Los términos se usan de varias formas en la industria. Estas definiciones son el
vocabulario de trabajo del taller. Un coding agent es el sistema completo; el
harness es su infraestructura de ejecución.

## Una llamada completa · 5 min

El contexto es lo que el modelo recibe **en esa llamada**: instrucciones, mensajes,
definiciones de herramientas y resultados que el harness haya incluido. Un archivo
disponible en disco no está automáticamente en el contexto.

```text
Usuario: compara las ventas de septiembre y octubre.
Harness: prepara el contexto y llama al modelo.
Modelo: solicita leer ventas.csv.
Harness: ejecuta la herramienta; devuelve el contenido.
Modelo: solicita calcular totales por mes.
Harness: ejecuta el cálculo; devuelve 1500 y 2000 MXN.
Modelo: redacta una comparación.
Harness: entrega la respuesta o aplica controles de cierre configurados.
```

Esta es una **traza didáctica**, no una ejecución registrada. El modelo solicita;
el programa hace la operación. Las herramientas pueden fallar y el siguiente paso
debe partir de su resultado real.

Una instrucción de «revisa antes de terminar» y una comprobación obligatoria en el
programa son cosas distintas. Volveremos a esa diferencia en el tema 5.

> **Para quien presenta:** lee la traza señalando quién actúa en cada línea. No
> expliques todavía todos los formatos de la API. Si abres código, muestra solo el
> ciclo: llamar al modelo → ejecutar solicitudes → agregar resultados → continuar.

## Dos trabajos distintos · 2 min

En el taller podemos usar un agente para **construir** el programa del reporte.
Después, ese programa puede hacer los cálculos sin volver a llamar al modelo.
También podemos añadir un modelo a la ejecución para explicar resultados.

Decide dónde aporta criterio el modelo y qué debe quedar como código repetible.
No toda automatización necesita un agente en cada paso.

## Comprobación · 2 min

Pregunta: **«El agente asegura que guardó el reporte, pero no existe el archivo.
¿Qué revisarías?»**

Respuesta esperada: si hubo solicitud de escritura, si la herramienta se ejecutó,
qué resultado devolvió y en qué ruta. Una afirmación del modelo no prueba una acción.

**Transición:** ya sabemos quién ejecuta. Ahora vamos a elegir qué información y
capacidades necesita para hacer bien el trabajo.

Fuentes: [CMU, Agents, pp. 9–15 y 26–27](https://www.cmu-agents.com/slides/lecture-01-agents.pdf)
y [Tool use sin abstracciones, Carlos Haro](https://h1sort.com/claude4aieng/).
