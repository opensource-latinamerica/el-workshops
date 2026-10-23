# De instrucciones a controles

¿Quién decide que la comprobación ocurra?

Avanzado · 5 de 6 · 20 min

---

## La misma regla, cuatro mecanismos

1. «Comprueba antes de publicar».
2. Script disponible para comprobar.
3. Comprobación obligatoria en el flujo.
4. Publicación que valida internamente.

¿Dónde sigue dependiendo del modelo?

---

## Hook

Integración en un evento del ciclo.

Antes de una operación · después de editar · al terminar.

Ejecutar, observar y bloquear son capacidades distintas.

---

## Juicio y ejecución

Un hook puede ejecutar código o consultar un modelo.

Ejecución obligatoria no significa juicio infalible.

Revisa errores, timeout y rutas alternativas.

---

## Una compuerta

Traza ilustrativa:

```text
Fuente:  2000.00 MXN
Reporte: 2400.00 MXN
→ Rechazar: incluye una cancelación.
→ Corregir y volver a comprobar.
```

El verificador necesita una referencia confiable.

---

## Válido no implica correcto

```json
{"estado":"ok","total_mxn":"2400.00"}
```

Forma válida, cifra incorrecta para nuestro caso.

Schema · reglas del dominio · resultado final.

---

## Reintentar sin duplicar

Un timeout no demuestra que la acción no ocurrió.

Identificador de operación + consulta de estado.

Idempotencia: repetir la solicitud no duplica el efecto.

---

## ¿Existe otra ruta?

Si puede publicar por un comando sin validar,
la compuerta no cubre toda la operación.

La garantía depende del entorno y de las propiedades verificadas.
