
# Transformer Architecture

## Resources Studied

* 3Blue1Brown – *Attention in Transformers, Step-by-Step*
* Jay Alammar – *The Illustrated Transformer*

---

## In One Sentence

The Transformer is a deep learning architecture that uses attention to understand relationships between tokens and process many tokens in parallel.

---

## What Is It?

A Transformer is a neural network architecture introduced in the 2017 paper **Attention Is All You Need**.

Unlike earlier sequence models such as Recurrent Neural Networks (RNNs), Transformers process many tokens simultaneously instead of one token at a time. This makes them significantly faster to train and better at modelling long-range relationships.

The original Transformer architecture consists of:

```
Input
   ↓
Embedding
   ↓
Positional Encoding
   ↓
Multiple Encoder Layers
   ↓
Multiple Decoder Layers
   ↓
Linear Layer
   ↓
Softmax
   ↓
Output
```

Modern Large Language Models such as GPT are based on the Transformer architecture but typically use only the decoder stack.

---

## Why Was It Invented?

Before Transformers, sequence models processed tokens one after another.

This sequential nature made training slow and made it difficult for models to capture relationships between words that were far apart in a sentence.

The Transformer replaced recurrence with attention, allowing every token to directly examine every other relevant token in a single layer.

Because all tokens can be processed simultaneously, Transformer models are highly parallelizable during training.

---

## High-Level Flow of Information

### Step 1 — Tokenization

The input is broken into tokens.

Depending on the application, these could represent words, subwords, characters, image patches, audio segments, or other discrete units.

---

### Step 2 — Embeddings

Each token is converted into a dense numerical vector called an embedding.

These embeddings capture semantic meaning.

For example,

```
Embedding(King)
− Embedding(Man)
+ Embedding(Woman)

≈ Embedding(Queen)
```

This demonstrates that certain directions within embedding space capture meaningful relationships such as gender.

(See the Embeddings note.)

---

### Step 3 — Encoder Stack

The sequence of embeddings passes through multiple encoder layers.

Each encoder layer contains:

* Multi-Head Self-Attention
* Feed Forward Network
* Residual Connections
* Layer Normalization

The self-attention mechanism allows every token to gather relevant information from the other tokens.

The feed-forward network then processes each token independently, enriching its representation without exchanging information between tokens.

Each successive encoder layer produces a richer contextual understanding than the previous one.

---

### Step 4 — Decoder Stack

The decoder receives:

* the encoder's output
* the tokens generated so far

Each decoder layer performs:

* Masked Self-Attention
* Cross-Attention
* Feed Forward Network

The decoder gradually refines its understanding before predicting the next token.

Like the encoder, multiple decoder layers progressively improve the representation used for generation.

---

### Step 5 — Prediction

The final decoder representation is projected into a vector whose length equals the model's vocabulary size.

Each value (called a logit) represents the model's score for one possible next token.

Softmax converts these logits into a probability distribution.

The model then selects (or samples) the next token.

---

## Model Parameters (Weights)

A Transformer's behaviour is determined by millions or billions of learned parameters called **weights**.

These weights are learned during training using backpropagation.

Examples include:

* Embedding Matrix
* Query Matrix
* Key Matrix
* Value Matrix
* Output Projection Matrix
* Feed Forward Up-Projection Matrix
* Feed Forward Down-Projection Matrix
* Unembedding Matrix

Unlike attention weights, which are computed anew for every input, these model weights remain fixed during inference.

---

## Parallelization

One of the Transformer's biggest advantages is that many computations can happen simultaneously.

For example:

* embeddings for all tokens can be computed together
* self-attention considers all tokens in one operation
* feed-forward networks process every token independently in parallel

This parallelism dramatically reduces training time compared with earlier recurrent architectures.

---

## Context Window

A Transformer can only process a limited number of input tokens at one time.

This limit is called the **context window**.

If earlier tokens fall outside this window, the model can no longer directly attend to them.

---

## Common Misconceptions

### "A Transformer is multiple neural networks."

No.

A Transformer is one neural network architecture composed of many layers.

---

### "Attention is used to make Transformers faster."

Not exactly.

Attention was introduced to better model relationships between tokens.

The ability to process tokens in parallel is a major advantage that follows from this design.

---

### "The Transformer predicts words."

Not exactly.

It predicts the next **token**, which may be a word, part of a word, punctuation, or another unit depending on the tokenizer.

---

## Key Takeaways

* A Transformer is a neural network architecture built from stacks of encoder and decoder layers.
* Self-attention enables every token to gather information from every other relevant token.
* Feed-forward networks enrich each token independently.
* Multiple layers progressively refine the representation.
* Learned weights determine how the model behaves.
* The final layer produces a probability distribution over the vocabulary for the next token.

