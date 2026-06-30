# Foundation Models

## Resource(s) Studied

* IBM Think – *What Are Foundation Models?*
* Kate Soule – *How to Build Enterprise-Ready Foundation Models*

## What I Learned

### What are Foundation Models?

Foundation models are large AI models trained on massive and diverse datasets that can perform a wide variety of general-purpose tasks.

Unlike traditional machine learning models, which are typically developed for a single task, foundation models act as a reusable base that can be adapted to numerous downstream applications through prompting or fine-tuning.

Examples include:

* GPT
* Claude
* Gemini
* Llama
* Mistral

### How Foundation Models are Built

The development of foundation models typically involves:

1. **Data collection**

   * Large, mostly unlabeled datasets are gathered.
   * Data may include text, images, audio, video, and code.

2. **Choice of modality**

   * Unimodal models process one type of data.
   * Multimodal models process multiple data types.

3. **Model architecture**

   * Most modern foundation models are based on transformer architectures.
   * Some image-generation models use diffusion architectures.

4. **Training**

   * Models are trained using self-supervised learning.
   * Regularization techniques help prevent overfitting.

5. **Evaluation**

   * Standardized benchmarks are used to assess and improve performance.

### Adapting Foundation Models

Foundation models can be adapted in two major ways:

#### Fine-tuning

* Continues training on a smaller, domain-specific dataset.
* Updates the model's parameters.
* Specializes the model for particular tasks or industries.

#### Prompting

* Uses instructions or examples to guide behavior.
* Does not modify the model's parameters.
* Relies on in-context learning.

## Concepts Encountered

* Foundation Models
* Transfer Learning
* Enterprise AI
* Fine-tuning
* Prompting
* Self-supervised Learning
* Multimodal Models
* Transformers
* Diffusion Models
* Enterprise Deployment
* Responsible AI
* Governance
* Foundation Model Lifecycle

## Mental Models / Analogies

One analogy that helped me understand foundation models was:

### Engine vs Car

```text
Foundation Models
-----------------

GPT
Claude
Gemini
Llama
Mistral

        ↓

Applications
------------

ChatGPT
Claude App
Gemini App
Copilot
Perplexity
```

A foundation model is like an engine.

Applications are the vehicles built using that engine.

This helped me understand why ChatGPT is not itself a foundation model, but rather an application built on top of one.

## What Surprised Me

Several aspects of foundation models surprised me:

* Foundation models inherit biases present in their training data.
* Building foundation models requires enormous computational resources.
* Organizations often derive more value from adapting existing foundation models than from building their own.
* The distinction between foundation models and applications built on top of them is more important than I had initially realized.

## Enterprise Implications

Foundation models offer organizations several advantages:

### Benefits

* Faster time-to-value by avoiding expensive pre-training.
* Access to strong baseline capabilities.
* Lower development costs compared with building models from scratch.
* Adaptability across multiple business domains.

### Enterprise Use Cases

* Natural language processing
* Code generation
* Computer vision
* Healthcare applications
* Robotics
* Knowledge management
* Enterprise search

### Challenges

Organizations must also address:

* Bias
* Hallucinations
* Privacy and intellectual property concerns
* Computational costs
* Environmental impact
* Governance and regulatory requirements

## Questions I Still Have

* At what point does it become economically viable for an organization to build its own foundation model?
* How do enterprises decide between using closed models and open-source foundation models?
* How are foundation models evaluated for enterprise readiness?

## Personal Reflection

I particularly enjoyed Kate Soule's presentation because it focused on enterprise reality rather than model internals.

While Andrej Karpathy was essentially asking:

> "How do these systems work?"

Kate Soule was asking:

> "How do organizations actually build, deploy, govern, and derive value from these systems?"

This made me realize that I am naturally drawn toward the organizational, strategic, and governance dimensions of AI rather than purely technical implementation details.

## Key Takeaway

> Foundation models are not applications. They are reusable, adaptable platforms upon which applications, workflows, and enterprise AI systems can be built.
