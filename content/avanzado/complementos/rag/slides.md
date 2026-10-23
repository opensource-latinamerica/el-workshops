# Retrieval-Augmented Generation

Curso avanzado · Complemento opcional

---

## Agenda

1. Una pregunta y su evidencia esperada
2. Búsqueda textual, semántica o híbrida
3. Evaluar recuperación y respuesta por separado

---

## Código

```python
docs = buscar(pregunta, k=5)
respuesta = llm(pregunta, contexto=docs)
```

---

## RRF y reranking

RRF combina posiciones de varias listas.

Un reranker reordena los candidatos recuperados.

Compara calidad, costo y tiempo con tu búsqueda inicial.
