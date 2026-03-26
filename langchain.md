# Langchain

- Plumbing for AI apps, it standardizes the interfaces between all moving parts
- It simplifies the creation/management of:
  - API for interacting with LLMs
  - Memory
  - Vector dbs
  - Tool routing
  - State management
  - Embedding pipeline
  - Semantic search

## LangChain vs Vercel SDK

- Both are abstraction layers over LLM, but they target different ecosystems

| Feature      | Langchain                             | Vercel AI SDK               |
| ------------ | ------------------------------------- | --------------------------- |
| language     | Python (primary)/JS                   | TS/JS only                  |
| target       | backend, data pipelines, agents       | frontend/fullstack web apps |
| streaming UI | not the focus                         | first-class                 |
| RAG tooling  | mature                                | basic                       |
| agents       | LangGraph (powerful)                  | basic tool calling          |
| complexity   | higher                                | lower                       |
| best for     | complex AI pipelines, Python backends | AI-powered web UIs          |

## Concepts

### Components and chains

- Components: modular building blocks
  - LLM wrapper, prompt template, or a db connector
- Chains: glue that "connects" the components together in a specific order (LangChain Expression Language - LCEL)

### Prompts template

- Instead of hardcoding strings, use templates
- Define the structure of the prompt and inject variables dynamically

### Memory

- LLMs don't remember previous interactions
- Memory allows components to store and retrieve past turns of a conversation
- It provides "context"

### RAG (Retrieval augmented generation)

- Process of giving the LLM access to external data (PDFs, websites, databases) that it wasn't originally trained on
- Document loaders
  - fetch data
  - vector stores: dbs that store data as "embeddings" (mathematical representations of meaning)

### Agents

- A chain follows a hardcoded path, an Agent uses the LLM as a "reasoning engine" to decide which tools to use to reach a goal

## Example | RAG-based assistant

```py
import os
from langchain_openai import OpenAIEmbeddings, ChatOpenAI
from langchain_community.vectorstores import DocArrayInMemorySearch
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import RunnableParallel, RunnablePassthrough

# 1. Setup Environment
os.environ["OPENAI_API_KEY"] = "your-key-here"
model = ChatOpenAI(model="gpt-4")

# 2. The Data (RAG Concept)
# In a real app, use PyPDFLoader or WebBaseLoader
vectorstore = DocArrayInMemorySearch.from_texts(
    ["LangChain was created by Harrison Chase in 2022.",
     "The sky is blue because of Rayleigh scattering."],
    embedding=OpenAIEmbeddings()
)
retriever = vectorstore.as_retriever()

# 3. Prompt Template
template = """Answer the question based only on the following context:
{context}

Question: {question}
"""
prompt = ChatPromptTemplate.from_template(template)
output_parser = StrOutputParser()

# 4. The Chain (LCEL - LangChain Expression Language)
# This pipes the components together: Context -> Prompt -> Model -> String Output
setup_and_retrieval = RunnableParallel(
    {"context": retriever, "question": RunnablePassthrough()}
)
chain = setup_and_retrieval | prompt | model | output_parser

# 5. Execution
response = chain.invoke("Who created LangChain and when?")
print(response)
```
