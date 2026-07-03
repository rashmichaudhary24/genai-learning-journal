# Chunking Strategies

## Resource(s) Studied

* Pinecone — *Chunking Strategies for LLM Applications*

---

## What I Learned

Chunking is one of the most important design decisions in Retrieval-Augmented Generation (RAG) systems. It involves a fundamental trade-off between:

* **Semantic coherence** (keeping related information together),
* **Retrieval precision** (finding the most relevant information),
* **Latency and cost**, and
* **Fitting retrieved information into the context window of the LLM.**

In vector search systems, similarity is determined through **chunk-level comparisons** between the user query embedding and the embeddings of stored chunks. Therefore, how information is divided directly impacts retrieval quality.

### Criteria for Choosing a Chunking Strategy

A chunking strategy should be chosen based on:

* **The type of data being chunked**, e.g., long-form documents (books, articles, manuals), short-form content (tweets, chat messages, product descriptions), code, legal documents, etc.
* **The embedding model being used.** Different embedding models have been trained on different document types and exhibit different context window limitations and semantic behaviors.
* **The length and complexity of user queries.**
* **The purpose of retrieval**, such as:

  * Semantic search
  * Question answering
  * Retrieval-Augmented Generation (RAG)
  * Agentic workflows

---

## Chunking Methods

### 1. Fixed-Size Chunking

The simplest approach: divide documents into chunks containing a fixed number of tokens or characters.

* Chunk size should not exceed the embedding model's maximum input context window.
* In practice, chunk sizes are usually much smaller than the maximum supported context size.

---

### 2. "Content-Aware" Chunking

Chunk boundaries are determined by the document's structure rather than arbitrary token counts.

Examples:

* Chapters
* Sections
* Headers/sub-headers
* Paragraphs
* Tables
* HTML/Markdown structure

Content-aware chunking asks:

> **"How is this document organized?"**

---

### 3. Simple Sentence and Paragraph Splitting

Documents are divided using obvious linguistic boundaries:

* Sentences
* Paragraphs
* Sections

This preserves readability and often provides a good baseline.

---

### 4. Recursive Character-Level Chunking

Recursive chunking attempts to preserve the largest meaningful unit possible.

Typical separator hierarchy:

```text
Paragraphs (\n\n)
        ↓
Lines (\n)
        ↓
Words (space)
        ↓
Characters
```

It can be summarized as:

> **"Try to preserve the largest meaningful text unit possible (paragraph → line → word), and only split more aggressively when the chunk is still too large."**

This represents a practical middle ground between fixed-size and semantic chunking.

---

### 5. Document Structure / Hierarchical Chunking

Large documents can be chunked according to their inherent hierarchy.

Example:

```text
Book
   ↓
Chapter
   ↓
Section
   ↓
Paragraph
```

Examples include:

* Books
* Employee handbooks
* Policy manuals
* Technical documentation
* Legal documents

---

### 6. Semantic Chunking

Semantic chunking attempts to identify changes in meaning, topic, or theme and uses these transitions as chunk boundaries.

Examples:

* Topic shifts
* Concept changes
* Narrative transitions

Semantic chunking asks:

> **"What ideas or meanings belong together?"**

---

## Chunking Approaches Compared

| Chunking Type          | Question it Asks                                    |
| ---------------------- | --------------------------------------------------- |
| Fixed Chunking         | "Where do I hit the character/token limit?"         |
| Content-Aware Chunking | "What structural boundaries exist in the document?" |
| Semantic Chunking      | "What ideas or meanings belong together?"           |

---

## Advanced Chunking Techniques

### Contextual Chunking / Contextual Retrieval

Sometimes chunks lose meaning when separated from their larger document.

Anthropic's contextual retrieval approach addresses this by:

1. Providing an LLM with the entire document plus an individual chunk.
2. Asking the LLM to generate a brief description explaining the chunk's role within the larger document.
3. Appending this contextual description to the chunk before embedding.

Example:

```text
Context:
This chunk comes from the employee leave policy section
and describes eligibility criteria for paid leave.

Original chunk:
Employees become eligible after six months of employment.
```

This allows chunks to retain high-level document context while still benefiting from semantic search.

Prompt caching makes this approach economically feasible.

---

### Chunk Expansion

Chunking strategy and retrieval strategy do not need to be identical.

A common approach is:

**Store small chunks → Retrieve small chunks → Expand context during retrieval**

Example:

```text
Chunk 3 retrieved
        ↓
Retrieve neighboring chunks
        ↓
Chunk 2 + Chunk 3 + Chunk 4
        ↓
Provide expanded context to the LLM
```

Chunk expansion improves contextual understanding without sacrificing retrieval precision.

---

## Key Concepts Encountered

* Fixed-size chunking
* Recursive chunking
* Semantic chunking
* Hierarchical chunking
* Content-aware chunking
* Contextual retrieval
* Chunk expansion
* Chunk overlap
* Lost-in-the-middle problem
* Embedding context windows
* Prompt caching

---

## Mental Models / Analogies

Chunking is really answering a deceptively simple question:

> **"How much context should we show the AI at one time?"**

For example, imagine having an employee handbook:

```text
100-page handbook
        ↓
Should it be stored as:
        ↓
100 pages?
10 chapters?
500 paragraphs?
2000 sentences?
```

That decision affects:

* Retrieval quality
* Hallucinations
* Cost
* Latency
* Answer accuracy

---

Another useful mental model:

* **Content-aware chunking** asks:

> "How is this document organized?"

* **Semantic chunking** asks:

> "What is this document actually about?"

---

Chunk expansion can be thought of as:

> "Retrieve the sentence that matched, then read the surrounding paragraphs to understand what it means."

---

## What Surprised Me

Chunking is fundamentally an information management problem:

> **How do we break knowledge into pieces so that semantic search can retrieve the right information later?**

I was surprised to learn that:

* The maximum context window of an embedding model is merely an upper limit and not necessarily the optimal chunk size.
* Small chunks often produce better retrieval performance than large chunks.
* Retrieval and context provision can be optimized independently using chunk expansion.
* Contextual retrieval techniques can preserve document-level understanding without embedding entire documents.

---

## Enterprise Implications

Organizations implementing RAG systems must balance:

* Precision versus recall
* Context preservation versus retrieval accuracy
* Latency versus answer quality
* Storage costs versus retrieval effectiveness

There is no universal chunking strategy.

The optimal approach depends on:

* Document types
* User behavior
* Embedding models
* Business objectives
* Performance requirements

In practice, enterprise RAG systems often combine multiple chunking approaches.

---

## Questions I Still Have

* How can chunk quality be objectively measured?
* How does chunk size affect hallucination rates?
* How do agentic workflows influence chunking strategies?
* What are the best chunking strategies for structured enterprise data such as ERP and HRIS systems?
* When does semantic chunking become cost-prohibitive compared to content-aware chunking?

---

## Personal Reflection

A useful rule of thumb is:

> **If a chunk of text makes sense without the surrounding context to a human, it will likely make sense to the language model as well.**

Ultimately, chunking is not merely a preprocessing step; it is a knowledge representation problem that determines how effectively an AI system can retrieve, understand, and reason over information.
