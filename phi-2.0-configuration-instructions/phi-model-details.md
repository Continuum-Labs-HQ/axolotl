# Phi - Model Details

## <mark style="color:blue;">Phi 2.0 Model Details</mark>

This is the documentation for fine tuning the Phi 2.0 model using small datasets

### <mark style="color:blue;">Model Summary</mark>

* **Phi-2 Description**: It's a 2.7 billion parameter Transformer model trained with various NLP synthetic texts and filtered websites. It's designed to address common sense, language understanding, and logical reasoning.
* **Intention**: The model is not fine-tuned with reinforcement learning from human feedback. It is intended for research, especially in safety challenges like reducing toxicity, understanding biases, etc.
* **Formats**: Phi-2 is optimized for QA format, chat format, and code format.&#x20;

#### <mark style="color:green;">Sample Code</mark>

* **Execution Modes**: Four modes are detailed, depending on whether you use CUDA or CPU and the floating-point precision (FP16 or FP32).
* **Recommended Usage**: A Python example is provided to demonstrate how to load and use the model, including tokenizing inputs and generating outputs.

#### <mark style="color:green;">Training</mark>

* **Architecture and Dataset**: Details about the Transformer architecture, dataset size, context length, and training tokens are provided.
* **Hardware and Software**: It mentions the use of 96xA100-80G GPUs and a 14-day training period. Software used includes PyTorch, DeepSpeed, and Flash-Attention.
* **License**: The model is released under the Microsoft Research License.

## <mark style="color:blue;">The configuration file</mark>

```yaml
base_model: microsoft/phi-1_5
model_type: AutoModelForCausalLM
tokenizer_type: AutoTokenizer
is_llama_derived_model: false
trust_remote_code: true

load_in_8bit: false
load_in_4bit: true
strict: false

datasets:
  - path: garage-bAInd/Open-Platypus
    type: alpaca

dataset_prepared_path:
val_set_size: 0.05
output_dir: ./phi-sft-out

sequence_len: 1024
sample_packing: false  # not CURRENTLY compatible with LoRAs
pad_to_sequence_len:

adapter: qlora
lora_model_dir:
lora_r: 64
lora_alpha: 32
lora_dropout: 0.05
lora_target_linear: true
lora_fan_in_fan_out:

wandb_project: phi
wandb_entity: continuum-labs
wandb_watch: true
wandb_name: training-run-1
wandb_log_model: true

gradient_accumulation_steps: 1
micro_batch_size: 1
num_epochs: 4
optimizer: adamw_torch
adam_beta2: 0.95
adam_epsilon: 0.00001
max_grad_norm: 1.0
lr_scheduler: cosine
learning_rate: 0.000003

train_on_inputs: false
group_by_length: true
bf16: true
fp16: false
tf32: true

gradient_checkpointing:
early_stopping_patience:
resume_from_checkpoint:
local_rank:
logging_steps: 1
xformers_attention:
flash_attention:

warmup_steps: 100
eval_steps: 0.05
save_steps:
debug:
deepspeed:
weight_decay: 0.1
fsdp:
fsdp_config:
resize_token_embeddings_to_32x: true
special_tokens:
  bos_token: "<|endoftext|>"
  eos_token: "<|endoftext|>"
  unk_token: "<|endoftext|>"
  pad_token: "<|endoftext|>"
```

<details>

<summary><mark style="color:green;">config.json file</mark></summary>

\
The provided configuration file appears to be for a language model based on the Phi architecture developed by Microsoft. Let's analyze the key components of this configuration file:

1. **Model Identifier**:
   * <mark style="color:yellow;">`_name_or_path`</mark><mark style="color:yellow;">:</mark> "microsoft/phi-2" indicates the model's unique identifier, likely used to fetch the model from a repository or to identify it within a system.
2. **Activation Function**:
   * <mark style="color:yellow;">`activation_function`</mark><mark style="color:yellow;">:</mark> "gelu\_new" suggests the use of a newer version of the Gaussian Error Linear Unit (GELU) activation function, which is common in transformer models.
3. **Architectures**:
   * <mark style="color:yellow;">`architectures`</mark>: \["PhiForCausalLM"] implies that this model is designed for a causal language modeling task, where the model predicts the next word in a sequence based on previous words.
4. **Attention Dropout**:
   * <mark style="color:yellow;">`attn_pdrop`</mark>: 0.0 indicates that there is no dropout applied to the attention weights. Dropout is typically used to prevent overfitting, but in this case, it seems to be disabled.
5. **Mapping to Configuration and Model Classes**:
   * <mark style="color:yellow;">`auto_map`</mark> specifies the mapping to custom configuration and model classes specific to the Phi architecture, ensuring that the right classes are used for this specific model type.
6. **Embedding Dropout**:
   * <mark style="color:yellow;">`embd_pdrop`</mark><mark style="color:yellow;">:</mark> 0.0, similar to `attn_pdrop`, suggests that dropout is not applied to the embeddings.
7. **Flash Attention and Rotary**:
   * <mark style="color:yellow;">`flash_attn`</mark><mark style="color:yellow;">:</mark> false and `flash_rotary`: false indicate that this model configuration does not use Flash Attention (a technique for fast attention calculation) or rotary embeddings.
8. **Dense Layer Fusion**:
   * <mark style="color:yellow;">`fused_dense`</mark><mark style="color:yellow;">:</mark> false implies that the dense layers in the transformer are not fused, which is an optimization technique for faster computation.
9. **Image Processor**:
   * <mark style="color:yellow;">`img_processor`</mark><mark style="color:yellow;">:</mark> null suggests that this model does not have an integrated image processor, indicating its focus on language tasks rather than multimodal tasks.
