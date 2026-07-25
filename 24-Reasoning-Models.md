# Reasoning Models

## Resource(s) Studied

* OpenAI Developers — *Reasoning Best Practices*  
  https://developers.openai.com/api/docs/guides/reasoning-best-practices

* Anthropic — *Claude Prompting Best Practices*  
  https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

* Google AI for Developers — *Gemini Thinking Models*  
  https://ai.google.dev/gemini-api/docs/thinking

---

# In One Sentence

Modern reasoning models are also Transformer-based language models, but they are designed to analyse a problem before generating an answer.

---

# Why This Topic?

Earlier in this journal, I compared the behaviour of leading AI models through practical experimentation.

**AI Models Comparative Exercise:**  
https://github.com/rashmichaudhary24/genai-learning-journal/blob/main/AI-Models-Comparative-Exercise.md

That exercise focused on **what** each model does well.

This chapter explains **why** those differences exist.

Although GPT-5, Claude Opus, Gemini 2.5 and other frontier models share the same underlying Transformer architecture, they differ in how they are trained, aligned, prompted and—most importantly—how much reasoning effort they apply before responding.

---

# What Is a Reasoning Model?

Earlier language models generally followed a straightforward pattern:

```text
Question

↓

Answer
```

Modern reasoning models devote additional computation to analysing the problem before producing the final response.

```text
Question

↓

Think

↓

Evaluate

↓

Revise (if needed)

↓

Answer
```

> **Note:** *"Think"* is a convenient shorthand. The model is not conscious or self-aware; it performs additional computation to analyse the problem before generating a response.

Unlike earlier models, which often responded immediately, reasoning models can spend additional time exploring alternatives, checking assumptions and refining their answer before producing the final output.

---

# Reasoning Is Not a Different Architecture

One of the biggest misconceptions is that reasoning models are built using a fundamentally different architecture.

They are not.

GPT-5, Claude Opus and Gemini 2.5 are still Transformer-based Large Language Models that predict the next token.

What has changed is **how inference is performed**.

Instead of immediately producing an answer, these models can allocate additional computation to difficult problems before deciding what to generate next.

Reasoning models are therefore better understood as an evolution in **how** language models solve problems rather than an entirely new type of AI.

---

# Why Different Models Behave Differently

If several models share the same Transformer architecture, why do they produce noticeably different responses?

Because every AI company optimises for different trade-offs.

These include:

* reasoning effort
* response speed (latency)
* cost
* safety and alignment
* instruction following
* tool use
* multimodal capabilities
* long-context performance

As a result, two models may answer the same question differently—not because one is "smarter," but because they have been designed and optimised with different priorities.

---

# Dynamic Reasoning

Modern reasoning models do not apply the same amount of reasoning to every question.

Instead, they adjust their reasoning effort according to the complexity of the task.

Simple questions may receive an almost immediate response.

More challenging problems—such as mathematical proofs, software design or multi-step planning—trigger additional reasoning before an answer is generated.

This helps balance accuracy, latency and computational cost.

---

# Where Reasoning Models Excel

Reasoning models are particularly effective at tasks that require analysis rather than simple recall.

Examples include:

* resolving ambiguous or incomplete instructions
* extracting relevant information from large amounts of unstructured text
* identifying relationships across multiple documents
* applying nuanced policies and rules
* multistep planning and agentic workflows
* reviewing and improving code
* visual reasoning over charts, diagrams and images
* evaluating responses produced by other models

Many of these tasks involve combining evidence, identifying patterns or making decisions rather than simply retrieving facts.

---

# Prompting Reasoning Models

Although OpenAI, Anthropic and Google provide different guidance, their recommendations converge on several common principles.

* Keep prompts clear and direct.
* State the desired outcome explicitly.
* Specify important constraints.
* Use structured prompts with headings or delimiters where appropriate.
* Start with zero-shot prompting before introducing examples.
* Avoid unnecessary instructions such as "Think step by step," since modern reasoning models already perform internal reasoning.

In general, modern reasoning models require **better problem definitions**, not more complicated prompts.

---

# One Insight That Stood Out

I initially assumed that reasoning models represented a completely new type of AI.

They do not.

They are still language models predicting one token after another.

The difference lies in **how much computation they devote to solving a problem before deciding which tokens to generate.**

That seemingly small change explains why modern frontier models often produce significantly better results on complex reasoning tasks.

---

# Common Misconceptions

❌ Reasoning models use a completely different architecture.

❌ Reasoning models simply know more facts.

❌ Asking a model to "think step by step" always improves performance.

❌ All reasoning models behave in the same way.

---

# How This Changes the Way I Think About AI

Understanding reasoning models explains why GPT-5, Claude Opus, Gemini 2.5 and similar models often produce different responses to the same prompt.

The differences are not solely due to training data.

They also reflect different design choices regarding reasoning effort, safety, instruction following, tool use and optimisation goals.

Rather than asking:

> **Which model is the best?**

it is often more useful to ask:

> **Which model has been optimised for this task?**

---

# Key Takeaways

* Reasoning models are still Transformer-based language models.
* They spend additional computation analysing complex problems before responding.
* Modern models dynamically adjust their reasoning effort according to task complexity.
* Different AI companies optimise different trade-offs, resulting in distinct model behaviour.
* Stronger reasoning does not necessarily imply greater knowledge.
* Clear objectives and well-defined constraints are generally more effective than elaborate prompting techniques.

---

> *"Reasoning models don't think differently because they know more—they think differently because they spend more effort deciding how to use what they know."*
