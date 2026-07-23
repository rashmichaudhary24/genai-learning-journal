# Training vs. Inference

## Resource(s) Studied

- Andrej Karpathy – *Large Language Models: LLMs Explained*
- Jay Alammar – *The Illustrated Transformer*
- NVIDIA – *What's the Difference Between Deep Learning Training and Inference?*
- Google Developers – *Intro to Inference*

---

## Learning Objectives

After completing this note, you should be able to:

- distinguish between training and inference
- explain why training is significantly more computationally expensive than inference
- differentiate between the forward and backward passes
- explain where fine-tuning fits into the model lifecycle

---

## Introduction

A large language model operates in two distinct phases:

1. **Training**, during which the model learns its parameters (weights) from data.
2. **Inference**, during which the trained model applies those learned parameters to generate predictions for previously unseen inputs.

Although both phases use the same neural network architecture, they serve fundamentally different purposes. The key distinction is whether the model's parameters are being **updated**.

---

## Training vs. Inference

| Training | Inference |
|----------|-----------|
| Learns from data | Applies learned knowledge |
| Updates model weights | Uses fixed model weights |
| Requires forward and backward passes | Requires only a forward pass |
| Optimises model parameters | Generates predictions |
| Performed occasionally | Performed every time the model is used |
| Computationally expensive | Comparatively inexpensive |

---

## Training

Training is the process through which a model learns statistical patterns from large datasets.

For each training example, the model:

1. performs a forward pass to generate a prediction,
2. compares that prediction with the expected output,
3. calculates the prediction error (loss),
4. propagates that error backwards through the network, and
5. updates its weights to reduce future error.

This process is repeated across enormous datasets for many iterations until the model converges on a set of weights that generalise well to unseen data.

Training determines **what the model knows**.

---

## Inference

Inference is the process of using a trained model to generate outputs for new inputs.

When a user submits a prompt:

1. the prompt is processed by the model,
2. the model performs a forward pass using its learned weights,
3. probability scores are computed for possible next tokens,
4. one token is selected,
5. the process repeats until the response is complete.

Unlike training, inference does **not** modify the model's parameters.

Inference determines **how the model applies what it has already learned**.

---

## Why Training Is Expensive

Training is computationally intensive because it requires much more than simply generating predictions.

During training, the system must:

- process enormous datasets repeatedly,
- compute prediction errors,
- calculate gradients,
- store intermediate activations,
- perform backpropagation, and
- update billions of parameters.

These operations require substantial GPU memory, compute capacity, and time.

Modern foundation models are therefore trained using large GPU clusters over weeks or even months.

---

## Why Inference Is Comparatively Cheap

Once training has finished, the model's parameters remain fixed.

Inference therefore avoids several expensive operations:

- no gradient computation,
- no backpropagation,
- no weight updates,
- no optimisation step.

The model simply performs a forward pass to predict the next token.

Although inference still requires considerable computation—especially for large models—it is significantly less demanding than training because learning is no longer taking place.

---

## Forward Pass vs. Backward Pass

The distinction between training and inference can be understood in terms of the computations performed.

### Forward Pass

The input moves through the neural network to produce an output.

Occurs during:

- Training
- Inference

### Backward Pass

The prediction error is propagated backwards through the network to determine how the model's weights should be updated.

Occurs during:

- Training only

Consequently,

- **Training = Forward Pass + Backward Pass + Weight Updates**
- **Inference = Forward Pass**

---

## Fine-Tuning

Fine-tuning is a specialised form of training performed after pre-training.

Instead of learning from scratch, an existing model is trained further on a smaller, task-specific dataset so that it performs better for a particular domain or application.

The underlying process remains training because the model's parameters continue to be updated.

---

## Key Takeaways

- Training and inference use the same model architecture but serve different purposes.
- Training learns model parameters; inference applies them.
- Training updates weights; inference keeps them fixed.
- Training requires both forward and backward passes.
- Inference requires only a forward pass.
- Fine-tuning is an additional stage of training rather than a separate process.
