# Large Language Models

## Resource(s) Studied

* IBM Think – *What Are Large Language Models?*

## What I Learned

* The primary difference between traditional language models and Large Language Models (LLMs) is scale, including both the number of parameters and the amount of training data.
* Transformers represented a major breakthrough compared with earlier architectures such as recurrent neural networks (RNNs) because their self-attention mechanism enables them to capture relationships between tokens while allowing computations to be performed in parallel. Self-attention figures out what the sentence means; next-token prediction uses that understanding to guess what comes next. 
* Embeddings convert text into numerical vector representations that capture semantic and syntactic relationships.
* Self-supervised learning creates training labels automatically from unlabeled data, allowing models to learn without requiring human annotation.
* LLMs sometimes produce hallucinations because they generate statistically probable outputs rather than verifying factual accuracy.
* Fine-tuning involves further training a pretrained model on a smaller, task-specific dataset to adapt it to particular domains or applications.
* Parameters are learned numerical values that determine how a model processes inputs and generates outputs.

### Fine-tuning

* Specializes a pretrained model for a specific domain or task.
* Improves performance on relevant applications.
* Does not eliminate hallucinations.

### Hallucinations

* Arise because the model generates statistically likely outputs.
* Reflect limitations of pattern prediction rather than deliberate fabrication.

### Self-supervised Learning vs Supervised Learning

In supervised learning, the computer is explicitly provided with the correct answers during training. These answers are known as labels or ground truth.

LLMs, however, are initially trained using self-supervised learning. This approach begins with unlabeled data and automatically creates training tasks from that data itself. Because the correct answers can be derived from the training data, no human labeling is required.

During training, the model compares its predictions with these automatically generated targets, making the process resemble supervised learning despite the absence of manually provided labels.

### Parallelization

Parallelization means performing many computations simultaneously rather than sequentially.

When people say:

> "Transformers are highly parallelizable,"

they mean that many computations can be performed at the same time, allowing training and inference to occur much faster and enabling models to scale to billions of parameters.

In plain English:

> Parallelization means dividing work among many workers so that several tasks can happen simultaneously.

This contrasts with recurrent neural networks (RNNs), which process information sequentially.

For example:

* In an RNN, word 4 must wait for word 3, which must wait for word 2, which must wait for word 1.
* In a Transformer, all positions can be processed simultaneously because each position can access all other positions through self-attention.

### From Tokens to Attention

LLMs do not process words directly.

Instead:

1. Input text is tokenized.
2. Each token is converted into an embedding vector.
3. Each embedding is transformed into three vectors:

   * Query
   * Key
   * Value
4. Queries are compared with keys to determine attention weights.
5. These weights are used to combine the value vectors.
6. The resulting weighted combination becomes the updated representation of the token.

In simplified terms:

* Query: "Who should I pay attention to?"
* Key: "How relevant am I to others?"
* Value: "What information do I contribute if someone pays attention to me?"

## Concepts Encountered

* Large Language Models (LLMs)
* Parameters
* Tokens
* Embeddings
* Self-attention
* Transformers
* Self-supervised learning
* Fine-tuning
* Hallucinations
* Parallelization
* Recurrent Neural Networks (RNNs)
* Query, Key, and Value vectors
* Scale

## Mental Models / Analogies

One analogy that helped me understand embeddings was:

> An embedding is like the coordinates of a point in a high-dimensional space.

Words and concepts that are semantically similar occupy nearby regions of this space, allowing the model to capture relationships between them mathematically.

## What Surprised Me

Several ideas challenged my assumptions:

* Transformers owe much of their success not only to self-attention but also to their ability to perform computations in parallel.
* Self-supervised learning creates its own training labels from unlabeled data.
* Fine-tuning improves domain performance but does not eliminate hallucinations.
* LLMs do not process words directly; they process tokens, which are then converted into embeddings.
* The same underlying mechanisms that allow LLMs to understand grammar and facts also enable them to infer subtle concepts such as sarcasm and irony.

## Enterprise Implications

Although larger models often demonstrate greater capabilities, scale alone does not determine performance.

Enterprise AI outcomes also depend on:

* model architecture,
* quality and quantity of training data,
* fine-tuning,
* alignment methods,
* inference settings,
* evaluation frameworks,
* and business context.

This suggests that organizations should evaluate AI systems holistically rather than assuming that larger models automatically produce better business outcomes.

## Questions I Still Have

* How are embeddings and tokens related?
* How do billions of parameters collectively encode useful knowledge?
* How do transformer architectures enable capabilities that appear far more sophisticated than simple next-token prediction?

## Personal Reflection

One realization I found particularly fascinating was that ChatGPT does not possess a separate "sarcasm detector."

Instead, it uses the same mechanisms it uses for all language understanding:

* examining tokens,
* analyzing context,
* identifying patterns learned during training,
* and estimating the most probable interpretation.

This made me appreciate how many apparently distinct cognitive abilities may emerge from a surprisingly small set of underlying mechanisms.

I also noticed something interesting about my own interests. The parts of AI that I found most engaging were hallucinations, jailbreaks, prompt injection attacks, and security vulnerabilities. This suggests that I may be naturally drawn toward the governance, safety, and risk management aspects of AI rather than purely technical implementation details.

## Key Takeaway

> Large Language Models exhibit remarkably sophisticated behavior through the seemingly simple process of predicting the next token.
