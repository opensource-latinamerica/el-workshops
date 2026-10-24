---
title: "Antes de la sesión: requisitos"
weight: 0
---

## Lo mínimo para trabajar

- Laptop con permiso para crear archivos y ejecutar herramientas de desarrollo.
- Un agente que pueda trabajar en una carpeta, con sesión iniciada y acceso disponible.
- Un editor y una terminal que ya sepas abrir.
- Git para guardar el estado inicial y revisar los cambios. GitHub es opcional para compartir.
- Un proyecto pequeño o el [caso de ventas del taller](../07-practica/#archivos-del-caso-de-ventas).

No necesitas haber tomado el introductorio. Tampoco necesitas tener instalado un
framework de agentes, una base vectorial o todos los MCP que aparecen en ejemplos.

## Comprobación antes de llegar

En una carpeta de prueba, pide a tu agente:

```text
Lista los archivos de esta carpeta. Crea un archivo de texto que diga
"entorno listo" y vuelve a leerlo. Indica qué herramienta usaste.
```

Comprueba tú que el archivo existe. Ejecuta `git --version`. Si usarás el caso de
ventas, comprueba `python3 --version` (o `python --version` en tu entorno): basta
Python 3.10 o posterior y su biblioteca estándar.

Llega con una tarea que puedas expresar en una frase y un ejemplo de resultado
correcto. Si no tienes proyecto, usaremos los datos sintéticos incluidos.

## Acceso a modelos y demos

Trabajar con tu agente habitual consume el acceso de ese producto. Las demos
externas que llaman a una API pueden requerir una llave y saldo **adicionales**:
no asumas que tu suscripción cubre esas llamadas.

El recorrido principal no requiere que todos ejecuten las demos externas. Quien
presenta puede mostrarlas; los participantes practican con su agente y archivos.
No compartas llaves. Usa datos de ejemplo para poder enseñar y comparar resultados.

## Si tu equipo o acceso falla

Trabaja en pareja: una persona opera y la otra revisa los criterios y registra los
resultados. Sin modelo, puedes revisar una traza y calcular los resultados esperados
del caso de ventas; eso practica verificación, pero **no mide el comportamiento de
un agente**. Anota qué parte quedó sin ejecutar.
