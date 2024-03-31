# Model Configuration - General

### <mark style="color:blue;">Model Configuration</mark>

The first configuration block of the <mark style="color:yellow;">Axolotl YAML configuration file</mark> is 'model type'.  It comprises three main configurations.

1. base\_model
2. model\_type
3. tokenizer\_type

Below are a number of example model configurations for different neural language models supported by Axolotl.

<mark style="color:green;">Model Configuration example for Phi 2.0</mark>

```yaml
base_model: microsoft/phi-2
model_type: AutoModelForCausalLM
tokenizer_type: AutoTokenizer
```

<mark style="color:green;">Model Configuration example for Llama2</mark>

```yaml
base_model: NousResearch/Llama-2-7b-hf
model_type: LlamaForCausalLM
tokenizer_type: LlamaTokenizer
is_llama_derived_model: true
```

<mark style="color:green;">Model Configuration example for TinyLLama</mark>

```yaml
base_model: TinyLlama/TinyLlama-1.1B-intermediate-step-1431k-3T
model_type: LlamaForCausalLM
tokenizer_type: LlamaTokenizer
```

<mark style="color:green;">Model Configuration example for Code-LLama</mark>

```yaml
base_model: codellama/CodeLlama-7b-hf
model_type: LlamaForCausalLM
tokenizer_type: CodeLlamaTokenizer
```

The next step after determining the <mark style="color:yellow;">model type configurations</mark> is to configure that <mark style="color:blue;">data loading and processing parameters</mark>
