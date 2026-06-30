# Open Source AI

## Resource(s) Studied

- ✅ IBM Think – *What Is Open Source AI?*

---

## What I Learned

### What is Open Source AI?

Open-source AI refers to AI systems that can be used, examined, modified, and redistributed without requiring permission.

Unlike traditional software, open-source AI extends beyond source code and may include:

- Model architecture
- Model weights
- Training methodology
- Data processing pipelines
- Inference code
- Documentation about training data

The goal is to enable transparency, reproducibility, and collaborative innovation.

---

### Open Source AI vs Open Source Software

Traditional open-source software primarily requires access to source code.

Open-source AI introduces additional components that may need to be disclosed:

- Training data descriptions
- Model weights
- Training pipelines
- Fine-tuning procedures
- Evaluation methods

This makes open-source AI substantially more complex than traditional open-source software.

---

### Open Weights vs Open Source AI

One of the most important distinctions I learned was that:

**Open weights does not necessarily mean open source.**

Open-weight models provide access to trained model parameters but may keep private:

- Training datasets
- Data processing pipelines
- Reinforcement learning procedures
- Training infrastructure
- Safety and alignment methods

Fully open-source AI attempts to expose the entire development process.

---

### Why Open Source AI Matters

The emergence of generative AI accelerated the open-source movement significantly.

According to IBM, approximately two-thirds of large language models released in 2023 were open source or open weight models.

This has accelerated:

- Innovation
- Experimentation
- Research
- Enterprise adoption
- Community collaboration

---

## Key Concepts Encountered

- Open Source AI
- Open Weights
- Open Source vs Open Weights
- Model Weights
- Attention Weights
- Models vs Frameworks
- Enterprise AI
- Transparency
- Reproducibility
- Fine-tuning

---

## Mental Models / Analogies

### Model Weights ≠ Attention Weights

#### Model Weights

- Learned during training
- Persistent
- Billions of parameters
- Represent the model's knowledge

**Mental model:**
> Model weights are the brain.

#### Attention Weights

- Computed dynamically
- Temporary
- Different for every prompt
- Determine what the model focuses on at a given moment

**Mental model:**
> Attention weights are attention.

---

### Models ≠ Frameworks

| Models | Frameworks |
|---------|------------|
| GPT | PyTorch |
| Llama | TensorFlow |
| Mistral | LangChain |
| Claude | Haystack |

**Mental model:**

> A model is what reasons.
>
> A framework is what helps build, train, or use it.

---

### Open Weights ≠ Open Source

Traditional software intuition suggests:
