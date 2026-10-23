---
title: "Práctica: mejorar un flujo con evidencia"
weight: 7
---

**Duración:** 120 min. Puedes trabajar en pareja. Usa tu proyecto si ya tienes una
tarea acotada y entradas disponibles; si no, utiliza el caso de ventas de esta página.

El entregable es **un flujo ejecutable, una mejora y una comparación documentada**.
No necesitas instalar un MCP, construir un framework ni usar todas las técnicas.

## Ruta y alcance · 10 min

| Ruta | Punto de partida | Mejora posible |
|---|---|---|
| Reporte de ventas | Los archivos sintéticos de abajo. | Separar cálculo, validación y explicación. |
| Tu tarea con herramientas | Un flujo existente que consulta o transforma datos. | Mejorar un contrato, la recuperación o un control. |
| Tu proyecto de código | Un repositorio que ya puedes ejecutar. | Añadir criterios comprobables y revisión independiente. |

Escribe: **«Dada esta entrada, quiero este resultado; lo aceptaré cuando pueda
comprobar estas condiciones»**. Define también qué queda fuera. Evita dedicar la
práctica a configurar credenciales o desplegar infraestructura.

En tu propio proyecto prepara entre tres y seis casos: uno normal, uno límite y uno
que deba rechazarse. Si trabajas con ventas, ya tienes seis. Usa datos que puedas
compartir con las herramientas elegidas.

## Archivos del caso de ventas

Todos los datos son inventados. Descarga los archivos en una carpeta nueva:

- [ventas.csv](ventas.csv): base con cancelación, cero y duplicado exacto.
- [ventas-conflicto.csv](ventas-conflicto.csv): un ID con dos importes distintos.
- [ventas-invalido.csv](ventas-invalido.csv): un importe que no es un número válido.
- [ventas-ceros.csv](ventas-ceros.csv): octubre tiene registros válidos de importe cero.
- [reglas.txt](reglas.txt): contrato del reporte y criterios de aceptación.
- [casos.json](casos.json): entradas y expectativas para seis evaluaciones.
- [registro-evaluacion.csv](registro-evaluacion.csv): plantilla sin resultados medidos.

El archivo de casos **describe** qué comprobar; no es un evaluador ejecutable. Tu
implementación debe convertir los criterios numéricos en comprobaciones y conservar
una revisión de la respuesta final cuando corresponda.

## Ejecutar y guardar la versión inicial · 20 min

Guarda una copia o commit local del estado inicial. Registra modelo, configuración,
entradas y comandos. No publiques el repositorio como parte del ejercicio.

Para ventas, puedes empezar con esta solicitud a tu agente de código:

```text
Lee reglas.txt y ventas.csv. Crea una herramienta local en Python 3.10+
usando solo la biblioteca estándar. Debe recibir la ruta de un CSV
y un mes YYYY-MM, y producir un reporte con los campos de reglas.txt.
Documenta el comando para ejecutarla. No modifiques los datos de entrada.
No publiques ni envíes nada. Ejecuta el caso normal y muestra la evidencia.
```

Ejecuta los casos con la versión inicial y guarda las salidas. Si aún no alcanza el
tiempo para los seis, registra cuáles no ejecutaste y reserva tiempo para completar
la comparación. La respuesta «ya funciona» del agente no cuenta como ejecución.

**Dos cosas diferentes:** las pruebas del programa comprueban su comportamiento;
los casos del agente observan también cómo obtiene datos, maneja un error y explica
el resultado. Para el caso causal, pide al agente que explique el cambio a partir
del reporte y conserva esa respuesta. Un script que suma bien no prueba que la
explicación del agente sea fiel.

## Elegir e implementar una mejora · 50 min

Inspecciona el primer fallo observado. Elige **una intervención principal**:

- Contexto: instrucciones breves, referencias y criterio de terminado explícito.
- Herramienta: argumentos, salida y errores con un contrato claro.
- Verificación: cálculo por código y aceptación condicionada a reglas comprobables.
- Revisión: otra sesión o subagente busca fallos con evidencia y sin exigir hallazgos.

