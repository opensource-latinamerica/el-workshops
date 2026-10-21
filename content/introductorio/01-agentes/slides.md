# ¿Qué es un agente?

Curso introductorio · Tema 1

---

## El mismo modelo, dos resultados

En la web: te da código y tú ves si funciona.

En la terminal: lo escribe, lo prueba y lo arregla.

**¿Por qué, si es el mismo modelo?**

---

## ¿Quién cierra el ciclo?

- **Chat web:** tú. Copias → pegas → pruebas → "salió este error" → repites
- **Agente:** se cierra solo. Actúa → ve el resultado → corrige

---

## Chat vs agente

| | Chat web | Agente en la terminal |
|---|---|---|
| Ve tus archivos | Solo lo que pegas | La carpeta donde lo abres |
| Ejecuta cosas | Solo en su propio espacio, no en tu computadora | Sí, con tu permiso |
| Revisa su trabajo | Solo lo que corre en su espacio | Sí |
| Tu papel | Copiar y pegar | Pedir y revisar |

---

## Agente = modelo + herramientas + ciclo

---

## El modelo solo escribe texto

- Predice la siguiente palabra
- No tiene manos
- No recuerda nada que no venga en la conversación

---

## Herramientas: una lista

Al modelo se le entrega una lista de lo que puede **pedir**:

```text
leer_archivo(ruta)       → devuelve lo que dice el archivo
ejecutar(comando)        → corre un comando, devuelve el resultado
editar_archivo(ruta, …)  → cambia un archivo
```

---

## Pedir no es hacer

El modelo escribe una solicitud:

```text
→ leer_archivo("gastos.csv")
```

Un programa alrededor del modelo (el *harness*) la **ejecuta de verdad** y le devuelve el resultado.

---

## El ciclo

1. El programa llama al modelo
2. El modelo pide una herramienta
3. El programa la ejecuta
4. Vuelve a llamar al modelo con **toda la conversación** + el resultado
5. Repite hasta que el modelo responde sin pedir nada

---

## Ejemplo: tus gastos (1/2)

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
```

Esto es una **traza**: lo que el modelo pide (→) y lo que el programa le devuelve (←).

---

## Ejemplo: tus gastos (2/2)

```text
Modelo:    ¿0 en octubre? No puede ser. Las fechas vienen como
           día/mes/año. Corrijo.
           → ejecutar("sumar monto donde fecha tenga '/10/2026'")
Programa:  ← 4320
Modelo:    Gastaste $4,320 en octubre.
```

---

## Lo que acaba de pasar

- El modelo se llamó **cuatro veces**
- Cada vez recibió **toda la conversación**
- Vio que `0` no tenía sentido y corrigió **sin ti**

---

## ¿De dónde viene la agencia?

- **Herramientas:** puede actuar
- **Ciclo:** ve el resultado real

Juntas hacen posible la **autonomía**: tú das el objetivo, él decide los pasos (dentro de tus permisos).

No es una cuarta pieza: sigue siendo modelo + herramientas + ciclo.

---

## Un espectro, no un interruptor

- El chat web ya tiene algunas herramientas: buscar en internet, correr código en su propio espacio
- Más herramientas + más acceso a tu entorno + más pasos sin ti = **más agente**
- El agente en la terminal está en el extremo: trabaja sobre **tus archivos**

---

## Permisos

Existen porque las herramientas **actúan de verdad**.

**Lee antes de aceptar.** Si no entiendes, pregúntale.

---

## Cómo pedir

1. **Objetivo:** qué quieres lograr
2. **Contexto:** lo que no puede adivinar
3. **Terminado:** cómo sabrás que quedó (algo que el agente pueda comprobar)

---

## Ejemplo

❌ "Hazme una página"

✅ "Haz una página que muestre mis gastos de `gastos.csv`. Está lista cuando el total del mes que muestra coincide con la suma de `gastos.csv`."

Abrirla en el navegador es **tu** revisión.

---

## Cuándo te sirve

- **Chat web:** preguntas, lluvia de ideas
- **Agente:** cuando el resultado tiene que *existir*
