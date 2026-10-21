---
title: "1. ¿Qué es un agente?"
weight: 1
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

## Chat vs agente

En la página web, la IA **responde**: tú copias el código, lo pegas, lo pruebas y le
cuentas qué falló. Tú eres sus manos.

Un agente **actúa**: lee tus archivos, ejecuta comandos, edita, revisa el resultado y
corrige. Tú dejas de ser sus manos y te vuelves quien lo dirige.

| | Chat web | Agente en la terminal |
|---|---|---|
| Ve tus archivos | Solo lo que pegas | Toda la carpeta donde lo abres |
| Ejecuta cosas | No | Sí, con tu permiso |
| Verifica su trabajo | No | Sí: corre, lee el error, corrige |
| Tu papel | Copiar y pegar | Decir qué quieres y revisar |

## El ciclo del agente

Un agente repite el mismo ciclo hasta terminar:

1. **Piensa:** ¿qué necesito para cumplir el objetivo?
2. **Actúa:** lee un archivo, ejecuta un comando, escribe código.
3. **Observa:** ¿funcionó? ¿qué dijo el error?

## ¿Por qué en la terminal (CLI)?

La terminal es donde viven tus archivos y tus programas. Si abres el agente en una
carpeta, esa carpeta se vuelve su mesa de trabajo. Todo lo que hace queda en tu
computadora y lo puedes revisar.

## Permisos

El agente te pide permiso antes de hacer algo que cambia tu sistema (editar, borrar,
instalar). **Lee antes de aceptar.** Si no entiendes qué va a hacer, pregúntale.

## Cómo pedirle las cosas

Un buen pedido tiene tres partes:

- **Objetivo:** qué quieres lograr ("una página que muestre mis gastos del mes").
- **Contexto:** lo que el agente no puede adivinar ("los gastos están en `gastos.csv`").
- **Terminado:** cómo sabrás que quedó ("se abre en el navegador y muestra el total").

## Cuándo te sirve

Usa el chat web para preguntas y lluvia de ideas. Usa el agente cuando el resultado
tenga que **existir**: archivos, programas o datos que se queden en tu computadora.

## Ejercicio (5 min)

1. Crea una carpeta vacía y abre tu agente ahí.
2. Pídele: "Explícame qué hay en esta carpeta".
3. Pídele que cree un archivo `notas.md` con tres ideas de proyecto para ti.
4. Ábrelo y confirma que existe.
