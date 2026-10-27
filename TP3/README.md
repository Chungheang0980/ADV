# Fine-Tuning LLMs with Unsloth

Lesson notes on using **Unsloth** to fine-tune large language models efficiently.

## Table of Contents

1. [Introduction to Unsloth](#1-introduction-to-unsloth)
2. [Installation Requirements](#2-installation-requirements)
3. [Recommended Installation Method](#3-recommended-installation-method)
4. [Customizable Chat Templates](#4-customizable-chat-templates)
5. [Benefits and LoRA Configuration](#5-benefits-and-lora-configuration)
6. [Fine-Tuning (Core Concept)](#6-fine-tuning-core-concept)
7. [Summary](#summary)

---

## 1. Introduction to Unsloth

Unsloth is a Python library that helps fine-tune large language models efficiently. It supports models such as **Llama-3, Mistral, Phi-4, and Gemma**.

**Why use Unsloth?**

- **Faster training:** optimized for efficiency.
- **Less memory usage:** about 70% reduction, so it works well on devices with limited GPU power.
- **High accuracy:** achieves state-of-the-art fine-tuning results.

---

## 2. Installation Requirements

Before installing Unsloth, make sure you have:

| Requirement | Details |
|---|---|
| **Operating system** | Linux, Windows, macOS, Google Colab, or Kaggle |
| **Python version** | 3.9 or later |
| **GPU** (optional, recommended) | NVIDIA CUDA GPUs give faster performance. A CPU also works but is slower. |
| **pip** | Make sure pip is up to date |

```bash
pip install --upgrade pip
```

---

## 3. Recommended Installation Method

**Install with pip (recommended):**

1. Open Terminal / Command Prompt.
2. Run the installation command:

   ```bash
   pip install unsloth
   ```

3. Verify the installation by running Python and importing Unsloth:

   ```python
   import unsloth
   print(unsloth.__version__)
   ```

### Common Error: Import Errors

**Problem:** `ModuleNotFoundError: No module named 'unsloth'`

**Solution:** Reinstall Unsloth and check your Python path:

```bash
pip uninstall unsloth
pip install unsloth
```

---

## 4. Customizable Chat Templates

Chat templates can be modified to fit different AI models. Example (Llama-3 template):

```python
chat_template = """<|begin_of_text|><|start_header_id|>system<|end_header_id|>

{SYSTEM}<|eot_id|><|start_header_id|>user<|end_header_id|>

{INPUT}<|eot_id|><|start_header_id|>assistant<|end_header_id|>

{OUTPUT}<|eot_id|>"""
```

**Key points:**

- Uses placeholders like `{SYSTEM}`, `{INPUT}`, and `{OUTPUT}`.
- Defines headers for the system, user, and assistant roles.
- Uses special tokens like `<|begin_of_text|>`, `<|eot_id|>`, `<|start_header_id|>`, and `<|end_header_id|>` for structured interactions.

---

## 5. Benefits and LoRA Configuration

**Benefits:**

- **Task-specific adaptation:** models improve accuracy in specialized areas.
- **Resource efficiency:** optimized training reduces GPU and memory usage.
- **Improved performance:** enhanced output relevance and precision.

**Code snippet:** configuring a vision model for fine-tuning with Unsloth.

```python
model = FastVisionModel.get_peft_model(
    model,
    finetune_vision_layers     = True,  # Set False if not finetuning vision part
    finetune_language_layers   = True,  # Set False if not finetuning language part
    finetune_attention_modules = True,  # Set False if not finetuning attention layers
    finetune_mlp_modules       = True,  # Set False if not finetuning MLP layers

    r = 16,            # The larger, the higher the accuracy, but might overfit
    lora_alpha = 16,   # Recommended alpha == r at least
    lora_dropout = 0,
    bias = "none",
    random_state = 3407,
    use_rslora = False,  # We support rank stabilized LoRA
    loftq_config = None, # And LoftQ
    # target_modules = "all-linear",  # Optional now! Can specify a list if needed
)
```

**Fine-tuning options:** vision layers, language layers, attention modules, and MLP modules (all `True` by default).

**LoRA parameters:**

| Parameter | Value | Meaning |
|---|---|---|
| `r` | 16 | Rank for fine-tuning. Larger means higher accuracy but may overfit. |
| `lora_alpha` | 16 | Recommended setting: at least equal to `r`. |
| `use_rslora` | False | Option for rank-stabilized LoRA support. |

---

## 6. Fine-Tuning (Core Concept)

**Fine-tuning** is a technique where a pretrained model is adapted to a new, specific task by continuing its training on a smaller, task-specific dataset. It leverages the knowledge learned from large-scale datasets and adjusts the model's parameters to improve performance on the new task.

**Workflow:**

```
Large corpus of data ──► LLM ──► Fine-tuning the model ──► Final Model
                                        ▲                       │
                          Task-specific dataset                 ▼
                                                  Ready for real-world applications
```

---

## Summary

Unsloth makes fine-tuning LLMs faster and lighter on memory. Install it with pip, customize chat templates and LoRA settings, and train a pretrained model on your own dataset for a specific task.
