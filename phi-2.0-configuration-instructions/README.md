---
cover: broken-reference
coverY: 0
---

# Phi 2.0 Configuration Instructions

### <mark style="color:blue;">Model Configuration</mark>

As highlighted, the first configuration block of the Axolotl configuration file is 'model type'.  It comprises three main configurations.

1. base\_model
2. model\_type
3. tokenizer\_type

```yaml
base_model: microsoft/phi-2
model_type: AutoModelForCausalLM
tokenizer_type: AutoTokenizer
```

AutokTokenizer

{% embed url="https://github.com/huggingface/transformers/blob/6e584070d4f86964c4268baed08a5a5da8f82633/src/transformers/models/auto/tokenization_auto.py#L646" %}





The next step after determining the model type configurations is to configure the <mark style="color:blue;">data loading and processing parameters</mark>
