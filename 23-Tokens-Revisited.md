# Tokens Revisited

## Resource(s) Studied

* OpenAI Cookbook – *How to Count Tokens with tiktoken*
* Hugging Face NLP Course – *Tokenization*
* OpenAI Tokenizer
* Jay Alammar – *The Illustrated GPT-2* (Tokenization overview)
* Andrej Karpathy – *Let's Build the GPT Tokenizer*

---

# In One Sentence

Language models do not read words or characters directly—they first convert text into discrete units called **tokens**, and different tokenizers may split the same text differently.

---

# Why Do We Need Tokens?

Language models work with numbers, not text.

Before a model can process a sentence, the text must first be converted into smaller pieces called **tokens**, which are then mapped to numerical IDs.

These tokens become the basic units that flow through embeddings, attention mechanisms, and every other stage of the model.

Without tokenization, an LLM cannot process text at all.

---

# Tokens Are Not Words

One of the biggest misconceptions is that a token is simply a word.

It isn't.

A token can be:

* an entire word
* part of a word
* punctuation
* a number
* part of a number
* an emoji
* or another frequently occurring piece of text.

For example:

| Text | Possible Tokenization |
|------|------------------------|
| Hello! | `[Hello] [!]` |
| Artificial Intelligence | `[Artificial] [Intelligence]` |
| RashmiChaudhary24 | `[Rash] [mi] [Chaud] [hary] [24]` |
| ₹25,00,000 | `[₹] [25] [,] [00] [,] [000]` |

These are **illustrative examples**. The exact token boundaries depend on the tokenizer being used.

---

# Why Not Just Split by Words?

Word-level tokenization sounds simple but creates several problems.

Consider words like:

* ChatGPT
* RashmiChaudhary24
* cryptocurrency
* anti-disestablishmentarianism

A word-based tokenizer would either need an impossibly large dictionary or classify many words as "unknown."

Character-level tokenization solves that problem but creates another one—sequences become far too long.

For example,

```
Artificial Intelligence
```

would become twenty-three individual characters instead of just a few meaningful pieces.

Subword tokenization provides a practical balance between these two extremes.

---

# Byte Pair Encoding (BPE)

Most modern tokenizers use some form of **subword tokenization**.

One of the most influential techniques is **Byte Pair Encoding (BPE).**

Instead of storing every possible word, BPE learns the most frequently occurring pieces of text.

It begins with very small units and repeatedly merges the most common adjacent pairs.

Over many iterations, common chunks such as

* `ing`
* `tion`
* `pre`
* `Artificial`
* ` Intelligence`

become individual tokens.

Rare words are then represented by combining these learned pieces.

In other words, the tokenizer learns **reusable building blocks** rather than memorising every word.

---

# Character Count ≠ Token Count

One of the most interesting observations was that token count is **not directly proportional** to character count.

A shorter piece of text can use more tokens than a longer one.

Why?

Because tokenization depends primarily on **how efficiently the tokenizer can represent the text**, not on its length.

Common words and phrases are often stored as single tokens, while unfamiliar names, symbols or rare combinations may be split into several smaller pieces.

---

# Why Different Models Count Tokens Differently

Different models use different tokenizers.

Each tokenizer has its own vocabulary learned from different training data.

As a result, the same text may produce different token counts across GPT, Claude, Gemini or Llama.

This explains why:

* context windows cannot be compared purely by token count,
* pricing differs between models,
* and the same prompt may consume different numbers of tokens on different platforms.

Token count is therefore **a property of both the text and the tokenizer**.

---

# Why This Matters

Tokenization affects far more than just preprocessing.

It directly influences:

* prompt cost
* inference latency
* context window usage
* document chunking
* Retrieval-Augmented Generation (RAG)
* API pricing

A prompt that appears short may still consume many tokens if it contains rare names, symbols or unusual formatting.

---

# One Insight That Stood Out

I initially assumed that tokenization was simply a way of splitting text.

It is more accurate to think of it as a **compression strategy**.

The tokenizer tries to represent text as efficiently as possible by using frequently occurring pieces as reusable building blocks.

The better the tokenizer's vocabulary matches the input, the fewer tokens are needed to represent it.

---

# Common Misconceptions

❌ One word always equals one token.

❌ More characters always mean more tokens.

❌ Token counts are the same across all models.

❌ Emojis always count as one token because they appear as one character.

---

# How This Changes the Way I Think About AI

Understanding tokenization makes several concepts from earlier topics much clearer.

Embeddings are created **after** tokenization.

Attention operates over **tokens**, not words.

Context windows are measured in **tokens**, not characters.

Prompt costs are calculated using **tokens**, not pages or word counts.

Ultimately, the model never "sees" my original text.

It only sees the sequence of tokens produced by the tokenizer.

---

# Key Takeaways

* Tokens are the basic units processed by language models.
* Tokens are neither words nor characters.
* Modern LLMs typically use subword tokenization.
* Byte Pair Encoding (BPE) learns frequent text fragments and reuses them efficiently.
* Character count and token count are only loosely related.
* Different models may tokenize the same text differently.
* Tokenization affects context windows, cost, speed and retrieval quality.

---

> *"The model doesn't read English. It reads tokens."*

That single idea changed how I think about prompts, context windows and the entire LLM pipeline.
