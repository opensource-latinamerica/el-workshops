---
title: "5. De instrucciones a controles"
weight: 5
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

**Duración:** 20 min. **Al terminar:** puedes señalar quién obliga a ejecutar una
comprobación y qué rutas podrían evitarla.

## ¿Quién decide comprobar? · 4 min

Parte de una regla: **«Antes de publicar el reporte, los totales deben cuadrar».**

| Implementación | Quién decide si se comprueba | Qué aporta |
|---|---|---|
| Escribir la regla en el prompt o skill | El modelo debe seguirla. | Orientación. |
| Añadir un script verificador | Si su invocación es opcional, el modelo puede omitirlo. | Un resultado comprobable cuando se ejecuta. |
| Ejecutarlo obligatoriamente en un hook o proceso de aceptación | El código del proceso. | La comprobación deja de depender de una solicitud del modelo. |
| Validar dentro de la única operación autorizada de publicación | La operación y los permisos del entorno. | La publicación requiere pasar esa validación. |

Un resultado determinista del script no hace determinista la decisión de ejecutarlo.
Esta es una escala didáctica de controles, no una clasificación oficial de productos.

Tampoco garantiza corrección universal: cada control verifica propiedades concretas
y depende de su implementación y del entorno. Si el agente puede modificar el
verificador o publicar por otra vía, la garantía cambia.

## Hooks · 4 min

Un **hook** es una integración en un evento del ciclo: por ejemplo, antes de una
herramienta, después de una edición o al intentar terminar. La configuración del
harness determina cuándo corre y qué efectos puede tener.

Ejemplos de usos:

- Tras editar: formatear o ejecutar una comprobación acotada.
- Antes de una operación: revisar entradas y permisos.
- Al aceptar el resultado: verificar los criterios de terminado.

**Ejecutar, observar y bloquear son capacidades distintas.** Un hook que solo registra
un evento no impide una acción. Un hook posterior no deshace por sí mismo una escritura.
Comprueba el comportamiento ante errores, timeout y desactivación.

Si un hook consulta a un modelo para emitir un juicio, su ejecución puede ser
obligatoria, pero el juicio sigue siendo probabilístico. Para una regla comprobable,
prefiere una comprobación por código.

> **Para quien presenta:** muestra la documentación del harness que usarás y un
> único evento que hayas ensayado. No copies el mismo archivo de configuración a
> productos diferentes. Sin demo preparada, sigue la traza de la siguiente sección.

## Una compuerta en el flujo · 4 min

Traza ilustrativa, sin operación real de publicación:

```text
Modelo solicita publicar el reporte.
Código calcula el total desde la fuente: 2000.00.
Código lee el total del reporte: 2400.00.
Código rechaza: el reporte incluye una venta cancelada.
Modelo propone corregirlo.
El flujo vuelve a comprobar antes de aceptar el resultado.
```

El rechazo comprueba una regla; no garantiza que el modelo consiga arreglar el
problema. Limita los intentos y registra la causa si no se resuelve.

Para que toda publicación pase por la compuerta, no puede existir otra herramienta
o comando accesible que publique sin validar. El alcance efectivo incluye todas
las herramientas y credenciales disponibles.

## Structured outputs · 4 min

Una salida estructurada facilita que otro programa procese el resultado. Un schema
define campos, tipos y restricciones admitidas. Hay que comprobar qué garantiza la
API o validador y manejar fallos o respuestas incompletas.

Ejemplo de resultado, no de schema:

```json
{
  "estado": "ok",
  "mes": "2026-10",
  "total_mxn": "2400.00",
  "fuente": "ventas.csv"
}
```

Tiene forma razonable, pero el total es incorrecto para nuestro caso. Validar la
estructura no demuestra que la cifra coincida con la fuente, que la herramienta
elegida sea adecuada ni que la tarea esté terminada.

Separa **validación estructural**, **reglas del dominio** y **resultado de la tarea**.
Un campo `"aprobado": true` escrito por el modelo tampoco sustituye una aprobación
registrada por el mecanismo autorizado.

## Reintentos y efectos · 2 min

Una operación **idempotente** evita duplicar el efecto cuando se repite la misma
solicitud. Si registrar un reporte se reintenta tras un timeout, usa un identificador
de operación y comprueba si ya se registró. Un timeout no demuestra que no ocurrió.

No todas las operaciones son idempotentes. El sistema debe decidir qué puede
reintentarse, cuántas veces y cuándo consultar el estado o pedir intervención.

## Comprobación · 2 min

Pregunta: **«La skill exige ejecutar el verificador. El verificador funciona.
¿Puede salir un reporte sin verificar?»** Sí, si la invocación sigue siendo opcional.

Pregunta de extensión: **«¿Y si existe otra vía de publicación?»** Hay que revisar
esa vía: la garantía depende de cubrir todas las rutas autorizadas.

**Transición:** podemos describir los controles. Falta observar qué diferencia
producen cuando ejecutamos el sistema con casos reales.

Fuentes: [referencia de hooks de Claude Code](https://code.claude.com/docs/en/hooks),
[Dante Bazaldúa, p. 26](https://stdout.mx/claude4aieng/datos-mcp-ibero.pdf)
y [CMU, Tool Use, pp. 28–30](https://www.cmu-agents.com/slides/lecture-02-tool-use.pdf).
