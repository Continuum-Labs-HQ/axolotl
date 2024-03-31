# Phi 2.0 Training Configuration

```yaml
accelerate launch -m axolotl.cli.train examples/phi/phi-qlora.yml
```

To execute the main training script Axolotl provides this command:

```yaml
datasets:
  - path: axolotl/know_medical_dialogue_v2/know_med_v4.json
    type: alpaca
    ds_type: json
dataset_prepared_path:
val_set_size: 0.05
output_dir: ./phi-sft-out
```

```bash
Success! Preprocessed data path: `dataset_prepared_path: ./llama-data`
```

The output should indicate success:

{% code fullWidth="false" %}
```bash
python -m axolotl.cli.preprocess examples/phi/phi-qlora.yml
```
{% endcode %}

Once you have configured the dataset component of the YAML file, then execute the following command which uses the <mark style="color:yellow;">preprocess.py script</mark> within the Axolotl library. &#x20;

To set up the preprocessing command, find the <mark style="color:yellow;">path to your dataset</mark> in VS Code by right clicking on the dataset and asking for the relative path.  Use this in the command below.  <mark style="color:yellow;">Remember to include the file name.</mark>

### <mark style="color:green;">Training Phi 2.0</mark>

To execute the main training script Axolotl provides this command to begin training Phi 2.0

```bash
accelerate launch -m axolotl.cli.train examples/phi/phi2-ft.yml
```

### <mark style="color:green;">LLama2</mark>

```bash
accelerate launch -m axolotl.cli.train examples/llama-2/lora.yml
```

If you have not already done so, you will be asked to enter your Weights and Biases API Key.&#x20;

&#x20;Enter the key at the command line prompt:

