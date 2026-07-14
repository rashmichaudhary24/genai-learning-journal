# Rerankers

## Resource(s) Studied

* Pinecone — *Rerankers and Two-Stage Retrieval*

---

## What I Learned

Reranking exists because a retriever's recall is typically higher than an LLM's effective recall. A retriever can identify a larger set of potentially relevant chunks, but an LLM cannot reliably process and recall all of them, especially in long contexts. Therefore, modern RAG systems often use a two-stage retrieval process:

1. **Retrieve** a larger set of candidate chunks using a fast retriever.
2. **Rerank** those candidates using a more accurate model before passing only the most relevant chunks to the LLM.

Retrieving the "top k" chunks based solely on vector similarity is often insufficient because the most relevant information may not appear in the top few retrieved chunks. Reranking helps recover these cases by performing a more precise relevance evaluation.

I also learned that embedding-based retrieval is inherently lossy because each chunk of text is compressed into a single fixed-length vector representation. This makes retrieval fast and scalable but imperfect, which is why reranking is necessary.

---

## Key Concepts Encountered

### top_k cutoff

The number of chunks initially retrieved from a vector database. Choosing a value that is too low may exclude relevant information, while choosing a value that is too high may overwhelm the LLM.

### LLM's Recall

An LLM's practical ability to identify and use relevant information from its context window. This is often lower than the retriever's recall, especially for long contexts.

### Retriever's Recall

The ability of a retrieval system to identify relevant documents or chunks from a corpus. Retrievers are optimized for high recall rather than perfect precision.

### Bi-encoder

A retrieval architecture in which queries and documents are encoded independently into vectors and compared using similarity measures. Embedding models used in RAG are typically bi-encoders.

### Cross-encoder

A model that evaluates a query and a document together, allowing direct interaction between their tokens. Cross-encoders are slower but significantly more accurate and are commonly used for reranking.

### Reranking

The process of reordering retrieved documents using a more sophisticated relevance model after the initial retrieval step.

### Similarity Score

A numerical measure (such as cosine similarity) indicating how semantically similar two embeddings are.

### Two-stage Retrieval

A retrieval pipeline consisting of:

* Stage 1: Fast retrieval using a bi-encoder.
* Stage 2: Precise reranking using a cross-encoder.

### Semantic Search

A search technique that retrieves information based on meaning rather than exact keyword matches.

### Lexical Search

A search technique that retrieves information based on exact words, phrases, or keyword overlap.

### "Lost in the Middle"

A phenomenon in which LLMs are more likely to miss information placed in the middle of a long context window than information placed near the beginning or end.

---

## Mental Models / Analogies

### Preparing for an Interview (Bi-encoder)

Preparing for an interview resembles a bi-encoder retrieval system. I prepare numerous answers and mentally organize them into semantic categories. When an interviewer asks a question, I rapidly retrieve the answer that seems most semantically relevant.

### Consulting Notes During an Interview (Cross-encoder)

If the interviewer allowed me to consult my preparation notes, I could compare the actual question against several candidate answers before responding. This resembles how a cross-encoder reranker compares a query and retrieved chunks together to determine true relevance.

### Bihar Examination Strategy and "Lost in the Middle"

A humorous analogy for the "Lost in the Middle" phenomenon comes from a common examination strategy: students write an excellent introduction and conclusion because they know examiners tend to focus on the beginning and end of long answers. Similarly, LLMs often pay disproportionate attention to information appearing at the start or end of a context window.

---

## What Surprised Me

* That an entire chunk of text is compressed into a single fixed-length vector.
* That LLMs internally represent each token as a vector, whereas embedding models ultimately compress an entire chunk (consisting of many token vectors) into a single fixed-length embedding vector for efficient retrieval.
* That a retriever can have better practical recall than the LLM consuming its output.
* That providing information to an LLM can sometimes degrade performance if that information is buried in the middle of a long context window.
* That modern RAG systems often depend as much on retrieval quality and context management as on the underlying LLM itself.

---

## Enterprise Implications

* Simply increasing context window size is not sufficient for building effective enterprise RAG systems.
* Retrieval quality, reranking, and context organization significantly impact answer quality.
* Enterprises should avoid passing large quantities of retrieved content directly to LLMs and instead use reranking to improve precision.
* Hybrid retrieval (combining semantic and lexical search) can improve performance on domain-specific terminology, product names, IDs, and exact matches.
* Understanding "Lost in the Middle" is important when designing prompts and arranging retrieved context.
* Two-stage retrieval architectures provide a practical balance between speed, cost, and accuracy.

---

## Questions I Still Have

* How exactly do embedding models compress hundreds of token vectors into a single embedding?
* What architectural features cause the "Lost in the Middle" phenomenon?
* How do modern long-context models attempt to mitigate this problem?
* What metrics are typically used to evaluate reranker performance?
* When should lexical search, semantic search, or hybrid search be preferred in enterprise RAG systems?
* How do organizations determine the optimal value of top_k?

---

## Personal Reflection

Before studying rerankers, I assumed that retrieving the top few semantically similar chunks would be sufficient for RAG. I now understand that retrieval itself is only the first stage of a larger process. I found it particularly fascinating that embedding models compress an entire chunk into a single vector and that LLMs can sometimes perform worse when relevant information is hidden within large contexts. The concepts of bi-encoders, cross-encoders, reranking, and "Lost in the Middle" have helped me appreciate why enterprise AI systems require careful retrieval design rather than simply larger models or larger context windows.