10. **Initializer Range**:
    * <mark style="color:yellow;">`initializer_range`</mark>: 0.02 defines the range for initializing model weights. This is a standard practice to start the training process from a reasonable state.
11. **Layer Normalization Epsilon**:
    * <mark style="color:yellow;">`layer_norm_epsilon`</mark><mark style="color:yellow;">:</mark> 1e-05 specifies a small epsilon value used in layer normalization to prevent division by zero.
12. **Model Type and Specifications**:
    * `model_type`: "phi-msft" identifies the specific type of model.
    * `n_embd`: 2560 signifies the size of the embedding layer.
    * `n_head`: 32 indicates the number of attention heads.
    * `n_layer`: 32 represents the number of transformer layers.
    * `n_positions`: 2048 specifies the maximum sequence length the model can handle.
    * `resid_pdrop`: 0.1 denotes the dropout rate for residual connections.
13. **Rotary Dimensions**:
    * `rotary_dim`: 32 suggests the use of rotary embeddings with the specified dimension.
14. **Word Embeddings**:
    * `tie_word_embeddings`: false indicates that the word embedding weights are not tied between the input and output, which is a common technique in some models to reduce the number of parameters.
15. **Model Precision and Transformers Version**:
    * `torch_dtype`: "float16" indicates that the model uses 16-bit floating-point precision, which is often used to reduce memory usage and increase speed.
    * `transformers_version`: "4.35.2" specifies the version of the Hugging Face Transformers library compatible with this configuration.
16. **Vocabulary Size**:
    * `vocab_size`: 51200 states the size of the vocabulary used by the model.

</details>

<details>

<summary><mark style="color:green;">configuration_phi.py</mark></summary>

\
The `configuration_phi.py` file you have is a part of the Phi 2.0 language model's implementation, specifically <mark style="color:yellow;">designed for setting up and customizing the model's configuration.</mark> Here's what you can do with this file:

1. **Understanding Model Configuration**:
   * Use this file to understand the configurable parameters of the Phi model. It provides insights into the model's architecture and the various options you can adjust.
2. **Customizing the Model**:
   * If you plan to use the Phi model for specific tasks, you can modify this configuration file to tweak the model parameters according to your requirements. For example, you could adjust the number of layers (`n_layer`), the number of attention heads (`n_head`), or the dropout rates (`attn_pdrop`, `embd_pdrop`, `resid_pdrop`).
3. **Model Initialization**:
   * When initializing the Phi model in your code, you can use this configuration class to set up the model. Typically, you would create an instance of the `PhiConfig` class with desired parameters and pass it to the model during initialization.
4. **Training and Fine-tuning**:
   * If you are training or fine-tuning the Phi model on a custom dataset, this configuration file becomes crucial. You can adjust the parameters to better suit the size and complexity of your dataset, which can impact the training efficiency and model performance.
5. **Integration with Transformers Library**:
   * If you are using the Hugging Face Transformers library, this configuration class can be used in conjunction with it. The Transformers library utilizes such configuration classes to standardize model setups across different model types.
6. **Educational Purposes**:
   * Even if you're not actively adjusting the model for a specific task, studying this configuration file can be educational. It helps in understanding how large language models are configured and what parameters are important.
7. **Model Experimentation**:
   * Experiment with different configurations to see how they affect the model's behavior and performance. This can be part of a larger process of model experimentation to find the optimal setup for your specific use case.

The `configuration_phi.py` file you've shared is a Python class definition for the configuration of the Phi 2.0 language model developed by Microsoft. This class, `PhiConfig`, inherits from `PretrainedConfig` provided by the Hugging Face Transformers library. Let's break down the key elements of this configuration class:

1. **Model Type**:
   * `model_type`: "phi-msft" identifies the type of model, specifically indicating it's a Phi model developed by Microsoft.
2. **Attribute Mapping**:
   * `attribute_map`: Maps specific configuration terms to their corresponding attributes in the model. For example, `max_position_embeddings` is mapped to `n_positions`.
3. **Configuration Initialization**:
   * The `__init__` method initializes the configuration with a set of parameters. These parameters define the architecture and behavior of the Phi model.
4. **Model Parameters**:
   * `vocab_size`: The size of the vocabulary used by the model.
   * `n_positions`: The maximum sequence length the model can handle.
   * `n_embd`: The size of the embedding layer.
   * `n_layer`: The number of transformer layers in the model.
   * `n_inner`: An optional parameter for the size of the inner layer of the model (used in some transformer architectures).
   * `n_head`: The number of attention heads.
   * `rotary_dim`: Specifies the dimension for rotary embeddings, which are used to enhance the model's understanding of relative positions within the sequence.
   * `activation_function`: Specifies the activation function used in the model, like GELU.
5. **Optimization and Regularization Techniques**:
   * `flash_attn`, `flash_rotary`, `fused_dense`: Flags to enable specific optimization techniques.
   * `attn_pdrop`, `embd_pdrop`, `resid_pdrop`: Dropout rates for attention, embeddings, and residual connections, respectively.
   * `layer_norm_epsilon`: A small epsilon value used in layer normalization.
   * `initializer_range`: The range used for initializing the model's weights.
6. **Vocabulary Size Padding**:
   * `pad_vocab_size_multiple`: Ensures the vocabulary size is a multiple of this value, likely for optimization purposes.
7. **Word Embeddings Tying**:
   * `tie_word_embeddings`: Indicates whether the word embedding weights are shared between the input and output layers.

This configuration file essentially outlines the structural and functional specifics of the Phi model. It allows for flexible initialization with various parameters, making it adaptable for different requirements or datasets. The Phi model, with its large number of parameters and advanced features like rotary embeddings and specialized activation functions, is likely a powerful tool for natural language processing tasks.

\


</details>
