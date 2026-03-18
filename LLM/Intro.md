
# Intro to LLM

My class notes on large language models.

## Table of Contents
- [1. What is a Large Language Model?](#1-what-is-a-large-language-model)
- [2. LLMs vs Earlier NLP Models](#2-llms-vs-earlier-nlp-models)
- [3. What Makes LLMs Powerful?](#3-what-makes-llms-powerful)
- [4. Learning in Multiple Dimensions](#4-learning-in-multiple-dimensions)
- [Key Takeaways](#key-takeaways)
- [Glossary](#glossary)

---

## 1. What is a Large Language Model?

A **Large Language Model (LLM)** is a neural network designed to understand, generate, and respond to human language.

### Main idea
- Built using deep neural networks
- Trained on massive amounts of text data
- Learns patterns, structure, and relationships in language
- Can generate human-like text

### In simple words
An LLM predicts what text should come next based on the text it has already seen.

### Notes
- LLMs do not “understand” language like humans do
- They learn statistical patterns from huge datasets
- Scale matters: more data, more parameters, more compute

---

## 2. LLMs vs Earlier NLP Models

Earlier NLP models were usually built for narrow tasks.

### Earlier NLP models
- Sentiment analysis
- Spam detection
- Named entity recognition
- Translation for limited setups

### LLMs
- One model can do many language tasks
- Better generalization
- Better few-shot and zero-shot performance
- More flexible than traditional NLP pipelines

### Difference
Traditional NLP:
- Often task-specific
- Heavy feature engineering
- Limited adaptability

LLMs:
- General-purpose
- Learn representations automatically
- Can be prompted for many tasks

---

## 3. What Makes LLMs Powerful?

A major reason is the **Transformer architecture**.

### Why transformers matter
- Handle long-range dependencies better
- Process context more effectively
- Scale well with data and compute

### Important points
- Self-attention helps the model focus on relevant words
- Transformers capture relationships across the input
- This architecture enabled modern LLM progress

### Practical meaning
This is why LLMs can summarize, answer questions, translate, reason over text, and generate coherent responses.

---

## 4. Learning in Multiple Dimensions

Language is represented mathematically as vectors and embeddings.

### Core idea
Words and tokens are mapped into high-dimensional space.

### Why this matters
- Similar words are placed closer together
- Relationships can be captured numerically
- Meaning is represented through patterns in dimensions

### Example intuition
Embeddings help the model understand that:
- `king` and `queen` are related
- `dog` and `puppy` are semantically close
- context changes meaning

---

## Key Takeaways

- LLMs are large neural networks trained on huge text datasets
- They are far more flexible than older NLP models
- Transformers are a key breakthrough behind modern LLMs
- Embeddings let models represent language in mathematical space

---

## Glossary

**LLM**  
Large Language Model

**NLP**  
Natural Language Processing

**Transformer**  
A neural network architecture built around attention mechanisms

**Embedding**  
A vector representation of a token or word in numerical space

**Self-attention**  
A mechanism that helps the model decide which parts of the input matter most

---

## Personal Notes

- Add examples from class here
- Add diagrams later if needed
- Add links to papers or videos
