# Semantic Search

## Resource(s) Studied

* Pinecone: *Semantic Search Explained*
* IBM Technology: *What is a Vector Database? Powering Semantic Search & AI*

## What I Learned

### Semantic Search vs Keyword Search

Keyword search searches for the same words; semantic search searches for the the same meaning or intent.

| Query                      | Traditional Search                         | Semantic Search                                                     |
| -------------------------- | ------------------------------------------ | ------------------------------------------------------------------- |
| "car insurance"            | Documents containing "car" and "insurance" | Also finds "automobile coverage", "vehicle protection plans"        |
| "heart attack symptoms"    | Documents containing those exact words     | Also finds "myocardial infarction signs"                            |
| "how to reset my password" | Exact matches                              | Also finds "can't log in", "forgot credentials", "account recovery" |

This explains why keyword search often fails:

* Different people use different words for the same concept.
* Users make spelling mistakes.
* Synonyms and domain-specific terminology may not overlap.
* Exact keyword matching cannot capture context or intent.

### Vectors and Embeddings

* Vectors are simply data represented in numerical form.
* Vector embeddings translate unstructured content (text, images, audio, video) into high-dimensional numerical representations that capture meaning and context.
* Embeddings are arrays of numbers where each number represents a learned feature or characteristic of the input.
* Similar meanings tend to be represented by vectors that are close together in high-dimensional space.

Example:

```
"dog"    → [0.12, -0.45, 0.91, ...]
"puppy"  → [0.15, -0.41, 0.88, ...]
```

Since "dog" and "puppy" have similar meanings, their vectors are close to each other.

### Embeddings vs Model Weights

| Term                 | What it is                                                          |
| -------------------- | ------------------------------------------------------------------- |
| Parameters / Weights | The numbers the model learns during training                        |
| Embedding            | The vector produced by applying those learned weights to some input |
| Embedding Dimensions | The individual numbers inside that output vector                    |

An important nuance is that in older embedding models like CBOW and Skip-Gram, embeddings are directly learned as weight matrices. In modern transformer-based models, embeddings are computed representations produced by many layers of learned weights.

### How Semantic Search Works

The process involves:

1. Converting the user's query into an embedding.
2. Comparing it against embeddings stored in a vector database.
3. Using similarity search to find the closest matches.
4. Returning content with the most similar meaning, rather than the same words.

### Vector Similarity

Semantic search works because vectors with similar meanings occupy nearby positions in vector space. Similarity is measured mathematically using techniques such as:

* Cosine similarity
* Euclidean distance
* Dot product

### Semantic Search and RAG

One of the biggest insights for me was that Retrieval-Augmented Generation (RAG) is essentially:

```
Semantic Search + Large Language Model
```

The semantic search component retrieves relevant information, and the LLM uses that information to generate an accurate, context-aware response.

## Key Concepts Encountered

* Semantic Search
* Keyword Search
* Similarity Search
* Vectors
* Vector Embeddings
* Vector Databases
* Vector Storage
* Vector Indexing
* Vector Search
* Approximate Nearest Neighbour (ANN) Algorithms
* High-Dimensional Vector Space
* Similarity Metrics
* Retrieval-Augmented Generation (RAG)

## Mental Models / Analogies

### Semantic Search Pipeline

```
Question
    ↓
Embedding
    ↓
Vector Database
    ↓
Similarity Search
    ↓
Relevant Results
```

### Semantic Search vs Keyword Search

* Keyword search asks:

  > "Which documents contain these exact words?"

* Semantic search asks:

  > "Which documents mean the same thing?"

### Enterprise AI Perspective

Semantic search can be thought of as the retrieval skeleton of many modern enterprise AI systems.

## What Surprised Me

* Search engines historically relied much more heavily on exact keyword matching than I had realized.
* Semantic search can understand intent even when no keywords overlap.
* Embeddings are not the model's weights; they are outputs generated using those weights.
* RAG is conceptually simpler than it initially appears: retrieve relevant information first, then let the LLM reason over it.
* Vector databases are not universally superior and are optimized for a specific type of retrieval problem.

## Enterprise Implications

### Benefits of Vector Databases

* High speed and performance
* Scalability
* Lower computational costs for retrieval workflows
* Efficient data management and insertion
* Flexibility across text, images, video and other multimodal data

### Common Use Cases

* Retrieval-Augmented Generation (RAG)
* Conversational AI
* Recommendation engines
* Anomaly detection
* Semantic search applications

### Limitations

Vector databases are particularly effective for fact-based retrieval and similarity search, but they are not ideal for every type of query.

Tasks such as:

* topic summarization,
* trend analysis,
* thematic analysis,
* large-scale synthesis,

often require an LLM to examine all relevant information rather than retrieve only the nearest neighbours.

For example:

* Semantic search question:

  > "How do I reset my password?"

  Retrieve the most relevant documents.

* Thematic analysis question:

  > "What were the major customer complaints during the last year?"

  Retrieve all relevant records and allow the LLM to identify patterns and themes.

In such cases, list indexes, metadata filtering, or other non-vector retrieval methods may be more efficient than navigating vector space.

## Questions I Still Have

* How exactly are embedding dimensions learned during training?
* How do transformer-based embedding models differ internally from Word2Vec approaches such as CBOW and Skip-Gram?
* How do ANN algorithms achieve speed without checking every vector?
* How are embeddings updated when knowledge changes?
* How do enterprises decide when to use vector search versus traditional search or hybrid search?
* How do chunking strategies affect semantic search performance and RAG accuracy?

## Personal Reflection

This topic helped me understand the transition from traditional keyword search to meaning-based retrieval. It also connected several concepts I had previously studied separately, including embeddings, CBOW, Skip-Gram, sliding windows, vector databases and RAG.

A particularly satisfying realization was understanding that many modern AI experiences I already use every day—such as recommendation engines, semantic search, and content discovery systems—are fundamentally powered by embeddings and similarity search.
