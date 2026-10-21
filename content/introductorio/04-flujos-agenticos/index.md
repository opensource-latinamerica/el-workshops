---
title: "4. Flujos agénticos y superpowers"
weight: 4
outputs: [html, slides]
---

[Abrir la presentación](slides.html)

## El error más común

Pedirle al agente "hazme una app de X" y dejarlo correr. El agente adivina lo que
quieres, construye mucho y rápido, y al final no es lo que tenías en mente.

La solución no es un mejor pedido: es un mejor **flujo**.

## Plugins

Un plugin es un paquete de skills (y a veces tools o MCPs) que alguien ya armó.
Lo instalas una vez y tu agente aprende un flujo de trabajo completo.

[Superpowers](https://github.com/obra/superpowers) es un plugin que le enseña al agente
a trabajar como un buen equipo de desarrollo: preguntar antes de construir, planear,
probar y revisar.

## Spec-driven development

Primero se acuerda **qué** y **por qué**; después el **cómo**.

- **Spec** (especificación): un documento corto que dice qué se va a construir, para
  quién y qué queda fuera.
- **Plan:** los pasos concretos para construir el spec.

Con el spec escrito, tú y el agente tienen la misma idea antes de que exista una sola
línea de código.

## El flujo de superpowers

1. **Brainstorming:** el agente te hace preguntas, una a la vez, hasta entender lo que
   quieres. Tú describes, él escucha.
2. **Spec:** escribe lo acordado. Tú lo lees y lo apruebas o corriges.
3. **Plan:** divide el trabajo en pasos pequeños y verificables.
4. **Ejecución:** construye paso por paso (a veces con varios subagentes).
5. **Revisión:** revisa su propio trabajo antes de decir "terminé".
6. **Cierre:** commit, push y pull request.

Tu papel cambia en cada paso: en 1 y 2 **decides**; en 3 a 5 **supervisas**; en 6
**apruebas**.

## Por qué funciona

- El agente pregunta en lugar de adivinar.
- Los errores se corrigen en el spec, donde cuestan poco, no en el código.
- Cada paso deja algo revisable.

## Mapa del flujo

Tu guía para las 2 horas de práctica.

| Paso | Qué haces tú | Qué le dices al agente |
|---|---|---|
| 0. Preparar | Carpeta nueva, repo de Git, `AGENTS.md` corto | "Inicia un repo de Git aquí y crea un `AGENTS.md` con…" |
| 1. Idea | Describe tu problema real, no la solución | "Quiero hacer brainstorming sobre…" |
| 2. Spec | Lee el spec completo; corrige lo que no sea tuyo | "Esto no es lo que quiero: …" |
| 3. Plan | Revisa que los pasos sean pequeños | "Escribe el plan." |
| 4. Ejecución | Acepta permisos leyendo; observa | "Ejecuta el plan." |
| 5. Revisión | Prueba tú mismo el resultado | "Muéstrame cómo probarlo." |
| 6. Guardar | Revisa el cambio y súbelo | "Haz commit y súbelo a mi GitHub." |

### Si te atoras

- **El agente se confunde o se repite:** inicia una sesión nueva. El spec y el plan
  están guardados en archivos, así que no pierdes nada.
- **Rompió algo:** "Regresa al último commit."
- **No entiendes qué hizo:** "Explícame en lenguaje sencillo qué cambiaste y por qué."
- **El proyecto creció demasiado:** "Ayúdame a recortar esto a lo mínimo que funcione."
