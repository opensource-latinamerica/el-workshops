---
title: "RAG, búsqueda híbrida y reranking"
weight: 1
outputs: [html, slides]
aliases: ["/avanzado/01-rag/"]
---

[Abrir la presentación](slides.html)

Material opcional. Antes de añadir un índice, identifica una pregunta que tu búsqueda
actual no resuelva y guarda la evidencia que debería recuperar.

## Elegir cómo recuperar

| Necesidad | Punto de partida |
|---|---|
| Identificador, ruta o mensaje de error exactos | Búsqueda por texto, por ejemplo `rg`. |
| Importes, fechas o agregaciones de una tabla | Consultas y cálculos con código. |
| Conceptos expresados con palabras distintas | Evaluar búsqueda semántica. |
| Mezcla de identificadores y lenguaje natural | Evaluar búsqueda híbrida. |

RAG significa generar usando información recuperada. Puede usar búsqueda textual,
semántica o ambas; no exige una base vectorial. Una CLI puede consultar cualquiera
de esos mecanismos.

## RRF y reranking

**RRF** combina listas ordenadas usando la posición de cada resultado. Sirve, por
ejemplo, para unir candidatos de búsqueda textual y semántica sin tratar sus scores
como si midieran lo mismo. Su score no es una probabilidad de que la respuesta sea cierta.

Un **reranker** vuelve a valorar los candidatos respecto de la consulta. No puede
recuperar un documento que nunca entró en el conjunto de candidatos. Añade costo y
latencia: compara si mejora las preguntas que importan.

## Ejercicio de extensión

Elige diez preguntas sobre tus documentos y anota las fuentes esperadas. Compara
búsqueda textual y una alternativa manteniendo fijo el presupuesto de contexto y
el modelo que responde. Separa dos resultados: si recuperaste evidencia suficiente
y si la respuesta la utilizó correctamente. Incluye una pregunta sin respuesta en
las fuentes y otra sobre información desactualizada.

Fuentes: [RRF, Elastic](https://www.elastic.co/docs/reference/elasticsearch/rest-apis/reciprocal-rank-fusion)
y [ranking y reranking](https://www.elastic.co/docs/solutions/search/ranking).
