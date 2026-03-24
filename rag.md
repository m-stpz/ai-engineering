# RAG (Retrieval-Augmented Generation)

- A design pattern for connecting LLMs to a private or real-time db
- Instead of training a model on your data (slow and expensive), you search for the right information and "adds" it into the prompt before the model answers
- LLMs have a knowledge cutoff and no access to your private data. RAG solves this by fetching relevant context at query time and injecting it into the prompt

```
User query -> Retrieve relevant docs -> Inject it into prompt -> LLM answers
```

## RAG Pipeline

### Ingestion

- offline, runs once or on schedule

```
raw docs -> chunk -> embed -> store in vector db
```

- Chunking: split documents into smallar pieces
- Embedding: convert each chunk into a vector (array of floats) using an embedding model
- Storage: Store `(chunk_text, vector, metadata)` in a vector db

### Retrieval

- online, per query

```
user query -> embed query -> vector similarity search -> Top-K chunks
```

- embed the query with the same model used during ingestion
- search the vector db for the most similar chunk vectors
- return the top-K most relevant chunks

### Generation

```
System prompt + retrieved chunks + user query -> LLM -> answer

prompt = f"""
Answer using only the context below.

Context: {retrieved_chunks}

Question: {user_query}
```
