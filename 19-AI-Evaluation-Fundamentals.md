# AI Evaluation Fundamentals

## Resources Studied

* Pinecone — *Evaluating RAG Systems*
* OpenAI Cookbook — *Evaluation Best Practices*

---

# What Is an Evaluation?

An **evaluation (eval)** is a systematic way to measure the quality of an AI model or AI system.

Given:

* an input,
* a generated output,
* and a desired outcome,

we determine how well the system performed.

The key insight is:

> There is no single "AI accuracy score." The appropriate evaluation depends entirely on what part of the system we are trying to evaluate.

---

# The Three Levels of AI Evaluation

## 1. Retrieval Evaluation

This evaluates whether the system retrieved the correct information.

Questions:

* Did we retrieve the right documents?
* Did we retrieve enough documents?
* Did we rank them correctly?

Examples:

* Precision
* Recall
* F1
* Precision@k
* Recall@k
* Mean Reciprocal Rank (MRR)
* Average Precision
* nDCG

Mental model:

> Did we fetch the right evidence?

---

## 2. Generation Evaluation

This evaluates the quality of the model's answer.

Questions:

* Is the answer factually correct?
* Is it grounded in the retrieved information?
* Is it relevant to the question?
* Did the model hallucinate?

Examples:

* Accuracy
* Groundedness/Faithfulness
* Relevance
* Hallucination rate

Mental model:

> Did we use the evidence correctly?

---

## 3. End-to-End System Evaluation

This evaluates the usefulness of the entire AI system.

Questions:

* Was the answer helpful?
* Did the user accomplish their task?
* Can users trust the system?
* Would they use it again?

Examples:

* User satisfaction
* Task completion
* Reliability
* Trust scores

Mental model:

> Did we solve the user's problem?

---

# How OpenAI Evals Work

An eval is essentially a test.

The process is:

1. Provide an input.
2. Generate an output.
3. Compare the output against expected behavior.

There are two broad ways to grade outputs.

## Rule-Based Evaluation

We write validation logic ourselves.

Examples:

* Exact match
* Regex matching
* JSON schema validation
* String comparison
* Programmatic assertions

Mental model:

> The computer checks the answer.

---

## Model-Graded Evaluation

This is a two-stage process:

### Stage 1

The model generates an answer.

### Stage 2

A model (often another LLM) evaluates that answer.

The evaluator checks things like:

* correctness,
* relevance,
* completeness,
* factuality,
* safety.

Mental model:

> We ask an AI to judge another AI.

---

# OpenAI Eval Templates

OpenAI broadly provides:

## Basic Eval Templates

Used when correctness can be checked programmatically.

Examples:

* Exact answers
* Classification tasks
* Structured outputs

---

## Model-Graded Templates

Used when correctness requires judgment.

Examples:

* Essay evaluation
* Summarization quality
* Helpfulness
* Groundedness
* Relevance

---

# Retrieval Evaluation

Retrieval evaluation originates from the field of Information Retrieval (IR).

The two fundamental questions are:

## Question 1

> Did we retrieve the right information?

## Question 2

> Did we retrieve the information in the right order?

This gives rise to two families of metrics.

---

# Category 1: Order-Unaware Metrics

These metrics only care whether relevant information was retrieved.

They do not care about ranking.

Example:

User asks:

> "How do I apply for maternity leave?"

The user only cares whether the correct policy documents were retrieved, not whether they appeared first or third.

---

## Precision

Question:

> Of everything we retrieved, how much was actually relevant?

Mental model:

> Precision = Accuracy of retrieval

High precision means:

* few irrelevant documents,
* high quality retrieval.

---

## Recall

Question:

> Of all relevant documents that existed, how many did we retrieve?

Mental model:

> Recall = Coverage

High recall means:

* we found most of the important information,
* we missed very little.

---

## F1 Score

The F1 score balances precision and recall.

Mental model:

> F1 = Overall retrieval quality

A good F1 score means:

* we found enough information,
* without retrieving too much irrelevant information.

---

# Category 2: Order-Aware Metrics

Sometimes ranking matters.

Suppose the correct answer exists but appears as result number 400.

Technically the system succeeded.

Practically the system failed.

Order-aware metrics measure ranking quality.

---

## Precision@k

Question:

> Of the first k results, how many were relevant?

Mental model:

> How good are my first few results?

Useful when:

* users only examine the first page of results,
* user attention is limited.

---

## Recall@k

Question:

> Of all relevant documents, how many appeared in the first k results?

Mental model:

> How much useful information did I find quickly?

Useful when:

* missing information is expensive.

---

