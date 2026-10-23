---
title: "1. ¿Qué es un agente?"
weight: 1
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

## El mismo modelo, dos resultados

Pide lo mismo al mismo modelo en la página web y en la terminal. En la web te da
código y te toca a ti ver si funciona. En la terminal lo escribe, lo prueba, ve el
error y lo arregla. ¿Por qué tanta diferencia si el modelo es el mismo?

La respuesta: **quién cierra el ciclo**.

- En el **chat web**, lo cierras tú. Copias, pegas, pruebas y le cuentas qué falló.
  Tú eres sus manos.
- En el **agente**, el ciclo se cierra solo. Actúa, ve el resultado y corrige. Tú
  dejas de ser sus manos y te vuelves quien lo dirige.

| | Chat web | Agente en la terminal |
|---|---|---|
| Ve tus archivos | Solo lo que pegas | La carpeta donde lo abres |
| Ejecuta cosas | Solo en su propio espacio, no en tu computadora | Sí, con tu permiso |
| Revisa su trabajo | Solo lo que corre en su espacio | Sí: corre, lee el resultado, corrige |
| Tu papel | Copiar y pegar | Pedir y revisar |

## Agente = modelo + herramientas + ciclo

Un agente no es un modelo distinto. Es el mismo modelo con dos cosas más alrededor.

### El modelo solo escribe texto

Un modelo de lenguaje hace una sola cosa: predice la siguiente palabra, una tras otra
(en realidad, pedazos de palabra: tema 2).
No tiene manos: no puede abrir un archivo ni correr nada. Tampoco tiene memoria
propia: no recuerda nada que no venga en la conversación que recibe (sabe lo que
aprendió al entrenarse, pero no lo que pasó antes).

### Herramientas: una lista de lo que puede pedir

Junto con tu mensaje, al modelo se le entrega una lista de herramientas. Cada una
tiene un nombre, qué datos necesita y qué devuelve. Simplificada, se ve así:

```text
leer_archivo(ruta)       → devuelve lo que dice el archivo
ejecutar(comando)        → corre un comando, devuelve el resultado
editar_archivo(ruta, …)  → cambia un archivo
```

El modelo no "tiene" estas herramientas. Solo sabe que existen y que puede pedirlas.
Agregar una herramienta es agregar una línea a esa lista.

### Pedir no es hacer

Cuando el modelo necesita algo, escribe una solicitud en vez de una respuesta:

```text
→ leer_archivo("gastos.csv")
```

Eso sigue siendo solo texto. Quien la ejecuta de verdad es un programa que rodea al
modelo. A ese programa se le llama *harness* (arnés): Claude Code, Codex o Gemini CLI
son harnesses. El programa lee la solicitud, abre el archivo en tu computadora y le
devuelve al modelo lo que encontró.

### El ciclo

1. El programa llama al modelo con tu mensaje y la lista de herramientas.
2. El modelo pide una herramienta.
3. El programa la ejecuta y obtiene el resultado.
4. El programa vuelve a llamar al modelo con **toda la conversación** más el resultado.
5. Se repite hasta que el modelo responde sin pedir nada más.

Ojo con el paso 4: **toda la conversación se reenvía cada vez**. El modelo no recuerda
la llamada anterior; la vuelve a leer completa. En el tema 2 veremos por qué esto
importa.

## Ejemplo: ¿cuánto gasté en octubre?

Tienes un archivo `gastos.csv` (una tabla tipo Excel guardada como texto) y abres el
agente en esa carpeta.

```text
Herramientas: leer_archivo(ruta), ejecutar(comando)

Tú:        ¿Cuánto gasté en octubre?
Modelo:    → leer_archivo("gastos.csv")
Programa:  ← fecha,concepto,monto
             28/09/2026,renta,6000
             03/10/2026,super,850
             …
Modelo:    → ejecutar("sumar monto donde fecha tenga '2026-10'")
Programa:  ← 0
Modelo:    ¿0 en octubre? No puede ser. Las fechas vienen como
           día/mes/año. Corrijo.
           → ejecutar("sumar monto donde fecha tenga '/10/2026'")
Programa:  ← 4320
Modelo:    Gastaste $4,320 en octubre.
```

Esto es una **traza**: lo que el modelo pide (→) y lo que el programa le devuelve (←).

(En la vida real el comando estaría escrito en un lenguaje como Python. Aquí lo
escribimos en español para que se lea fácil.)

Lo que pasó:

- El modelo se llamó **cuatro veces**, y cada vez recibió toda la conversación.
- El primer intento devolvió `0`: buscó fechas como `2026-10`, pero el archivo usa
  `03/10/2026`. No hubo error; el resultado simplemente no tenía sentido.
- Notó que `0` no podía ser, entendió el formato y corrigió. **Sin ti.**

En el chat web, ese `0` lo habrías visto tú, y te habría tocado darte cuenta y
contárselo. Aquí el ciclo lo resolvió solo.

> **Para quien presenta:** lee la traza en voz alta, línea por línea. En cada `→`,
> di "aquí el modelo **pide**"; en cada `←`, di "aquí el programa le **devuelve** el
> resultado real". Detente en el `← 0`: no es un error, es un resultado que no tiene
> sentido. El modelo lo ve y lo cuestiona; ahí el ciclo se gana su lugar.

## ¿De dónde viene la agencia?

Dos cosas alrededor del modelo hacen que se comporte como agente:

- **Herramientas:** puede actuar, no solo hablar.
- **Ciclo:** ve el resultado real de lo que hizo.

Juntas hacen posible la **autonomía**: tú das el objetivo; él decide los pasos, dentro
de los permisos que le das. La autonomía no es una cuarta pieza: la fórmula sigue
siendo modelo + herramientas + ciclo. Es lo que ese ciclo con herramientas permite.

## Un espectro, no un interruptor

La línea entre chat y agente no es tajante. Los chats web ya tienen algunas
herramientas: buscar en internet o correr código en su propio espacio aislado.

Más herramientas, más acceso a tu entorno real y más pasos seguidos sin ti = **más
agente**.

El agente en la terminal está en el extremo porque trabaja sobre **tus archivos**.
Desde la terminal el agente llega a tus archivos y tus programas: la carpeta donde lo
abres se vuelve su lugar de trabajo, y todo lo que hace queda en tu computadora para
que lo revises.

## Permisos

Los permisos existen porque las herramientas **actúan de verdad**: editar, borrar o
instalar cambia tu computadora. El agente te pide permiso antes de hacerlo.

**Lee antes de aceptar.** Si no entiendes qué va a hacer, pregúntale.

## Cómo pedirle las cosas

Esto es lo que vas a practicar. Un buen pedido tiene tres partes:

- **Objetivo:** qué quieres lograr ("una página que muestre mis gastos del mes").
- **Contexto:** lo que el agente no puede adivinar ("los gastos están en `gastos.csv`").
- **Terminado:** cómo sabrás que quedó ("el total que muestra coincide con la suma de
  `gastos.csv`").

El criterio de "terminado" es lo que el agente usa para saber cuándo salir del ciclo.
Por eso tiene que ser algo que él pueda comprobar. Abrirla en el navegador y mirarla es
tu revisión, después.

❌ "Hazme una página"

✅ "Haz una página que muestre mis gastos de `gastos.csv`. Está lista cuando el total
del mes que muestra coincide con la suma de `gastos.csv`."

## Cuándo te sirve

Usa el chat web para preguntas y lluvia de ideas. Usa el agente cuando el resultado
tenga que **existir**: archivos, programas o datos que se queden en tu computadora.
