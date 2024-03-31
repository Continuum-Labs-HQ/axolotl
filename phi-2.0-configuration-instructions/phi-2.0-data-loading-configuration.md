---
cover: broken-reference
coverY: 0
---

# Phi 2.0 - Data Loading Configuration

With the model configured, we next have to determine whether whether we will be using quantization in the training process.

&#x20;The first configuration is whether we will be <mark style="color:blue;">**training the model**</mark> using the Lora or QLora technique - that is training the model with **4 or 8 bit quantization.**

**We will be using the **<mark style="color:yellow;">**Lora Parameter Efficient Fine Tuning Technique**</mark>

### <mark style="color:blue;">Model Configuration</mark>

The first configuration block of the Axolotl configuration file is 'model type'.  It comprises three main configurations.

1. base\_model
2. model\_type
3. tokenizer\_type

```yaml
load_in_8bit: true
load_in_4bit: false
strict: false
```

### <mark style="color:blue;">load\_in\_8bit: true or false</mark>

This is configuration flag that determines <mark style="color:yellow;">whether the model should be loaded in</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**8-bit precision.**</mark>  If it is set to "true," the model will be loaded in 8-bit precision.

<mark style="color:blue;">**Memory Efficiency:**</mark> 8-bit precision reduces the memory footprint of the model compared to higher precision formats (like 16-bit or 32-bit). This is because it requires less memory to store each weight in the model.

Loading a model in 8-bit precision can accelerate model loading and inference times. This is due to the reduced computational load compared to higher precision formats.

While 8-bit precision is more efficient, it can slightly reduce the accuracy of the model compared to full precision (32-bit). This happens because of the reduced resolution in representing the weights and activations.

### <mark style="color:blue;">load\_in\_4bit: true or false</mark>

This is configuration flag that determines whether the model should be loaded in **4-bit precision**.  If it is set to "true," the model will be loaded in 4-bit precision.

4-bit precision takes the concept of memory efficiency further, halving the memory requirements compared to 8-bit. This can be crucial for deploying large models on limited hardware.

Similar to 8-bit, 4-bit precision can lead to even faster loading and inference times due to the further reduced computational requirements.

The trade-off in accuracy might be more pronounced in 4-bit precision. The reduced bit-depth means that the model's ability to represent nuanced information in weights and activations is more limited. This might affect tasks that require high precision or are sensitive to small changes in weights.

### <mark style="color:blue;">strict: true or false</mark>

#### Strict Mode (strict)

* If set to false, default weights will be chosen where missing in adapters.  This is a component of 'bits and bytes' library

<details>

<summary><mark style="color:green;">What is 'bits and bytes'?</mark></summary>

**Overview**

The <mark style="color:yellow;">`bitsandbytes`</mark> repository provides a lightweight wrapper around CUDA custom functions, primarily focusing on 8-bit optimizers, matrix multiplication <mark style="color:yellow;">(</mark><mark style="color:yellow;">`LLM.int8()`</mark><mark style="color:yellow;">),</mark> and quantization functions. This tool is designed to enhance the performance and efficiency of machine learning models, particularly in the context of CUDA-enabled computing environments.

**Key Features**

* **8-bit Optimizers**: Specialized for reducing memory usage and improving computational efficiency.
* **Matrix Multiplication (LLM.int8())**: Offers optimized matrix multiplication capabilities.
* **Quantization Functions**: Includes various methods for quantizing models, contributing to reduced model sizes and potentially faster inference times.

**Requirements**

* Python version 3.8 or higher.
* Linux distribution (Ubuntu, MacOS, etc.) with CUDA version greater than 10.0.
* Note: CUDA 10.0 is deprecated, and future support is focused on CUDA >= 11.0 with release 0.39.0.

**Installation**

* Installable via pip (`pip install bitsandbytes`).
* In cases where compilation from source is necessary, users are encouraged to submit a bug report and follow the provided compilation instructions.

**Usage Highlights**

* **Int8 Inference with HuggingFace Transformers**: Allows models to load in 8-bit for reduced memory usage.
* **8-bit Optimizer Usage**: Users can easily switch to 8-bit optimizers by replacing their existing optimizers with the corresponding 8-bit version from `bitsandbytes`.
* **Mixed 8-bit Training and Int8 Inference**: The library supports both mixed 8-bit training with 16-bit main weights and full 8-bit inference.

