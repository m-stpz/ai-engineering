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

## Embeeding

- Converts text into a dense vector (e.g. 1536 floats)

```
"the cat sat on the mat" -> [0.02, -0.14, 0.87,..] # 1536
"a feline rested on a rug" -> [0.03, -0.12, 0.85, ...] # very similar
"stock market crashed" -> [-0.54, 0.91, -0.23,...] # very different
```

- Semantically similar text -> geometrically close vectors

### Common embedding models

```
text-embedding-3-small (openai): cheap, good
text-embedding-3-large (openai): better, pricier
nomic-embed-text: good open-source option
```

## Chunking strategy

- Where most RAG quality issues come from

```
Document → [chunk1][chunk2][chunk3]...
              ↑overlap↑
```

- Too large: noisy context, wastes tokens
- Too small: loses context, fragments meaning
- Overlap: 10-20% overlap prevents cutting mid-sentence

### Strategies

- Fixed-size (naive, often fine)
- Recursive character splitting (LangChain default)
- Semantic chunking (split on meaning shifts)
- Document-aware (split on headers, paragraphs)

## Retrieval strategies

- Dense retrieval (standard): vector similarity, good for semantic search
- Sparse retrieval (BM25/keywor): classic keyword matching, good for exact terms, product IDs, names
- Hybrid search: combine both. Most production systems do this
- Reranking: after fetching top-20 chunks, use a cross-encoder model to re-score and pick top-5. Improves quality

```
query -> vector search (top-20) -> reranker -> top-5 -> LLM
```
