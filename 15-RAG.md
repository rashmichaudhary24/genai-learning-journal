# Retrieval-Augmented Generation (RAG)

## Resource(s) Studied

* Pinecone — *Retrieval-Augmented Generation (RAG)*
* IBM Technology — *What is Retrieval-Augmented Generation (RAG)?*
* NVIDIA — *What is Retrieval-Augmented Generation?*
* Pinecone — *Rerankers and Two-Stage Retrieval*

---

# What Problem Does RAG Solve?

Large Language Models are trained on enormous amounts of data, but they have several limitations:

* Their knowledge becomes outdated.
* They cannot access private or proprietary information.
* They may hallucinate.
* They cannot reliably provide citations.
* Retraining models is expensive and slow.

**Retrieval-Augmented Generation (RAG)** addresses these problems by allowing the model to retrieve relevant external information at inference time rather than relying solely on what it learned during training.

In other words:

> **Fine-tuning changes the model's memory.**
>
> **RAG changes the information available to the model while it is thinking.**

---

# The Fundamental Building Blocks of RAG

When I think about RAG conceptually, I find it useful to ignore vendor architectures and instead ask:

> **What components must exist for retrieval-augmented generation to work?**

A RAG system fundamentally requires:

```text
Knowledge Base
        ↓
Embedding Model
        ↓
Vector Database
        ↓
Retriever
        ↓
Reranker (optional)
        ↓
Context Injection
        ↓
LLM
```

---

## 1. Knowledge Base

The knowledge base is the source of truth.

Examples:

* Enterprise documents
* Wikis
* PDFs
* Product catalogs
* APIs
* Databases
* Research papers

The knowledge itself is not directly searchable by semantic similarity.

It must first be transformed.

---

## 2. Embedding (Retriever) Model

The embedding model converts text into vectors.

Examples:

* Sentence Transformers
* BGE
* E5
* OpenAI Embeddings

Example:

```text
"Paris is the capital of France"
                    ↓
             Embedding Model
                    ↓
         [0.12, 0.83, -0.45]

"What city contains the Eiffel Tower?"
                    ↓
             Embedding Model
                    ↓
         [0.14, 0.79, -0.43]
```

The embedding model creates a semantic vector space in which similar meanings are located near one another.

A key realization for me was that:

> The retriever model does not perform retrieval.
>
> It creates the embeddings that make retrieval possible.

---

## 3. Vector Database

The vector database stores embeddings and performs similarity search.

Examples:

* Pinecone
* Weaviate
* Milvus
* Chroma
* FAISS

The vector database stores:

```text
Vector
        ↓
Associated document chunk
```

Example:

| Vector            | Chunk                          |
| ----------------- | ------------------------------ |
| [0.12,0.83,-0.45] | Paris is the capital of France |
| [0.15,0.79,-0.43] | The Eiffel Tower is in Paris   |

When a query embedding arrives, the vector database finds the nearest vectors.

The vector database is therefore the component that actually performs semantic retrieval.

---

## 4. Retriever

The retriever orchestrates the retrieval process.

Its responsibilities include:

* embedding the query,
* searching the vector database,
* retrieving candidate chunks.

Modern retrievers often use:

* Dense retrieval
* Sparse retrieval
* Hybrid retrieval

The retriever prioritizes:

> **Recall**

Its job is to avoid missing relevant information.

---

## 5. Reranker

Retrievers optimize for recall.

LLMs require precision.

Rerankers bridge this gap.

Example:

```text
Query
      ↓
Retriever
      ↓
Top 100 chunks
      ↓
Reranker
      ↓
Top 5 chunks
      ↓
LLM
```

Rerankers are slower but more accurate than retrievers.

This architecture is called:

> **Two-stage retrieval.**

---

## 6. Context Injection

Context injection is the process of inserting retrieved information into the prompt sent to the LLM.

Example:

```text
Question:
What is our leave policy?

Retrieved Context:
Employees receive 24 days of annual leave.

Prompt:

Answer using the provided context.

Context:
Employees receive 24 days of annual leave.

Question:
What is our leave policy?
```

The quality of context injection depends on:

* retrieval quality,
* chunk size,
* context ordering,
* token limits,
* context window size.

---

## 7. Generator (LLM)

The generator is the language model itself.

Examples:

* GPT
* Claude
* Gemini
* Llama

The generator receives:

* the user's query,
* retrieved context,
* instructions,

and produces the final answer.

---

# Retrieval Pipeline

A retrieval pipeline is the sequence of operations used to retrieve and prepare information for the LLM.

```text
Documents
      ↓
Chunking
      ↓
Embedding
      ↓
Vector Database

                    User Query
                          ↓
                    Embedding
                          ↓
                      Retrieval
                          ↓
                      Reranking
                          ↓
                  Context Injection
                          ↓
                          LLM
                          ↓
                      Response
```

---

# Grounding

Grounding means constraining the model's responses using trusted external information.

Without grounding:

```text
LLM:
I think revenue was approximately $3.4 billion.
```

With grounding:

```text
Retrieved Document:
FY2025 Revenue = $2.9 billion

LLM:
According to the document,
FY2025 revenue was $2.9 billion.
```

RAG is fundamentally a grounding technique.

Grounding provides:

* factual accuracy,
* explainability,
* source attribution,
* reduced hallucinations,
* greater trustworthiness.

---

# Agentic RAG

Traditional RAG performs:

```text
Retrieve
      ↓
Generate
```

Agentic RAG performs:

```text
Reason
      ↓
Retrieve
      ↓
Validate
      ↓
Retrieve Again
      ↓
Reason
      ↓
Generate
```

Agentic RAG systems may:

* rewrite queries,
* decompose problems,
* invoke tools,
* perform multiple retrievals,
* validate information,
* aggregate evidence.

---

# Mental Models

### Traditional LLM

> Answer from memory.

### RAG

> Consult the library first, then answer.

---

### Fine-Tuning

> Rewriting someone's memory.

### RAG

> Giving someone access to Google and a company knowledge portal.

---

# What Surprised Me

* Retrieval quality often matters more than model quality.
* Chunking dramatically impacts answer quality.
* Reranking exists because retrievers optimize recall while LLMs require precision.
* A modern RAG system may contain multiple specialized AI models.
* Enterprise AI increasingly focuses on knowledge architecture rather than model architecture.

---

# Personal Reflection

Learning RAG fundamentally changed how I think about enterprise AI.

I initially assumed that building better AI systems meant building better models. I now understand that enterprise AI is often less about the model itself and more about designing an effective knowledge architecture around the model.

The most important insight for me was realizing that a RAG system is not a single AI model. It is a collection of specialized components—knowledge bases, embedding models, vector databases, retrievers, rerankers, and LLMs—working together to produce accurate, grounded, and trustworthy responses.

---