Para ventas, una intervención útil es separar el cálculo de la prosa y añadir un
verificador de reglas. Escribe los resultados esperados antes de pedirle al agente
que arregle el código; no obtengas las expectativas de la misma función que pruebas.

Pide un cambio pequeño, inspecciona el diff y ejecuta la comprobación que motivó
el cambio. Luego ejecuta regresiones. Si usas TDD, comprueba que la prueba falla por
la causa prevista antes de corregir y que después pasa sin debilitar el criterio.

Un encargo de revisión acotado:

```text
Revisa reglas.txt y la implementación. Busca discrepancias que produzcan
un reporte incorrecto. No edites archivos. Devuelve para cada hallazgo:
entrada que lo dispara, regla incumplida, evidencia y efecto.
No necesitas encontrar un número mínimo de problemas.
```

Si todo pasó desde el inicio, conserva ese resultado. Puedes medir tiempo,
intervenciones o ampliar los casos; si agregas casos, ejecútalos también sobre la
versión inicial. No fabriques una mejora ni dañes la base para justificar el cambio.

**Extensión opcional:** añade estado para retomar una tarea, o una compuerta local
que copie el reporte a una carpeta de aceptados solo después de validar. Sigue sin
haber una publicación real. No añadas extensiones si falta la comparación básica.

## Comparar las dos versiones · 25 min

Ejecuta los mismos casos sobre ambas versiones y conserva sus salidas. Registra
`aprobado`, `fallido` o `no_ejecutado`, evidencia, tiempo e intervención humana.
La plantilla contiene filas pendientes: **no representan resultados reales**.

En el caso de ventas, verifica estas expectativas:

| Caso | Criterio principal |
|---|---|
| C01 · Base | Septiembre: 1500.00; octubre: 2000.00, 3 ventas completadas únicas; variación: 33.33 %. |
| C02 · Conflicto | Rechazar el archivo e identificar V004; no emitir un total aceptado. |
| C03 · Importe inválido | Rechazar e identificar V004; no sustituir el importe por cero. |
| C04 · Cero válido | Octubre: 0.00, 1 venta completada; variación: −100.00 %. |
| C05 · Mes ausente | Noviembre: `sin_datos`; total y variación nulos. |
| C06 · Explicación causal | Usar las cifras correctas y reconocer que el CSV no permite determinar la causa. |

Para C06, una persona revisa que la respuesta no presente como hechos una campaña,
estacionalidad u otra causa ausente de la fuente. Citar «ventas.csv» no basta para
respaldar esa afirmación. Si presenta hipótesis, deben estar claramente identificadas
y separadas de lo que los datos demuestran.

Anota qué mediste: **programa**, **agente** o ambos. No conviertas seis pruebas del
programa en una afirmación sobre la confiabilidad completa del agente. Si puedes,
repite un caso del agente y observa si cambia. Reporta intentos, no solo el mejor.

## Mostrar y cerrar · 15 min

Cada pareja muestra una entrada, el resultado inicial, el cambio y la evidencia
posterior. Resume lo que sigue sin estar resuelto.

Entrega en tu carpeta de trabajo:

1. Objetivo, límites y criterios de aceptación.
2. Versión inicial y final, con instrucciones para ejecutarlas.
3. Casos, resultados y trazas de ambas versiones.
4. Una conclusión breve: qué mejoró, qué empeoró y qué no pudiste medir.

Si necesitas pausar, deja un estado de reanudación: archivos relevantes, último
resultado comprobado, siguiente paso y bloqueo. «Continuar mañana» no basta para
reconstruir qué quedó pendiente.

## Alternativa sin acceso al agente

Trabaja en pareja con alguien que tenga acceso. Si no es posible, usa las trazas
ilustrativas de los temas para localizar fallos y diseña contratos y casos. Marca
esa entrega como **análisis sin ejecución**; no completes métricas inventadas.

## Guía para facilitar

A los 30 minutos, cada equipo debe tener una base guardada o un bloqueo explícito.
A los 80, congela el alcance y pasa a evaluar. Reserva los últimos 15 para mostrar
evidencia. Si un equipo se atasca en instalación, ofrece el caso local de ventas o
trabajo en pareja. Prioriza terminar una comparación sobre añadir otra integración.
