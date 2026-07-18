# Attention Mechanism

## Resource(s) Studied

- 3Blue1Brown – *Attention in Transformers*
- Jay Alammar – *The Illustrated Transformer*

---

# In One Sentence

Attention is the mechanism by which each token decides which other tokens in the sequence are most relevant before updating its own representation.

---

# What Is It?

A token begins life with a static embedding that captures its general meaning. However, words derive their actual meaning from context. For example, the word *bank* may refer to a financial institution, a river bank or trusting someone.

Attention enables each token to gather information from other relevant tokens before updating its representation. Each token first produces three learned projections from its current representation: a Query, a Key and a Value. The Query and Key **together** determine where to look, while the Value determines what information is gathered.

- **Query (Q):** What kind of information am I looking for?
- **Key (K):** What information can I offer?
- **Value (V):** If I am relevant, what information should I contribute?

The compatibility between a token's Query and every other token's Key is measured using a dot product. These compatibility scores determine how much influence each Value vector has when constructing the token's new contextual representation.

---

# Why Was It Invented?

Earlier sequence models compressed an entire sentence into a single fixed representation before producing an output. As sentences became longer, important information was lost.

Attention removed this bottleneck by allowing every token to dynamically gather information from the most relevant parts of the sequence instead of relying on a single compressed representation.

---

# What Problem Does It Solve?

Attention solves the problem of **contextual understanding**.

Instead of assigning a fixed meaning to every word, it allows each token to interpret itself based on the surrounding context. This enables the model to capture relationships such as modifiers, references, dependencies and long-range interactions.

---

# What I Learned

A token is a chunk of text. It may represent a word, part of a word, punctuation, numbers or even spaces.

Every token begins with one learned embedding. During each attention layer, that representation is updated using information gathered from other relevant tokens. By the final layer, each token has evolved into a rich contextual representation.

To illustrate self-attention, consider the sentence:

> **She wears a red gown.**

Suppose we are updating the representation of **gown**.

Its Query asks, in effect,

> *"Which words contain information that would help me understand myself?"*

The Keys of all tokens are compared with this Query using a dot product. Higher compatibility scores indicate greater relevance.

The resulting attention pattern can be visualised as follows.

![Self-Attention Matrix](images/self_attention_matrix.png)

Once the attention weights have been computed, the corresponding Value vectors are combined to produce a new **contextual representation** for **gown**.

Although we have described the process for a single token, every token in the sequence performs the same computation simultaneously using its own Query vector.

Because GPT predicts the next token, future tokens must not influence earlier ones. My diagram places Queries on the columns and Keys on the rows, so the lower-left portion of the matrix is masked, ensuring that each token cannot attend to future tokens and that each prefix becomes an independent training opportunity.

An eight-word sentence therefore provides eight training opportunities:

- Predict token 2 from token 1.
- Predict token 3 from tokens 1–2.
- Predict token 4 from tokens 1–3.
- ...
- Continue until the context window.

If a model has a context window of 8,000 tokens, the attention mechanism conceptually compares every token with every other token within those 8,000 tokens. Consequently, the attention matrix grows with the size of the context window, allowing later tokens to draw information from much earlier parts of the input.

For example, when predicting the final word of a mystery novel, the model can attend to clues introduced much earlier in the story, provided they still lie within the context window.

This example illustrates a single attention head. In practice, Transformers use multi-head attention, where the model learns multiple sets of Query, Key and Value projection matrices. This allows different heads to focus on different aspects of the same sequence simultaneously, enabling richer contextual representations than a single head could learn on its own.

Cross-attention extends the same idea by allowing Queries from one sequence to attend to Keys and Values from another sequence.

For example, during translation:

![Cross-Attention Matrix](images/cross_attention_matrix.png)

Unlike self-attention, the two axes represent different sequences.

Each round of attention enriches every token with information gathered from other tokens. In the next layer, these richer representations interact again, allowing context to accumulate progressively. Over many Transformer layers, this iterative refinement enables the model to capture increasingly abstract concepts such as sentiment, tone, writing style and relationships between ideas.

Attention is also one of the key reasons Transformers scale well because all Query-Key comparisons can be be computed in parallel.

---

# Mental Model

Every token starts with a rough understanding of itself.

Before deciding what it really means, it asks every other token,

> **"Do you have information that is useful to me?"**

Relevant tokens respond more strongly, contribute more of their Value vectors, and collectively help produce a richer contextual representation.

In other words,

> **Attention tells a token where to look before deciding who it is.**

---

# Enterprise Implications

Attention enables LLMs to reason over relationships rather than isolated words. This makes them capable of understanding long documents, following instructions, resolving references, summarising information and maintaining coherence across large contexts.

Many enterprise use cases—including document analysis, code generation, legal review and knowledge retrieval—depend on this ability to relate information across a sequence.

---

# How This Changes the Way I Use AI

I now understand that LLMs do not interpret prompts one sentence at a time.

Every token influences how subsequent tokens are interpreted. This reinforces the importance of providing sufficient context, placing critical information clearly within the prompt, and recognising that wording changes the relationships the model discovers rather than simply changing individual words.

---

# Common Misconceptions

- Self-attention does **not** mean a token only attends to itself. It attends to every token in the same sequence, including itself.
- Keys do not explicitly encode concepts such as *"I am an adjective."* Query, Key and Value vectors are learned during training.
- Attention does not create understanding on its own. Rich representations emerge through many stacked Transformer layers working together with feed-forward networks and residual connections.
- Cross-attention is different from self-attention because the Queries and the Keys/Values come from different sequences.

---

# Questions I Still Have

- Why is the dot product the preferred measure of compatibility?
- Why are three separate projections (Query, Key and Value) needed instead of one?
- How do different attention heads naturally specialise during training?
- Why does scaling model size produce such large qualitative improvements?
- How exactly does the model learn the Query, Key and Value projection matrices?

---

# Key Takeaway

Attention is not about giving every word equal importance. It is a mechanism that allows every token to dynamically decide what information matters before updating its own representation. This ability to build context through learned relationships is what made the Transformer architecture both highly parallelisable and dramatically more capable than earlier sequence models.