**Features**

* Advanced techniques for 8-bit matrix multiplication and LLM.int8() inference.
* A range of 8-bit optimizers including Adam, AdamW, RMSProp, LARS, LAMB, and Lion.
* A stable embedding layer feature for improved stability in NLP models.
* Fast and efficient algorithms for quantile estimation.

**Requirements & Hardware Compatibility**

* Requires Anaconda, cudatoolkit, and PyTorch.
* Compatible with NVIDIA GPUs, specifically Turing or newer for LLM.int8(), and Kepler or newer for 8-bit optimizers and quantization.
* Supports CUDA versions from 10.2 to 12.0.
* Note: The library is currently supported only on Linux distributions.

**Additional Information**

* The repository includes instructions for users of Fairseq, detailing how to implement the Stable Embedding Layer and use the optimizers.
* A section on troubleshooting common errors and solutions is provided.
* The repository also contains detailed instructions for compiling from source if necessary.

**Licensing**

* The majority of `bitsandbytes` is under the MIT license, with some portions (like Pytorch) under different licenses.

**Community Contributions**

* Acknowledgment to Fabio Cannizzo for his work on FastBinarySearch, used for CPU quantization in the project.

</details>

<details>

<summary><mark style="color:green;">Summary of Tim Detmers' Presentation on 8-Bit Methods for Efficient Deep Learning</mark></summary>

His main thesis is that computationally efficient methods will accelerate progress in understanding deep learning.

<mark style="color:green;">**Key Points from Tim's Presentation**</mark>

**8-Bit Methods for Large Models**: Tim highlights the importance of making large models more accessible through quantization, which <mark style="color:yellow;">reduces the memory footprint.</mark>

**Quantization Explained**: He explains quantization as a process of <mark style="color:yellow;">converting floating-point or real representations into discrete buckets</mark>, akin to histogram binning.

**Linear vs. Nonlinear Quantization**: <mark style="color:yellow;">Linear (integer) quantization involves equally wide bins, while nonlinear quantization allows varying bin widths</mark>.

**Error Reduction in Quantization**: Tim illustrates how the <mark style="color:yellow;">choice of bins impacts precision and error distribution in quantized values.</mark>

**4-Bit Inference**: His recent work shows that <mark style="color:yellow;">4-bit inference is highly effective for large transformers</mark>.

**Floating Point Data Types**: The presentation delves into the structure of floating point data types, explaining the roles of exponent bits and fraction bits.

**Dynamic Exponent Data Type**: Tim introduces a <mark style="color:yellow;">unique data type he developed with a dynamic exponent</mark>, which offers flexibility in approximating large and small values with varying precision.

**8-Bit Optimizers**: The focus shifts to 8-bit optimizers, crucial for memory efficiency in training large models, particularly in language modeling.

Tim discusses <mark style="color:yellow;">reducing memory usage by approximately 40% by converting 32-bit Adam optimizer buffers to 8-bit.</mark>

This reduction is significant as it helps make large models more memory-efficient.

<mark style="color:yellow;">Outliers in Adam optimizer buffers cause issues in quantization</mark>, leading to increased error and ineffective 8-bit quantization.

Tim presents an example showing how <mark style="color:yellow;">outliers can skew the data</mark>, leading to a waste of bits and loss of effective representation.

To address the problem of outliers, Tim <mark style="color:yellow;">proposes chunking Adam states into blocks and quantizing each block independently</mark>.

This method isolates the impact of outliers to specific blocks, enhancing the stability of 8-bit optimizers.

The process involves <mark style="color:yellow;">chunking state into blocks</mark>, finding the maximum value for normalization, and storing the index for 8-bit representation.

This method ensures compact yet effective optimization, <mark style="color:yellow;">comparable to 32-bit optimizers</mark>.

This achievement indicates significant memory savings without compromising performance.

8-bit optimizers are efficient in mapping onto hardware, with the <mark style="color:yellow;">main overhead being the dequantization process.</mark>

<mark style="color:yellow;">Outliers become a significant problem in models larger than 6.7 billion parameters</mark>, causing performance drops.

