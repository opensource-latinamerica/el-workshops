---
title: "4. Coding agents: del pedido al cambio comprobado"
weight: 4
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

**Duración:** 25 min. **Al terminar:** puedes especificar un cambio, pedir pruebas
útiles y revisar evidencia antes de aceptarlo.

## Una spec pequeña · 5 min

*Spec-driven development* significa acordar el comportamiento esperado antes de
implementar. La spec puede ser breve: problema, entradas, resultado, restricciones,
fuera de alcance y aceptación. Un plugin puede ordenar el procedimiento, pero no
sustituye revisar lo que acordaste.

Ejemplo con el [caso de práctica](../07-practica/#archivos-del-caso-de-ventas):

```text
Problema: comparar ventas sin contar cancelaciones ni duplicados.
Entrada: CSV con id, fecha, estado e importe_mxn.
Salida: totales mensuales en MXN y variación porcentual.
Reglas: completadas; copia exacta = una venta; conflicto = detener.
Aceptación: septiembre 1500.00; octubre 2000.00; variación 33.33%.
Límites: no inventar causas; no publicar; no modificar el CSV.
Fuera de alcance: pronósticos, dashboards y conectar el sistema real.
```

Estos importes corresponden a los datos sintéticos del caso normal. No son resultados
de una ejecución del agente. La variación se redondea a dos decimales al presentar.

## Localizar → editar → verificar · 4 min

Antes de editar, el agente debe encontrar dónde vive el comportamiento y reproducir
el problema. Pide un cambio pequeño en una rama o copia de trabajo apropiada y revisa
el diff. Guarda un estado inicial al que puedas comparar; no hace falta un tutorial
completo de Git durante esta sesión.

Un cambio puede arreglar el caso solicitado y romper otro. Separa:

- **Fallaba → pasa:** la prueba que demuestra la reparación.
- **Pasaba → sigue pasando:** las pruebas de regresión.

## TDD con una regla concreta · 6 min

TDD: escribir una prueba del comportamiento, verla fallar por la razón esperada,
implementar y volver a comprobar. Después puedes mejorar la estructura conservando
el comportamiento.

Ejemplo ilustrativo de un error:

```python
# Antes: 0 se sustituye por el valor por defecto.
importe = valor or importe_por_defecto

# Después: solo None se sustituye.
importe = importe_por_defecto if valor is None else valor
```

Antes del arreglo, una prueba con `valor = 0` debe fallar. Después tiene que pasar;
también deben seguir pasando los casos de un importe positivo y de `None`, si el
contrato permite ese último caso. En nuestro CSV, un importe faltante se rechaza:
no se rellena con un valor por defecto.

> **Para quien presenta:** este fragmento enseña una regla de Python; no es el
> programa del reporte. Si haces una demo en vivo, prepara un archivo pequeño con
> esas tres pruebas y muestra el fallo real antes del cambio. Si usas la slide,
> pide al grupo predecir qué ocurre con cero.

## Qué probar · 4 min

| Capa | Ejemplo | Qué no demuestra |
|---|---|---|
| Unidad | Deduplicar una copia exacta sin perder una venta distinta. | Que todos los pasos estén conectados. |
| Integración | Leer el CSV, validar y calcular con las reglas. | Que el reporte final explique bien el dato. |
| Extremo a extremo | Ejecutar el flujo y revisar el archivo generado. | Que funcione para cualquier entrada. |
| Interfaz, si existe | Interactuar y comprobar estado; inspeccionar el render. | Una captura bonita no prueba los cálculos. |

Si el agente interpreta mal la spec, puede escribir código y pruebas que compartan
el mismo error. Los ejemplos esperados y las reglas del dominio deben tener una
referencia independiente. No aceptes cambiar un resultado esperado solo para poner
las pruebas en verde: revisa si cambió legítimamente el requisito.

## Review adversarial con evidencia · 4 min

«Adversarial» aquí significa intentar refutar que el cambio cumple sus requisitos.
El objetivo es encontrar fallos reales, no llenar una lista de objeciones.

```text
Revisa este diff contra la spec y los casos de aceptación.
No edites. Prioriza errores de comportamiento y regresiones.
Para cada hallazgo: archivo, condición que lo activa, efecto y
prueba o pasos para reproducirlo. Si no lo pudiste verificar,
márcalo como hipótesis. Puedes concluir que no encontraste fallos.
```

Usar otro modelo es una opción, si tienes acceso. Aun así, reproduce el hallazgo
antes de corregirlo. Una revisión con contexto separado ayuda a reducir anclaje,
pero sigue necesitando evidencia y puede producir falsos positivos.

## Comprobación · 2 min

Pregunta: **«El reviewer dice que hay un bug y propone cambiar la fórmula.
¿Lo aplicamos?»** Respuesta: primero comparar la fórmula con la regla acordada y
reproducir el fallo. Ni el implementador ni el reviewer son la referencia final.

**Transición:** hemos pedido verificar. Ahora haremos que ciertas comprobaciones
formen parte obligatoria del proceso.

Fuentes: [CMU, Coding Agents, pp. 23–24, 33–36, 47 y 56–59](https://www.cmu-agents.com/slides/lecture-06-coding-agents.pdf)
y [Superpowers](https://github.com/obra/superpowers), como ejemplo de un flujo empaquetado.
