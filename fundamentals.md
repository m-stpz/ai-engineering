# Fundamentals

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
