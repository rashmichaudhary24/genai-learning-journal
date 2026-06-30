# Introduction to Large Language Models

## Resource(s) Studied

* Andrej Karpathy – *Intro to Large Language Models*

## What I Learned

* Large Language Models (LLMs) fundamentally operate by predicting the next token in a sequence.
* This apparently simple objective—next-token prediction—gives rise to surprisingly sophisticated capabilities.
* LLMs are trained on massive amounts of text, including books, websites, articles, code repositories, and other digital content.
* LLMs learn statistical patterns in data rather than facts, beliefs, or human-like understanding.
* Modern LLMs became possible because of the transformer architecture.
* The behavior of an LLM emerges from learning patterns across enormous amounts of data and adjusting billions of parameters.
* Despite their capabilities, LLMs remain susceptible to hallucinations, prompt injection attacks, jailbreaks, and data poisoning.

## Concepts Encountered

* Large Language Models (LLMs)
* Next-token prediction
* Transformers
* Parameters
* Lossy compression
* Hallucinations
* Prompt injection
* Jailbreaks
* Data poisoning
* Tool use
* Agentic AI

## Mental Models / Analogies

One of the most helpful mental models presented in the lecture was the idea that:

> An LLM is a lossy compression of the Internet.

To understand this, I imagined reading 10,000 books and then destroying them.

All that remains is me.

I would not be able to reproduce every sentence from every book. However, I would have internalized:

* concepts,
* patterns,
* vocabulary,
* styles,
* and some factual knowledge.

In this sense, I myself would become a lossy compression of the books I had read.

This analogy helped me understand why LLMs can generate coherent and knowledgeable responses while simultaneously forgetting details and sometimes hallucinating.

## What Surprised Me

I was surprised to learn that merely providing an LLM with external tools such as calculators or Python libraries does not automatically make it an agentic AI system.

An LLM with access to tools may exhibit some agentic characteristics, but fully agentic AI systems typically also involve:

* planning,
* memory,
* autonomous decision-making,
* and the ability to execute multi-step workflows.

This made me realize that "AI agents" represent a broader architectural concept than simply "LLMs with tools."

## Enterprise Implications

The idea of LLMs as lossy compression has important implications for enterprise adoption.

Because LLMs learn patterns rather than store exact knowledge:

* hallucinations are inevitable,
* outputs require validation,
* governance mechanisms become essential,
* and human oversight remains important.

This reinforces the importance of responsible AI practices, evaluation frameworks, and enterprise governance structures.

## Questions I Still Have

* At what point does an LLM-based system become an AI agent?
* How do reasoning models differ from standard next-token prediction models?
* How do transformer architectures enable capabilities that appear far more sophisticated than simple next-token prediction?

## Personal Reflection

One thing I found particularly interesting was that my favorite sections of the lecture involved jailbreaks, prompt injection attacks, and security vulnerabilities.

This made me realize that I am naturally drawn toward the governance, safety, and risk management aspects of AI rather than purely technical implementation details.

That observation may have implications for the kinds of AI roles and domains that I ultimately find most engaging.

## Key Takeaway

> Large Language Models perform the astonishing task of generating human-like capabilities through the seemingly simple process of predicting the next token.
