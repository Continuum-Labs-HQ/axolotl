---
description: Formats and Customizations
---

# Types of Dataset Structures

### <mark style="color:blue;">Axolotl Dataset Formats and Customisation</mark>

Axolotl is versatile in handling various dataset formats.  Below are some of the formats you can use, with JSONL being the recommended format:

1. <mark style="color:green;">**Alpaca Format**</mark><mark style="color:green;">:</mark>
   * Structure: <mark style="color:yellow;">`{"instruction": "your_instruction", "input": "optional_input", "output": "expected_output"}`</mark>
   * Ideal for scenarios where you need to <mark style="color:yellow;">p</mark>_<mark style="color:yellow;">**rovide specific instructions along with optional input data.**</mark>_ The output field holds the expected result. This format is particularly useful for guided learning tasks.
2. <mark style="color:green;">**ShareGPT Format**</mark><mark style="color:green;">:</mark>
   * Structure: <mark style="color:yellow;">`{"conversations": [{"from": "human/gpt", "value": "dialogue_text"}]}`</mark>
   * This format suits conversational models where _<mark style="color:yellow;">**interactions are between a human and a GPT-like model.**</mark>_ It helps in training models to understand and respond in a dialogue setting, reflecting real-world conversational flows.
3. <mark style="color:green;">**Completion Format**</mark><mark style="color:green;">:</mark>
   * Structure: <mark style="color:yellow;">`{"text": "your_text_data"}`</mark>
   * The completion format is straightforward and best for training models on raw text corpora.  It's ideal for scenarios where the model needs to learn from unstructured text without specific instructions or dialogue contexts.

### <mark style="color:blue;">**Adding Custom Prompts**</mark>

For datasets preprocessed with instruction-focused tasks:

* Structure: <mark style="color:yellow;">`{"instruction": "your_instruction", "output": "expected_output"}`</mark>
* This format supports a direct instructional approach, where the model is trained to follow specific commands or requests. It's effective for task-oriented models.

Incorporating this into your YAML configuration:

```yaml
datasets:
  - path: repo
    type:
      system_prompt: ""
      field_system: system
      format: "[INST] {instruction} [/INST]"
      no_input_format: "[INST] {instruction} [/INST]"
```

This YAML config allows for a flexible setup, enabling the model to interpret and learn from the structured instructional format.

### <mark style="color:blue;">**Custom Pre-tokenized Dataset Usage**</mark>

To use a custom pre-tokenized dataset:

* Do not specify a <mark style="color:yellow;">`type`</mark> in your configuration.
* Ensure your dataset columns are precisely named as <mark style="color:yellow;">`input_ids`</mark><mark style="color:yellow;">,</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`attention_mask`</mark>, and <mark style="color:yellow;">`labels`</mark><mark style="color:yellow;">.</mark>

This approach is beneficial <mark style="color:blue;">when you have a dataset that is already tokenized</mark> and ready for model consumption. It skips additional preprocessing steps, streamlining the training process for efficiency.

### <mark style="color:blue;">Interesting Points Regarding Datasets</mark>

* <mark style="color:purple;">**Format Flexibility**</mark><mark style="color:purple;">:</mark> Axolotl’s support for multiple formats allows for training models on diverse data types - from structured instructional data to informal conversational dialogues.
* <mark style="color:purple;">**Customisability**</mark><mark style="color:purple;">:</mark> The ability to customise datasets and their integration into the system via YAML configurations provides a high degree of control over the training process, allowing for fine-tuning specific to the desired output of the model.
* <mark style="color:purple;">**Efficiency in Pre-tokenized Data**</mark><mark style="color:purple;">:</mark> The support for pre-tokenized datasets is a significant time-saver, particularly in scenarios where datasets are vast and tokenization can become a computationally expensive step.

This variety and customizability make Axolotl a robust tool for training language models across different scenarios and requirements, enhancing its versatility in AI model development.
