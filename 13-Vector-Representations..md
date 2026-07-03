# Vector Representations

## Resource(s) Studied

* Jay Alammar — *The Illustrated Word2Vec*
* StatQuest: *Word Embeddings Explained*

---

## What I Learned

A vector representation is a list of numbers that encodes the meaning or characteristics of an object in a multidimensional space. Similar objects are represented by vectors that are located close together.

Vector representations allow AI systems to work with meaning mathematically, enabling semantic search, retrieval, recommendations, clustering, similarity analysis, and retrieval-augmented generation (RAG).

Unlike traditional computing, where meaning is explicitly defined by humans, AI systems learn mathematical representations of meaning from data. This allows concepts with similar meanings to occupy nearby regions of a vector space.

I also learned that vector representations are not limited to words. They can represent documents, images, products, users, songs, videos, and even abstract concepts. Once represented as vectors, all of these can be searched, compared, grouped, and manipulated mathematically.

One of the most important ideas I encountered was that meaning itself can be represented geometrically. Once meaning becomes geometry, AI systems can perform mathematical operations on meaning.

I also learned that models often learn through contrast. They learn not only what things are similar, but also what things are dissimilar. This principle appears in word embeddings, image classification, recommendation systems, and many other areas of AI.

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
* Negative sampling
* Positive and negative examples
* Training embeddings
* Semantic search
* Recommendation systems
* Emergent representations
* Next-token prediction

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

### Learning by Contrast

AI systems often learn what something is by simultaneously learning what it is not. Models become better at identifying patterns by comparing positive and negative examples.

---

## What Surprised Me

Had never put together the fact that the next-word prediction performed by Google keyboards, WhatsApp, and iPhone predictive text was fundamentally the same objective used by ChatGPT and other LLMs.

The difference is mostly one of scale, training, architecture, and capability, rather than the underlying objective.

| Predictive Text on Phone             | LLMs like ChatGPT                                           |
| ------------------------------------ | ----------------------------------------------------------- |
| Predicts the next word               | Predicts the next token                                     |
| Trained on relatively small datasets | Trained on trillions of tokens                              |
| Uses simpler models                  | Uses massive transformer neural networks                    |
| Has very limited context             | Can use thousands to millions of tokens of context          |
| Produces a few suggested words       | Generates conversations, essays, code, and reasoning traces |

One of the most surprising ideas I encountered was that many capabilities of modern AI emerged from an apparently simple objective: predict the next token.

Researchers sometimes summarize this realization humorously as:

> "We trained a machine to autocomplete the Internet, and it accidentally learned to think."

While this is an oversimplification, it captures the remarkable fact that language understanding, translation, coding, reasoning, and conversation can emerge from large-scale next-token prediction.

Another surprising insight was that many AI capabilities I had thought of as separate technologies—recommendation engines, semantic search, RAG, clustering, similarity detection, personalization, and generative AI—are fundamentally built upon vector representations.

One of the most mind-expanding realizations was:

> "I can be represented as a vector of numbers."

This helped me understand that recommendation systems work because users, products, content, and preferences can all be represented within the same mathematical space, where similarity corresponds to proximity.

I also realized that one of the foundational ideas behind modern AI is remarkably simple: train a model to predict words from context at massive scale, and meaningful semantic structure emerges as a side effect.

---

## My Understanding of Sliding Windows, CBOW, and Skip-Gram

A sliding window moves across a sentence and determines which words are considered the context and which word is considered the target.

For example, in the sentence:

> The quick brown fox jumps over the lazy dog

a sliding window can be used to generate multiple context-target training examples.

### CBOW (Continuous Bag of Words)

CBOW learns by using the surrounding context words to predict the target word.

In other words:

> Given the neighbours, who is this word?

For example:

> (The, quick, fox, jumps) → brown

CBOW treats the surrounding words together as a group and uses them to predict the missing or target word.

### Skip-Gram

Skip-Gram works in the opposite direction. It learns by using the target word to predict the surrounding context words.

In other words:

> Given this word, who are its neighbours?

For example:

> brown → The, quick, fox, jumps

The key insight is that by repeatedly predicting words from context (or context from words), AI systems automatically learn meaningful vector representations.

---

## My Understanding of Negative Sampling

Word2Vec does not learn only from words that occur together. During training, it also creates "negative" examples consisting of words that are unlikely to occur together.

For example, if:

> (doctor, hospital)

is a positive example because the words frequently appear together, then examples such as:

> (doctor, banana)

or

> (doctor, mountain)

may be used as negative examples.

The model learns by increasing the similarity of positive examples and decreasing the similarity of negative examples.

This helped me understand a broader principle of machine learning:

> Models often learn what something is by simultaneously learning what it is not.

This is conceptually similar to image classification, where a model learns to recognize cats not only by seeing cats, but also by seeing examples of non-cats.

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
* Fraud detection
* Content recommendation
* User behavior modeling

Understanding vector representations helped me realize that embeddings and vector databases are not niche technologies but core infrastructure components for enterprise AI adoption.

---

## Questions I Still Have

* How exactly do billions of parameters in a neural network produce meaningful vector spaces?
* Why do some semantic relationships emerge naturally during training?
* How do embedding models determine the number of dimensions to use?
* How are vector representations updated as models continue learning?
* How do enterprise systems decide which embedding model to use?
* What are the limitations of representing meaning geometrically?
* Why do some capabilities emerge unexpectedly from simple training objectives?

---

## Personal Reflection

This topic fundamentally changed how I think about AI.

Before studying vector representations, I viewed AI systems primarily as sophisticated pattern-matching tools. After learning about embeddings and vector spaces, I began to understand that modern AI systems create mathematical representations of meaning itself.

The realization that meaning can be converted into geometry, and that geometry can then be searched, compared, and manipulated mathematically, was one of the most important conceptual breakthroughs in my AI learning journey so far.

I also realized that many of the AI applications I interact with every day—search engines, recommendation systems, predictive text, social media feeds, personalized advertisements, and generative AI systems—are all built upon the same underlying idea: representing meaning as vectors.

Perhaps the most profound realization was that words, documents, products, preferences, and even people can all be represented mathematically within the same conceptual space. This changed my understanding of AI from "machines recognizing patterns" to "machines constructing and operating within geometric representations of meaning."
