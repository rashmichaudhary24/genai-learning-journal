# What are Tokens?

## Resource(s) Studied

* OpenAI Help – *What are tokens and how to count them?*
* OpenAI Tokenizer Tool – https://platform.openai.com/tokenizer

## What I Learned

* Large Language Models (LLMs) do not process text as words or sentences but as tokens, which are chunks of text optimized for computational efficiency.
* A token is distinct from a token ID (the numerical identifier assigned to a token) and from the token count (the total number of tokens processed).
* Tokenization depends on the frequency of character sequences in the training corpus rather than on word length or semantic meaning.
* Common text sequences, including spaces and punctuation (e.g., " red" versus "red"), may receive different token IDs.
* Token counts influence the cost and performance of AI models.
* Reasoning models may perform additional internal computation ("reasoning tokens") while reducing the amount of user interaction required to complete a task.
* More capable models may require fewer user-visible instructions because they can leverage prior knowledge and perform additional internal reasoning.
* A corpus refers to the collection of data used to train or study language models; the corpus itself is not stored directly in the model.
* A string is a sequence of characters that serves as the input to the tokenization process.
* The conceptual processing pipeline of an LLM can be understood as:

> String → Tokens → Token IDs → Model Processing

## Concepts Encountered

* Token
* Tokenization
* Token ID
* Token Count
* Input Tokens
* Output Tokens
* Cached Tokens
* Reasoning Tokens
* Prompt Engineering
* Corpus Data
* String
* Reasoning Models
* Internal Computation
* Tokenizer

## What Surprised Me

That names, depending on how common they are in the training corpus, may have different token counts:

* Rashmi Chaudhary → 6 tokens
* Ruchi Sharma → 3 tokens

Similarly, words of comparable length can have different token counts:

* There → 1 token
* Plasma → 2 tokens
* Xylem → 3 tokens

## Enterprise Implications

* Token usage directly affects AI operating costs. Organizations adopting Generative AI must understand token consumption to accurately forecast budgets and optimize usage.
* Prompt quality has both performance and financial implications. Concise, well-structured prompts can improve outcomes while reducing token expenditure.
* More capable AI models may require less explicit user instruction because they can leverage prior knowledge and perform more effective internal reasoning.
* Token efficiency may become an important optimization metric for enterprise AI applications because it affects cost, latency, and scalability.

## Questions I Still Have

* Why do different models have different token counts?
* How do context windows actually work?
* How do embeddings and tokenization relate?

## Personal Reflection

One line from the article confused me:

> "Some reasoning models may use more tokens internally but aim to improve efficiency by reducing the number of tokens needed per completed task."

I struggled with this idea because it seemed intuitive that accomplishing a task should require a certain minimum amount of information. How, then, could a model perform the same task with less information?

The answer clicked when I thought about expertise.

Suppose someone tells me:

> "Boil the spaghetti until al dente, then toss it with olive oil, basil, garlic, and Parmesan."

I immediately understand what spaghetti, basil, Parmesan, and "al dente" mean because I already possess the necessary background knowledge.

My grandmother, however, might ask:

> "What's spaghetti?"
>
> "What's basil?"
>
> "What's Parmesan?"
>
> "What does al dente mean?"

The amount of information required to cook the dish hasn't changed. What has changed is how much information needs to be communicated explicitly.

This helped me understand why reasoning models may perform more internal computation while requiring less user interaction and fewer user-visible tokens.

### Key takeaway

> Expertise doesn't reduce the amount of information needed to solve a problem; it reduces the amount of information that needs to be explained.

Or, in AI terms:

> Reasoning models don't necessarily need less information—they often need less conversation.