## Mean Reciprocal Rank (MRR)

Question:

> How quickly did I find the first good answer?

MRR rewards systems that place the first correct answer very close to the top.

Mental model:

> How quickly did I strike gold?

Useful when:

* users typically need one correct answer.

Examples:

* customer support,
* enterprise search,
* question answering systems.

---

## Average Precision (AP)

Question:

> How consistently did I retrieve relevant documents throughout the ranking?

Unlike MRR:

* MRR cares only about the first correct result.
* Average Precision cares about all correct results.

Mental model:

> Did I keep finding useful information throughout the search results?

Useful when:

* multiple relevant answers matter.

---

## Discounted Cumulative Gain (DCG)

Sometimes relevance is not binary.

Examples:

* highly relevant,
* moderately relevant,
* slightly relevant.

DCG rewards:

* retrieving useful documents,
* placing the most useful ones near the top.

Mental model:

> Did I rank documents according to their usefulness?

---

## Normalized Discounted Cumulative Gain (nDCG)

nDCG compares your ranking with the ideal ranking.

Mental model:

> How close was my ranking to the perfect ranking?

nDCG is one of the most widely used ranking metrics in retrieval systems.

---

# Binary Relevance

Many retrieval metrics assume that documents are either:

* relevant, or
* not relevant.

This assumption is called **binary relevance**.

Metrics based on binary relevance include:

* Precision
* Recall
* F1
* Precision@k
* Recall@k
* MRR
* Average Precision

Metrics like nDCG allow multiple levels of relevance.

---

# Evaluation Dimensions in RAG Systems

| Question                                      | Evaluation Dimension |
| --------------------------------------------- | -------------------- |
| Did we retrieve the right information?        | Retrieval quality    |
| Did the answer use the retrieved information? | Grounding            |
| Is the answer factually correct?              | Accuracy             |
| Is the answer relevant?                       | Relevance            |
| Did the model hallucinate?                    | Hallucination rate   |
| Was the answer helpful?                       | User satisfaction    |
| Can we trust the system?                      | Reliability          |

---

# Mental Models / Analogies

| Metric             | Mental Model                                  |
| ------------------ | --------------------------------------------- |
| Precision          | Did I retrieve correct things?                |
| Recall             | Did I retrieve enough correct things?         |
| F1                 | Did I balance quality and coverage?           |
| Precision@k        | Are my top results good?                      |
| Recall@k           | Did I find enough useful information quickly? |
| MRR                | How quickly did I strike gold?                |
| Average Precision  | Did I keep finding useful results?            |
| nDCG               | Did I rank by usefulness?                     |
| Grounding          | Did the model show its work?                  |
| Hallucination Rate | How often did the model make things up?       |
| Reliability        | Can I trust this repeatedly?                  |

---

# What Surprised Me

* AI evaluation is not one problem but many different problems.
* There is no universal "best metric."
* Retrieval quality and answer quality are separate evaluations.
* A system can retrieve perfectly and still generate poor answers.
* MRR and Average Precision can give very different judgments of the same retrieval system.
* Modern AI evaluation increasingly uses models themselves as evaluators.

---

# Enterprise Implications

## Precision@k

Best when:

* reviewing irrelevant information is expensive,
* user attention is limited,
* quality matters more than quantity.

Examples:

* enterprise search,
* customer support.

---

## Recall@k

Best when:

* missing information is costly.

Examples:

* legal search,
* compliance,
* medical retrieval.

---

## F1

Best when:

* both missing information and retrieving irrelevant information are costly.

---

## MRR

Best when:

* users need one good answer quickly.

Examples:

* chatbots,
* help desks,
* search assistants.

---

## Average Precision

Best when:

* users benefit from multiple relevant answers.

Examples:

* research,
* discovery,
* recommendation systems.

---

## nDCG

Best when:

* some answers are more useful than others.

Examples:

* ranking systems,
* search engines,
* recommender systems.

---

# Questions I Still Have

* How do enterprises create ground-truth datasets?
* How is hallucination measured objectively?
* How reliable are LLM judges compared with humans?
* Which metrics matter most for AI agents?
* How frequently should evaluation datasets be updated?
* How do teams balance retrieval quality against generation quality?

---

# Personal Reflection

Before learning about evaluation, I assumed that a good answer meant a good AI system.

I now understand that evaluation depends entirely on what we are trying to measure. Retrieval quality, generation quality, grounding, and user satisfaction are all separate dimensions of performance.

The most useful takeaway for me is:

> "It depends on what we're evaluating."

That sentence has become a mental model for understanding almost every discussion about AI system performance.
