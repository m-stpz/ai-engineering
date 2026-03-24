# AI Engineering

Video: https://www.youtube.com/watch?v=JV3pL1_mn2M

- Building applications on top of foundation models
- Turning experimental AI models into reliable, scalable, and functional products
- Data scientists focus on: "What does this data mean?"
- AI enginers focus on: "How doe we make this AI work for millions of users without it breaking?"
- Bridge between AI Research & Software Engineer
  - Historically, to use AI, you had to be a PhD. However, today, it's about using APIs and frameworks to integrate pre-trained intelligence into software

## Core pillars

- Data engineering: building the "pipes" that feed clean data into the
- Model integration: using APIs or self-hosted models to add "brains" to an application
- MLOps & LLMOps: Managing the lifcycle of a model
  - deploying it
  - monitoring its "drift" (accuracy loss)
  - updating it
- Context engineering: designing the environment (memory, tools, retrieved data) that an AI needs to answer queries correctly

## What does it teach?

- How you can be a software engineer with AI superpowers

| Category      | Key concepts & skills                                                                                       |
| ------------- | ----------------------------------------------------------------------------------------------------------- |
| Programming   | Python (industry standard), SQL for dbs, and TS for building AI-powered interfaces                          |
| Foundations   | Linear algebra (how data is structure), Probability (how AI makes guesses), Calculus (how models learn)     |
| Generative AI | RAG (Retrival-Augmented Generation), Prompt Engineering, and Fine-tuning existing models for specific tasks |
| Architecture  | Building AI agents that can use tools (searching/writing code) to solve multi-step problems                 |
| Deployment    | Docker, Cloud platforms (AWS/Azure/GCP), and building high-speed APIs using FastAPI                         |

## Foundation model

- It's the "swiss army knife" of AI
- Previously, if you wanted an AI that did x, you train it on x
  - if you wanted to translate French, you'd build a translation model
- Foundation model changes that, it's a single, massive system trained on vast amount of data that can be adapted to a wide range of downstream tasks

### Pre-training phase

- They're trained using self-supervised learning
- They ingest nearly the entire public internet: books, articles, code, and scientific papers
- These models have billions or trillions of parameters, which are essentially the "synapses" that store information

### Emerging capabilities

- One of the most fascinating things about foundation models is that they develop "emergent" abilities, skills they weren't programmed to have
- They are:
  - reasoning: they can follow a chain of logic to solve a math word problem
  - coding: by seeing millions of lines of python, they learn how to write functional code
  - multimodality: they "understand" images, audio, and video simultaneously
