# Training vs. Inference

## Resources Studied

- Andrej Karpathy – *Large Language Models Explained*
- Jay Alammar – *The Illustrated Transformer*
- NVIDIA – *What's the Difference Between Deep Learning Training and Inference?*
- Google Developers – *Intro to Inference*

---

One of the biggest realisations was that **training** and **inference** are not two different models or two different architectures. They are two different phases in the life of the same model.

The Transformer architecture remains unchanged throughout. What changes is whether the model is still learning.

---

## Training

Training is the process through which a model learns its parameters, commonly called **weights**.

During training, the model repeatedly processes examples from a dataset, makes predictions, compares those predictions with the expected outputs, measures the error, and updates its weights to reduce future error.

This cycle is repeated over enormous datasets for many iterations until the model gradually learns statistical patterns present in the data.

Once training is complete, the learned weights become the model's knowledge.

---

## Inference

Inference begins after training has finished.

Instead of learning from data, the model now applies its learned weights to generate outputs for previously unseen inputs.

When a prompt is submitted, the model performs a forward pass through the network, predicts the next token, appends it to the sequence, and repeats the process until the response is complete.

Unlike training, inference does **not** modify the model's weights.

The model is using what it has already learned rather than learning something new.

---

## The Fundamental Difference

The distinction between training and inference can be summarised in one sentence:

> **Training changes the model. Inference uses the model.**

Everything else follows from this distinction.

| Training | Inference |
|----------|-----------|
| Learns from data | Applies learned knowledge |
| Updates weights | Uses fixed weights |
| Requires forward and backward passes | Requires only a forward pass |
| Optimises model parameters | Generates predictions |
| Happens during model development | Happens whenever the model is used |

---

## Forward Pass and Backward Pass

One idea that finally clicked today was the difference between the forward and backward passes.

A **forward pass** is simply the movement of information through the network to produce an output.

This happens during both training and inference.

A **backward pass** happens only during training.

After the model makes a prediction, the prediction error is propagated backwards through the network so that the weights can be adjusted.

This process is called **backpropagation**.

In other words:

- **Training = Forward Pass + Backward Pass + Weight Updates**
- **Inference = Forward Pass**

---

## Why Training Is Expensive

Training is computationally expensive because learning requires far more computation than simply generating predictions.

In addition to performing a forward pass, the model must:

- calculate prediction errors,
- compute gradients,
- perform backpropagation,
- update billions of weights, and
- repeat this process across enormous datasets for many iterations.

Modern foundation models therefore require large GPU clusters and can take weeks or even months to train.

---

## Why Inference Is Comparatively Cheap

Inference is comparatively cheaper because the learning phase has already been completed.

The model no longer needs to calculate gradients, perform backpropagation, or update its parameters.

Instead, it simply performs a forward pass using the learned weights to predict one token after another.

Although inference is still computationally intensive—especially for very large models—it requires significantly less computation than training.

---

## Where Fine-Tuning Fits

Fine-tuning is not a separate phase.

It is simply another form of training.

Instead of learning from scratch, a pretrained model is trained further on a smaller, task-specific dataset so that it becomes better suited for a particular domain or application.

Since the model's weights continue to change, fine-tuning remains part of the training phase.

---

## Common Misconceptions

### **Inference means the model is still learning**

It is easy to assume that a model becomes smarter every time someone interacts with it. In reality, inference does not update the model's weights. The model simply applies what it learned during training to generate a response.

---

### **Training and inference use different models**

Training and inference are two phases in the lifecycle of the same model. The architecture remains the same; only the objective changes. During training, the model learns by updating its weights. During inference, it uses those learned weights to make predictions.

---

### **Inference is computationally free**

Inference is significantly less computationally expensive than training, but it is not free. Every response still requires the model to perform a forward pass through billions of parameters. Larger models and longer prompts therefore require more computational resources than smaller models and shorter prompts.

---

## Key Takeaways

- Training and inference are two phases in the lifecycle of the same model.
- During training, the model learns by updating its weights.
- During inference, the model uses its learned weights to generate predictions.
- A forward pass occurs during both training and inference.
- A backward pass and backpropagation occur only during training.
- Training is computationally expensive because it involves repeated prediction, error calculation, backpropagation, and weight updates across massive datasets.
- Inference is comparatively cheaper because it only requires a forward pass using fixed weights.

---

## Questions I Still Have

- How are billions of weights initially assigned before training begins?
- How does backpropagation determine exactly which weights should be updated and by how much?
- How are learning rates chosen, and what happens if they are too high or too low?
- How do GPUs accelerate training compared to CPUs?
- Why do some models require weeks or months to train while others can be fine-tuned in a few hours?
- What techniques make inference faster and less expensive without significantly reducing model quality?
