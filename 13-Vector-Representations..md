# Vector Representations

## Resource(s) Studied

* Jay Alammar — *The Illustrated Word2Vec*
* StatQuest: *Word Embeddings Explained*

---

## What I Learned

A vector representation is a list of numbers that encodes the meaning or characteristics of an object in a multidimensional space. Similar objects are represented by vectors that are located close together.

Vector representations allow AI systems to work with meaning mathematically, enabling semantic search, retrieval, recommendations, clustering, and retrieval-augmented generation (RAG).

Unlike traditional computing, where meaning is explicitly defined by humans, AI systems learn mathematical representations of meaning from data. This allows concepts with similar meanings to occupy nearby regions of a vector space.

I also learned that vector representations are not limited to words. They can represent documents, images, products, users, songs, videos, and even abstract concepts. Once represented as vectors, all of these can be searched, compared, grouped, and manipulated mathematically.

---

## Key Concepts Encountered

* Vector representations
* Word embeddings
* Vector spaces
* Dimensions
* Semantic similarity
* Distance and proximity
* Context windows
* Sliding windows
* CBOW (Continuous Bag of Words)
* Skip-Gram
* Training embeddings
* Semantic search

---

## Mental Models / Analogies

### Coordinates for Meaning

Just as latitude and longitude represent a physical location on Earth, vector representations provide coordinates for meaning in a conceptual space.

### A Map of Concepts

A vector space can be imagined as a map where related ideas cluster together. "Dog" is close to "puppy," "doctor" is close to "physician," and unrelated concepts are farther apart.

### Meaning as Geometry

One of the most profound ideas I encountered is that meaning can be represented geometrically. Once meaning becomes geometry, AI systems can perform mathematical operations on meaning itself.

### "You Shall Know a Word by the Company It Keeps"

Words that frequently appear in similar contexts develop similar vector representations. For example, "doctor" and "physician" occupy nearby locations because they tend to appear in similar contexts.

---

## What Surprised Me

Had never put together the fact that the next-word prediction which Google and WhatsApp and iPhone have been doing for so long was fundamentally the same objective as ChatGPT and other LLMs.

The difference is mostly one of scale, training, and capability, not the underlying objective.

| Predictive Text on Phone             | LLMs like ChatGPT                                           |
| ------------------------------------ | ----------------------------------------------------------- |
| Predicts the next word               | Predicts the next token                                     |
| Trained on relatively small datasets | Trained on trillions of tokens                              |
| Uses simpler models                  | Uses massive transformer neural networks                    |
| Has very limited context             | Can use thousands to millions of tokens of context          |
| Produces a few suggested words       | Generates conversations, essays, code, and reasoning traces |

Another surprising insight was that many AI capabilities I had thought of as separate technologies—recommendation engines, semantic search, RAG, clustering, similarity detection, and personalization—are all fundamentally built upon vector representations.

---

## My Understanding of Sliding Windows, CBOW, and Skip-Gram

A sliding window moves across a sentence and determines which words are considered the context and which word is considered the target.

For example, in the sentence:

> The quick brown fox jumps over the lazy dog

a sliding window can be used to generate multiple context-target training examples.

**CBOW (Continuous Bag of Words)** learns by using the surrounding context words to predict the target word.

In other words:

> Given the neighbours, who is this word?

For example:

> (The, quick, fox, jumps) → brown

CBOW treats the surrounding words together as a group and uses them to predict the missing or target word.

**Skip-Gram** works in the opposite direction. It learns by using the target word to predict the surrounding context words.

In other words:

> Given this word, who are its neighbours?

For example:

> brown → The, quick, fox, jumps

The key insight is that by repeatedly predicting words from context (or context from words), AI systems automatically learn meaningful vector representations.

---

## Enterprise Implications

Vector representations are foundational to modern enterprise AI systems because they allow organizations to search and retrieve information based on meaning rather than exact keywords.

Enterprise applications include:

* Semantic search
* Recommendation systems
* Customer support assistants
* Enterprise knowledge retrieval
* Retrieval-Augmented Generation (RAG)
* Personalization engines
* Document classification
* Similarity analysis
* Memory systems for AI agents

Understanding vector representations helped me realize that embeddings and vector databases are not niche technologies but core infrastructure components for enterprise AI adoption.

---

## Questions I Still Have

* How exactly do billions of parameters in a neural network produce meaningful vector spaces?
* Why do some semantic relationships emerge naturally during training?
* How do embedding models determine the number of dimensions to use?
* How are vector representations updated as models continue learning?
* How do enterprise systems decide which embedding model to use?
* What are the limitations of representing meaning geometrically?

---

## Personal Reflection

This topic fundamentally changed how I think about AI.

Before studying vector representations, I viewed AI systems as sophisticated pattern-matching tools. After learning about embeddings and vector spaces, I began to understand that modern AI systems create mathematical representations of meaning itself.

The realization that meaning can be converted into geometry, and that geometry can then be searched, compared, and manipulated mathematically, was one of the most important conceptual breakthroughs in my AI learning journey so far.

I also realized that many of the AI applications I interact with every day—search engines, recommendation systems, predictive text, social media feeds, and generative AI systems—are all built upon the same underlying idea: representing meaning as vectors.