Tim's research identifies <mark style="color:yellow;">systematic outliers that emerge with scale</mark> and become problematic at specific model sizes.

Outliers in large models exhibit systematic and emergent properties, affecting the same dimensions across layers.

These outliers impact all layers in a transformer model once a certain scale is reached.

The emergence of outliers follows an exponential trend, leading to a phase shift-like effect at a certain scale.

Understanding and addressing this exponential trend is key to managing outliers in large models.

A novel approach was developed to identify and process these outliers in 16-bit while handling the rest in 8-bit, effectively maintaining efficiency while addressing the problem.

<mark style="color:green;">**Efficiency of 8-Bit Matrix Multiplication**</mark>

* By applying this method, 99.9% of weights are computed in 8-bit, with a small portion in 16-bit for outliers. This approach achieves performance equivalent to 16-bit computations while halving memory size.
* This makes large models like Llama 65B accessible on consumer hardware, significantly lowering the barrier to entry for working with such models.

<mark style="color:green;">**Few-Shot and Zero-Shot Performance**</mark>

* The few-shot performance of models using 8-bit methods is comparable to 16-bit models. Tim highlighted a strong correlation between zero-shot performance and perplexity in language models, indicating that complexity evaluations can reliably predict zero-shot performance.

<mark style="color:green;">**Understanding Outliers in Transformer Models**</mark>

* Outliers tend to be concentrated in specific columns of the input batch and are more prevalent in larger models. These outliers are crucial for attention mechanisms in transformers.
* They are context-independent, aiding the attention mechanism in focusing on specific values by providing predictable patterns for the model to cancel out unnecessary information.

<mark style="color:green;">**Trade-Offs in Activation Functions**</mark>

* Replacing traditional activation functions like softmax with more stable alternatives can increase stability but may lead to a drop in performance.
* This presents a research challenge in balancing stability with maintaining or enhancing model performance.

<mark style="color:green;">**Impact of Precision and Parameter Count on Model Efficiency**</mark>

* An interesting finding is that models with the same number of bits but different distributions of precision and parameter count (e.g., 8-bit with more parameters vs. 4-bit with fewer parameters) exhibit the same inference latency.
* This equivalence in performance is due to the nature of GPU computations, where memory loading is significantly more costly than computation. Therefore, the memory used during inference, rather than the computational complexity, often dictates the performance.

</details>

## <mark style="color:green;">datasets</mark>

<pre class="language-yaml"><code class="lang-yaml"><strong>datasets:
</strong>  - path: datasets/alpaca-cleaned/alpaca_data_cleaned.json
    type: alpaca
    ds_type: json
    data_files:
  - alpaca_data_cleaned.json
dataset_prepared_path:
val_set_size: 0.20
output_dir: ./llama-out
</code></pre>

This component of the configuration file tells the platform where the dataset it located, and how the dataset should be split up into <mark style="color:yellow;">training versus validation.</mark>

We will only be using a number of these parameters for our fine tuning.  The full number of configurations can be found here:  [<mark style="color:orange;">**data loading and processing configurations**</mark>](broken-reference)

## <mark style="color:green;">fine tuning data set location</mark>

### <mark style="color:blue;">dataset\_prepared\_path:</mark>

This parameter indicates the <mark style="color:yellow;">path to a dataset that has been prepared for training</mark>.&#x20;

### <mark style="color:blue;">ds\_type:</mark>

Huggingface datasets can come in a number of formats.  You can configure the data loading process to take into account the data type - csv, json, parquet.   We will be using JSON format.

## <mark style="color:green;">validation Set</mark>

### <mark style="color:blue;">val\_set\_size: 0.20</mark>

**Description:** Specifies the <mark style="color:yellow;">size of the validation set as a percentage of the total dataset.</mark>

**Meaning:** This parameter determines the proportion of the dataset that will be used for validation during the training process. In this case, the default is set to 5% of the total dataset.

## <mark style="color:green;">output files</mark>

### <mark style="color:blue;">output\_dir: ./output</mark>

Description: Specifies the directory where <mark style="color:yellow;">output files should be saved</mark>.

Meaning: This parameter designates the directory where various output files, such as trained model checkpoints or logs, should be stored.
