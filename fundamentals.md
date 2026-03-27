# Fundamentals

video: https://www.youtube.com/watch?v=ZaPbP9DwBOE

## How LLMS work

- They are transformer models, which are trained on absurd amount of data
- A token is around 3/4 of an English word
  - Simple words = 1 token (cat, run)
  - Longer words = multiple tokens (unbelievable ~ 3 tokens)
  - Estimate = 1 token == 4 char
  - Average: 1 token ~ 0.75 words

### Context window

- Nano, mini: around 2-4k tokens (1,5k - 3k words)
- GPT 4.1, Gemini 2.5 pro: 1M tokens (750k words / 50k lines of code)

## Embedding

- Embeddings transform the way we think about information
- We convert meaning into numbers, instead of storing them in texts, words
- They capture semantic similarity
- An embedding model, takes a text and converts it into a number [usually 1536 digits/dimensions]
  - Similar concepts = similar number patterns

## LangChain

- Abstraction layer to build AI agents with minimal code

- Important distinction: LLM vs Agent
  - LLM: static brain (e.g, gpt, claude, gemini)
  - Agent: a "dynamic" entity, it can use tools, memory and has "autonomy"
    - it's self-determining, differently from a normal software that uses if conditions

- For more in depth, check langchain.md

## Prompt engineering

- Quality of prompt impacts quality of response
- More specific == better

### Prompting techniques

- Zero-shot: direct commands without examples
  - AI relies exclusively on pre-trained knowledge and instructions
- One-shot: learning from a single example
  - AI learns format, style, and structure from a single example
- Few-shot: multiple examples for consistency
- Chain-of-thought: step-by-step reasoning

## Vector dbs

- Stores by meaning, not by value
- Ex: pinecone, chromadb
- They store the embedding (vectors)

### Embedding

- What allows us to go from value to meaning
- GPS for meanings
- Texts gets converter into numbers (coordinates)
- Computer can now measure "distance" between meanings

```
value -> embedding -> meaning

1. document -> embedding -> store in db
2. Query -> embedding -> find similar
3. return top K results (by cosine similarity)

Example:
Query: "remote work policy" [0.2, 0.8, ...]
   |
   v
Finds: "work from home guidelines" [0.21, 0.79,...] (98% similarity)
```

- holiday & vacation are stored close to each other, since they share a similar meaning
- embeddings allow computers to understand meaning

> I can't log in and authentication failed => now, even though they don't share any single word, the computer understands that they are talking about the same thing

### Dimensionality

- It's the standard practice to use 1536 dimensions currently

### Retrieval

- Compose by scoring and chunk overlap
- Scoring: threshold of how similar the results need to be to considered a match
- Chunk overlap: since we take "chunks" of information, in-between content might get cut off
  - Then, we provide some chunk overlap so that context spills over
  - Large docs must be split into smaller pieces for embedding

```
Docume: 123abcdef6789
chunk1: 123
chunk2:  23abcd
chunk3:      cdef6
chunk4:        ef6789

through the overlaps, we ensure context preserval
```

- Optimal settings:
  - chunk size: 500 characters (balanced)
  - overlap: 100 characters (20%)
  - result: 40% better retrieval accuracy

## RAG: Retrieval-Augmented Generation

- RAG uses a vector db as its retrieval engine
- RAG is the technique/pattern
- Vector db is the storage that allows it to work
- Retrieval: allows the search to work
  - The meaning is stored as embedding, the search is also converted to embedding and they are matched
- Augmentation: the retrieve data is injected into the prompt at runtime
  - It "augments" the prompt with retrieved data
- Generation: takes the retrieved text chunks (original words, not the vectors) + prompt + LLM to provide an answer
  - retrieved chunk text + prompt + LLM = result (generation)
  - vectors are only used during retrieval. LLM sees plain text