```yaml
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### <mark style="color:red;">Issues that arose (ignore)</mark>

We had a problem with dependencies - what a surprise

<details>

<summary><mark style="color:green;">What are xformers?</mark></summary>

The GitHub repository for xFormers, as described in the provided text, offers a comprehensive overview of the library and its functionalities. Here's an analysis of the key points:

#### Overview of xFormers:

1. **Customizable Building Blocks**:
   * xFormers provides <mark style="color:yellow;">domain-agnostic components for Transformers</mark>, usable in various fields like vision and NLP, without requiring extensive boilerplate code.
2. **Research-Oriented**:
   * The library contains cutting-edge components not yet available in mainstream libraries, indicating its focus on the latest developments in Transformer technology.
3. **Efficiency**:
   * Designed with speed and memory efficiency in mind, xFormers includes custom CUDA kernels and utilizes other libraries when appropriate.

#### Installation:

1. **Stable Versions**:
   * Recommended installation via conda or pip, depending on the environment (Linux or Windows) and CUDA version (11.8 or 12.1).
   * Specific to PyTorch versions 1.13.1, 2.0.1, or <mark style="color:yellow;">2.1.0.</mark>
2. **Development Binaries**:
   * For users who want to access the latest development features.
3. **Source Installation**:
   * An option for compatibility with different or nightly versions of PyTorch.
   * Additional steps like installing `ninja` for faster builds and setting the `TORCH_CUDA_ARCH_LIST` environment variable are suggested.

#### Key Components:

1. **Functional Operators and Components**:
   * The repository is organized into directories like `ops`, `components`, `benchmarks`, and `triton`. Each contains specific functionalities like attention mechanisms, feedforward blocks, positional embeddings, etc.
2. **Attention Mechanisms and More**:
   * xFormers offers a variety of attention mechanisms, feedforward styles, positional embeddings, and other Transformer components.
3. **Optimized Building Blocks**:
   * Includes memory-efficient attention mechanisms and various optimized operations, indicating a focus on performance.

#### Benchmarks and Testing:

* Benchmarks for memory-efficient multi-head attention (MHA) and other components are provided.
* Instructions for testing the installation and verifying available kernels are included.

#### Hackability and Extensibility:

* xFormers is designed to be hackable with composable building blocks, making it adaptable for research and development.
* It uses Triton for some optimized parts, which are explicit and accessible, indicating ease of customization.

#### Install Troubleshooting:

* The document provides troubleshooting tips for installation issues, like ensuring NVCC and CUDA runtime compatibility and setting the correct environment variables.

</details>

The setup.py script deals with issues between Xformers and Pytorch

<details>

<summary><mark style="color:green;">XFormers and Pytorch</mark></summary>

The setup.py script indicates a temporary workaround for a compatibility issue with `xformers`. If `torch==2.1.0` is in the requirements, the <mark style="color:yellow;">standard</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`xformers`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">dependency is removed and replaced with a specific version</mark> installed directly from the GitHub repository. This suggests that the <mark style="color:yellow;">current release of</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`xformers`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">does not support Torch 2.1.0</mark> and requires using the main branch from the GitHub repo.

The special handling of `xformers` in `setup.py` suggests that the version of `xformers` compatible with `torch==2.1.0` <mark style="color:yellow;">is not available in the standard Python package index</mark> (PyPI). Therefore, the script directly installs `xformers` from the main branch of its GitHub repository.

This approach indicates that the Axolotl platform is using features or fixes from `xformers` that are only available in the latest code and have not yet been released officially.

Users of Axolotl need to be aware that they are using a potentially unstable or untested version of `xformers`, which might have implications for production use.

</details>

### <mark style="color:blue;">An analysis of the axolotl.clt.train module</mark>

<details>

<summary><mark style="color:green;">Analysis of train.py script</mark></summary>

The <mark style="color:yellow;">`train.py`</mark> script in the Axolotl platform is a Command Line Interface (CLI) tool designed for training machine learning models.&#x20;

This script is structured to provide a user-friendly interface for configuring and executing model training. Here's a detailed analysis:

#### <mark style="color:blue;">Script Structure and Functionality</mark>

<mark style="color:green;">**Imports and Logger Setup**</mark>

* Essential modules like `logging`, `pathlib.Path`, `fire`, and `transformers` are imported.
* The script sets up a logger `LOG` using the `logging` module for logging various events and statuses during the script's execution.

<mark style="color:green;">**do\_cli Function**</mark>

* <mark style="color:blue;">**Function Definition**</mark><mark style="color:blue;">:</mark> The <mark style="color:yellow;">`do_cli`</mark> function is the main entry point of the script. It accepts a <mark style="color:yellow;">`config`</mark> argument (with a default value pointing to an "examples" directory) and `**kwargs` for additional arguments.
* <mark style="color:blue;">**ASCII Art Display**</mark><mark style="color:blue;">:</mark> <mark style="color:yellow;">`print_axolotl_text_art()`</mark> is called to display ASCII art, likely for aesthetic purposes.
* <mark style="color:blue;">**Configuration Loading**</mark><mark style="color:blue;">:</mark> <mark style="color:yellow;">`load_cfg`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">l</mark>oads configuration details from the provided `config` path. These configurations are essential for setting up model training parameters.
* <mark style="color:blue;">**Accelerator and User Token Checks**</mark><mark style="color:blue;">:</mark> The script verifies the default configuration for the accelerator (such as a GPU) and checks the user token. These checks are crucial for ensuring that the hardware is correctly set up and the user is authenticated.
* <mark style="color:blue;">**CLI Arguments Parsing**</mark><mark style="color:blue;">:</mark> It uses <mark style="color:yellow;">`transformers.HfArgumentParser`</mark> to parse additional CLI arguments into data classes (<mark style="color:yellow;">`TrainerCliArgs`</mark>). This step allows for dynamic customization of training parameters via the command line.
* <mark style="color:blue;">**Dataset Loading**</mark><mark style="color:blue;">:</mark> <mark style="color:yellow;">`load_datasets`</mark> is called with the parsed configuration and CLI arguments. This function is responsible for loading the dataset as per the configuration, which is a critical step in the training process.
* <mark style="color:blue;">**Model Training**</mark><mark style="color:blue;">:</mark> The <mark style="color:yellow;">`train`</mark> function is invoked with the loaded configuration, CLI arguments, and dataset metadata. This function likely encompasses the core logic for model training.

<mark style="color:green;">**Main Block**</mark>

* The script checks if it's being run as the main program <mark style="color:yellow;">(</mark><mark style="color:yellow;">`__name__ == "__main__"`</mark><mark style="color:yellow;">)</mark> and not as a module in another script. If it's the main program, it uses <mark style="color:yellow;">`fire.Fire(do_cli)`</mark> to execute the <mark style="color:yellow;">`do_cli`</mark> function, enabling the script to be interacted with from the command line.

</details>

