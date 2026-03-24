# Vector db

- Specialized DB optimized for similarity search over high-dimensional vectors

```
normal db: WHERE id = 42

vector db: find me the 5 vectors most similar to this one (nearest neighbor search)
- Similarity is measured with cosine similarity or dot product
- how close are two vectors in N-dimensional space?
```

## Options

| db       | notes                               |
| -------- | ----------------------------------- |
| pinecone | managed, easy to start              |
| weaviate | open-source, hybrid search          |
| qdrant   | open-source, rust, fast             |
| pgvector | postgres extension -- SQL + vectors |
| chroma   | lightweight, great for local dev    |
| FAISS    | facebook's library, in-memory       |
