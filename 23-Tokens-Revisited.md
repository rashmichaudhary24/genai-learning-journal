# Tokens Revisited

## Resource(s) Studied

* OpenAI Tokenizer  
  https://platform.openai.com/tokenizer

* Jay Alammar — *The Illustrated GPT-2*  
  https://jalammar.github.io/illustrated-gpt2/

* Hugging Face NLP Course — *Tokenization*  
  https://huggingface.co/learn/nlp-course/chapter6/1

* OpenAI Cookbook — *How to Count Tokens with tiktoken*  
  https://cookbook.openai.com/examples/how_to_count_tokens_with_tiktoken
---

# In One Sentence

Language models perform mathematical operations, not linguistic ones. Tokenization is the step that converts human-readable text into a representation the model can compute on.

---

# Why Do We Need Tokens?

Text
   ↓
Tokenizer
   ↓
Tokens
   ↓
Token IDs
   ↓
Embeddings
   ↓
Positional Encoding
   ↓
Attention Mechanism
   ↓
LLM Output

Computers cannot reason over raw text directly.

Tokenization converts text into manageable pieces that can be assigned numerical IDs and represented as vectors (embeddings).

These token embeddings then become the inputs processed by the Transformer's attention mechanism.

In other words, tokens form the bridge between human language and mathematical computation.

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

The examples below illustrate how token count depends far more on the tokenizer's learned vocabulary than on the number of characters.

| Text | Example Tokenization | Number of Tokens | Number of Characters | Why? |
|------|----------------------|-----------------:|---------------------:|------|
| hippopotomonstrosesquippedaliophobia | `[hip] [pop] [ot] [omon] [st] [ros] [es] [qu] [ipped] [ali] [ophobia]` | 11 | 36 | Long word |
| Hello | `[Hello]` | 1 | 5 | Common word |
| Hello! | `[Hello] [!]` | 2 | 6 | Punctuation separated |
| Disproportionate Engorgement | `[Dis] [pro] [portion] [ate] [ Eng] [org] [ement]` | 7 | 28 | Rare phrase |
| Artificial Intelligence | `[Artificial] [ Intelligence]` | 2 | 23 | Common phrase |
| William Shakespeare | `[William] [ Shakespeare]` | 2 | 19 | Extremely common phrase in training data |
| Donald Trump | `[Donald] [ Trump]` | 2 | 12 | Famous name |
| Prem Kumar | `[Prem] [ Kumar]` | 2 | 10 | Common name |
| Anubha Budhalakoti | `[An] [ub] [ha] [ Bud] [hal] [ak] [oti]` | 7 | 18 | Rare name |
| RashmiChaudhary24 | `[R] [ash] [mi] [Ch] [aud] [h] [ary] [24]` | 8 | 17 | Rare name + digits |
| ₹25,00,000 | `[₹] [25] [,] [00] [,] [000]` | 6 | 10 | Symbols and commas |
| 🤖 | *(varies by tokenizer)* | 2 | 2 | One visible character ≠ one token |

> **Note:** These token boundaries are illustrative and are based on one tokenizer. Different models may split the same text differently.
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
