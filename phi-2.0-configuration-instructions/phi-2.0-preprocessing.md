---
cover: broken-reference
coverY: 0
---

# Phi 2.0 - Preprocessing

To execute the training run, we will first <mark style="color:yellow;">preprocess the dataset.</mark>&#x20;

Axolotl allows us to optionally <mark style="color:blue;">pre-tokenize dataset</mark> before finetuning. This is recommended for large datasets.&#x20;

### <mark style="color:blue;">Populate the config.yaml file</mark>

To execute the preprocessing, we have to make sure the <mark style="color:yellow;">datasets component</mark> of the config.yaml is correctly populated. &#x20;

You will need to <mark style="color:yellow;">**direct Axolotl to where your dataset is**</mark>.

To do this, find the path to your dataset in VS Code by right clicking on the dataset and asking for the <mark style="color:yellow;">relative path.</mark> &#x20;

Then enter it into the <mark style="color:yellow;">**config YAML file**</mark> below which is located at:

### _your directory_/<mark style="color:blue;">axolotl</mark>/<mark style="color:green;">examples</mark>/<mark style="color:purple;">phi</mark>/<mark style="color:yellow;">phi2-ft.yml</mark>

```bash
your directory/axolotl/examples/phi/phi2-ft.yml
```

When you have located the file, then <mark style="color:yellow;">**populate the configuration file**</mark> below.

To do this, find the <mark style="color:yellow;">**path to your dataset**</mark> in VS Code by <mark style="color:green;">right clicking</mark> on the dataset and asking for the relative path. &#x20;

Use this in the command below.  <mark style="color:yellow;">Remember to</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**include the file name.**</mark>

```yaml
datasets:
  - path: datasets/alpaca-cleaned/alpaca_data_cleaned.json
    type: alpaca
        ds_type: json
    data_files:
    - alpaca_data_cleaned.json
dataset_prepared_path:
val_set_size: 0.20
output_dir: ./phi-out
```

The data set type (ds\_type) is JSON, and we have arbitrarily <mark style="color:yellow;">set the output directory as</mark> <mark style="color:blue;">./phi-out</mark>

For a refresher of what the alpaca-cleaned dataset contains:

<details>

<summary><mark style="color:green;">Alpaca Cleaned Dataset - Description</mark></summary>

The Alpaca dataset is a <mark style="color:yellow;">curated and cleaned version of an original dataset</mark> released by Stanford, specifically <mark style="color:yellow;">designed for instruction-tuning of language models</mark>.&#x20;

<mark style="color:green;">**Dataset Description and Improvements**</mark>

1. **Issues Addressed**:
   * <mark style="color:blue;">**Hallucinations**</mark><mark style="color:blue;">:</mark> The original dataset included instructions that led to irrelevant or fabricated responses by the model, particularly in cases where the input was a URL or an ambiguous prompt. These have been cleaned to prevent such issues.
   * <mark style="color:blue;">**Merged Instructions**</mark><mark style="color:blue;">:</mark> Instances where multiple instructions were combined have been separated for clarity and precision.
   * <mark style="color:blue;">**Empty Outputs**</mark><mark style="color:blue;">:</mark> Entries with no outputs have been addressed.
   * <mark style="color:blue;">**Missing Code Examples**</mark><mark style="color:blue;">:</mark> The cleaned dataset ensures that code examples are included where necessary.
   * <mark style="color:blue;">**Instructions for Image Generation**</mark><mark style="color:blue;">:</mark> Removed or modified instructions that required image generation, as this is not feasible for a text-based model.
   * <mark style="color:blue;">**N/A Outputs and Inconsistent Input Fields**</mark><mark style="color:blue;">:</mark> These issues have been standardised or corrected.
   * <mark style="color:blue;">**Incorrect Answers**</mark><mark style="color:blue;">:</mark> The dataset has been reviewed for accuracy, especially in areas like math problems where the original dataset had a high error rate.
   * <mark style="color:blue;">**Unclear Instructions**</mark><mark style="color:blue;">:</mark> Ambiguous instructions have been clarified or rewritten.
   * <mark style="color:blue;">**Extraneous Characters**</mark><mark style="color:blue;">:</mark> Removal of unnecessary escape and control characters.
2. **Original Alpaca Dataset Summary**:
   * The <mark style="color:yellow;">original dataset, Alpaca, contains 52,000 instruction examples</mark> created using OpenAI's `text-davinci-003` engine.
   * It was designed for instruction tuning, making language models better at following specific instructions.
   * The dataset was generated more cost-effectively and is more diverse compared to its predecessors.
3. **Dataset Structure**:
   * The dataset consists of fields like `instruction`, `input`, `output`, and `text`, which combine these elements in a format suitable for model fine-tuning.
   * The `input` field is optional and used when context is necessary for the instruction.
4. **Data Splits**:
   * <mark style="color:yellow;">The dataset contains 52,002 training examples.</mark>
5. **Usage and Applications**:
   * It is intended for instruction training of pre-trained language models, particularly in the text-generation domain.
6. **Languages**:
   * The dataset is exclusively in English.

</details>

Once you have configured the dataset component of the YAML file, then execute the following command which uses the <mark style="color:yellow;">preprocess.py script</mark> within the Axolotl library. &#x20;

{% code fullWidth="false" %}
```bash
python -m axolotl.cli.preprocess examples/phi/phi2-ft.yml
```
{% endcode %}

The output should indicate success:

```bash
Success! Preprocessed data path: `dataset_prepared_path: ./phi-out'
```

If you have not set a dataset\_prepared\_path in the configuration file, it will default to:

"preprocess CLI called without dataset\_prepared\_path set, using default path: <mark style="color:yellow;">last\_run\_prepared"</mark>

For an <mark style="color:yellow;">analysis of the output</mark> relating to the dataset preprocessing, see below:

<details>

<summary><mark style="color:green;">Analysis of Output from Pre-Processing</mark></summary>

The numbers:

1. **PID (Process ID)**: `6779`
   * This is the ID of the process running the script.
2. **Token IDs**:
   * End Of Sentence (EOS) Token ID: `2`
   * Beginning Of Sentence (BOS) Token ID: `1`
   * Padding (PAD) Token ID: `0`
   * Unknown (UNK) Token ID: `0`
3. **Data Downloading and Processing**:
   * Number of data files downloaded: `1`
   * Download speed: `12557.80 items/second`
   * Number of data files extracted: `1`
   * Extraction speed: `214.70 items/second`
4. **Dataset Generation**:
   * Number of examples in the train split: `51760`
   * Generation speed: `85351.57 examples/second`
5. **Mapping and Filtering**:
   * Number of examples processed in mapping (num\_proc=12): `51760`
   * Processing speed in mapping: `6035.04 examples/second`
   * Number of examples processed in filtering (num\_proc=12): `51760`
   * Filtering speed: `41994.96 examples/second`
   * Number of examples processed in the second mapping (num\_proc=12): `51760`
   * Second mapping speed: `30435.07 examples/second`
6. **Token Counts**:
   * Total number of tokens: `12104896`
   * Total number of supervised tokens: `8475133`
7. **Efficiency Estimates and Data Loading**:
   * Packing efficiency estimate: `1.0`
   * Total number of tokens per device: `12104896`
   * Data loader length: `1461`
   * Sample packing efficiency estimate across ranks: `0.9798729691644562`
   * Sample packing efficiency estimate: `0.98`
   * Total number of steps: `5844`
8. **Time and Date Information**:
   * Date and time of the log entries: `2023-12-06`
   * Times of various log entries: `05:24:22,428`, `05:24:22,688`, `05:24:32,282`, `05:24:36,028`, `05:24:36,393`, `05:24:41,028`, `05:24:41,029`, `05:24:41,037`
   * Total execution time: `26 seconds`
   * Time when the command prompt was ready again: `05:24:42`

</details>

If you would like information on how the preprocess.py script works you can view the code at   <mark style="color:purple;">axolotl</mark>/<mark style="color:green;">src</mark>/<mark style="color:blue;">axolotl</mark>/<mark style="color:yellow;">cli.</mark> &#x20;

Alternatively, take the time to read the analysis of the scripts, and the output it produced:

<details>

<summary><mark style="color:green;">Axolotl preprocess.py -</mark> <mark style="color:yellow;">analysis of script</mark> <mark style="color:green;">and</mark> <mark style="color:yellow;">command output</mark></summary>

The provided <mark style="color:yellow;">`preprocess.py`</mark> script is a <mark style="color:yellow;">command-line interface (CLI) tool</mark> for preprocessing datasets in the context of training models using the Axolotl platform.&#x20;

<mark style="color:green;">**Imports and Logger Setup**</mark><mark style="color:green;">:</mark>

* The script imports necessary modules such as <mark style="color:yellow;">`logging`</mark><mark style="color:yellow;">,</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`pathlib.Path`</mark> for file path operations, <mark style="color:yellow;">`fire`</mark> for the CLI, and several modules from <mark style="color:yellow;">`transformers`</mark> and <mark style="color:yellow;">`axolotl`</mark>.
* <mark style="color:yellow;">`colorama`</mark> is used for colored console output, enhancing readability.
* A logger `LOG` is set up for logging purposes, using the `logging` module.

<mark style="color:green;">**do\_cli Function**</mark><mark style="color:green;">:</mark>

<mark style="color:blue;">**Load Configurations**</mark>

The main function <mark style="color:green;">`do_cli`</mark> takes a `config` argument (with a <mark style="color:yellow;">default path of</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`"examples/"`</mark>) and <mark style="color:yellow;">`**kwargs`</mark> for additional arguments.  These configurations include essential details about the dataset, model, and training setup. This step is crucial as it sets up the parameters for how the dataset will be processed and how the model training will proceed.

<mark style="color:blue;">**Load Datasets**</mark>

The function <mark style="color:yellow;">`load_datasets`</mark> is called with the loaded configuration and parsed command-line arguments.&#x20;

This function is responsible for the heavy lifting of loading the dataset (which could include downloading it if not already present locally) and preprocessing it according to the specifications in the configuration. This step is central to preparing the data for model training.

<mark style="color:blue;">**ASCII Art and Configuration Loading**</mark>

It starts by printing ASCII art using <mark style="color:yellow;">`print_axolotl_text_art`</mark> for visual appeal. This is more for aesthetic purposes and has no impact on the functional aspects of the scrip

* Then, <mark style="color:yellow;">it loads the configuration file</mark> using <mark style="color:yellow;">`load_cfg`</mark>, which sets up the parameters for dataset preprocessing.  &#x20;
* &#x20;Initially, there's a deprecation warning from the <mark style="color:yellow;">`transformers.deepspeed`</mark> module. This suggests that in future versions of the Transformers library, you'll <mark style="color:yellow;">need to import DeepSpeed modules differently</mark>.&#x20;
* **Accelerator and User Token Checks**: It ensures that the default accelerator configuration is set and validates the user token for authentication or API access.
* **CLI Arguments Parsing**: The script uses <mark style="color:yellow;">`transformers.HfArgumentParser`</mark> to parse additional command-line arguments specific to preprocessing, defined in <mark style="color:yellow;">`PreprocessCliArgs`</mark>.
* **Dataset Preparation Path Check**: It checks if <mark style="color:yellow;">`dataset_prepared_path`</mark> is set in the configuration.  If the <mark style="color:yellow;">`dataset_prepared_path`</mark> is not explicitly set in the configuration, the script issues a warning and _<mark style="color:yellow;">assigns a default pat</mark>_<mark style="color:yellow;">h (</mark><mark style="color:yellow;">`DEFAULT_DATASET_PREPARED_PATH`</mark><mark style="color:yellow;">).</mark> This path is where the script will store the preprocessed dataset, ensuring that there’s always a defined location for this data.

<mark style="color:blue;">**Load and Preprocess Datasets**</mark>

The <mark style="color:yellow;">`load_datasets`</mark> function is called with the loaded configuration and parsed CLI arguments, handling the dataset loading and preprocessing.

* The script provides debug <mark style="color:yellow;">information about special tokens</mark> (End Of Sentence, Beginning Of Sentence, Padding, and Unknown) used by the tokenizer. This information is crucial for understanding how the model will interpret different types of tokens in the data.

<mark style="color:blue;">**Logging Success**</mark>

* Upon successful completion, the <mark style="color:yellow;">script logs a message indicating the path</mark> where the preprocessed data is stored. This is done using the <mark style="color:yellow;">`LOG.info`</mark> method, and the message is colored green for visibility.

<mark style="color:blue;">**Main Block**</mark>

This block checks if the script is the main program being run <mark style="color:yellow;">(</mark><mark style="color:yellow;">`__name__ == "__main__"`</mark><mark style="color:yellow;">)</mark> and not a module imported in another script. If it is the main program, it uses <mark style="color:yellow;">`fire.Fire(do_cli)`</mark> to enable the script to be run from the command line, where <mark style="color:yellow;">`do_cli`</mark> is the main function being executed.

<mark style="color:blue;">**General Observations**</mark>

* **User-Friendly**: The script is user-friendly, providing clear messages and using color coding for warnings and success messages.
* **Flexibility**: It is flexible and allows customization through command-line arguments.
* **Error Handling**: The script checks for potential issues like missing configuration parameters and handles them gracefully, providing default values and warnings.
* **Logging**: Effective use of logging helps in tracking the script's execution and diagnosing issues if any arise.

OUTPUT

1. <mark style="color:green;">**Warnings and ASCII Art**</mark><mark style="color:green;">:</mark>
2. <mark style="color:green;">**Token Information**</mark><mark style="color:green;">:</mark> The script provides debug <mark style="color:yellow;">information about special tokens</mark> (End Of Sentence, Beginning Of Sentence, Padding, and Unknown) used by the tokenizer. This information is crucial for understanding how the model will interpret different types of tokens in the data.

<!---->

1. <mark style="color:green;">**Data File Processing**</mark><mark style="color:green;">:</mark> The script downloads and extracts data files, then generates a training split with 51,760 examples. This is followed by mapping and filtering operations on the dataset, performed in parallel (noted by `num_proc=12`), which is an efficient way to handle large datasets.
2. <mark style="color:green;">**Dataset Merging and Saving**</mark><mark style="color:green;">:</mark> Post-processing, the datasets are merged and saved to disk. This is an essential step to ensure that the processed data is stored in a format ready for model training.
3. <mark style="color:green;">**Token Counts and Sample Packing**</mark><mark style="color:green;">:</mark> The script calculates the total number of tokens and supervised tokens. It also estimates the packing efficiency and total number of steps needed for training, which are critical for understanding how the data will be batched and fed into the model during training.
4. <mark style="color:green;">**Final Information and Path**</mark><mark style="color:green;">:</mark> Finally, the script concludes with a success message and provides the path to the preprocessed data. This is your confirmation that the preprocessing was successful and where the prepared data is stored.

</details>

This script for our Axolotl platform will be:&#x20;

<details>

<summary><mark style="color:green;">The configured</mark> <mark style="color:yellow;">Phi2-ft.yml</mark> <mark style="color:green;">YAML file</mark></summary>

```yaml
base_model: microsoft/phi-2
model_type: AutoModelForCausalLM
tokenizer_type: AutoTokenizer
load_in_8bit: false
load_in_4bit: false
strict: false
datasets:
  - path: datasets/alpaca-cleaned/alpaca_data_cleaned.json
    type: alpaca
    ds_type: json
    data_files:
      - alpaca_data_cleaned.json
dataset_prepared_path:
val_set_size: 0.20
output_dir: ./phi-out
sequence_len: 2048
sample_packing: true
pad_to_sequence_len: true
adapter:
lora_model_dir:
lora_r:
lora_alpha:
lora_dropout:
lora_target_linear:
lora_fan_in_fan_out:
wandb_project:
wandb_entity:
wandb_watch:
wandb_name:
wandb_log_model:
gradient_accumulation_steps: 1
micro_batch_size: 2
num_epochs: 4
optimizer: adamw_torch
adam_beta2: 0.95
adam_epsilon: 0.00001
max_grad_norm: 1.0
lr_scheduler: cosine
learning_rate: 0.000003
train_on_inputs: false
group_by_length: false
bf16: auto
fp16:
tf32: true
gradient_checkpointing: true
gradient_checkpointing_kwargs:
  use_reentrant: True
early_stopping_patience:
resume_from_checkpoint:
local_rank:
logging_steps: 1
xformers_attention:
flash_attention: true
warmup_steps: 100
evals_per_epoch: 4
saves_per_epoch: 1
debug:
deepspeed:
weight_decay: 0.1
fsdp:
fsdp_config:
resize_token_embeddings_to_32x: true
special_tokens:
  pad_token: "<|endoftext|>"





```

</details>

{% hint style="warning" %}
Potential Flash Attention Dependency Issues
{% endhint %}

### <mark style="color:red;">Flash Attention Issues</mark>

We had some issue with Flash Attention dependencies.  For some reason the axolotl environment keeps reverting to Pytorch 2.01 - Flash Attention needs Pytorch version 2.10

We executed this command in the axolotl library, and it upgraded Pytorch to 2.10.

```bash
pip install flash_attn -U --force-reinstall
```

<details>

<summary><mark style="color:green;">Flash Attention Debugging</mark></summary>

Flash Attention needs Pytorch 2.10 - not 2.0.  I had to force install Flash Attention to make it work:\
\
The error message you're encountering originates from running a Python script that attempts to preprocess a configuration file for a machine learning model using the <mark style="color:yellow;">`axolotl.cli.preprocess`</mark> module.&#x20;

The error is an <mark style="color:yellow;">`Import Error`</mark> associated with the <mark style="color:yellow;">`flash_attn_2_cuda`</mark> library, which is part of the `flash_attn` package. Let's break down the error message line by line:

1. **Command Executed**: <mark style="color:yellow;">`python -m axolotl.cli.preprocess your directory/axolotl/examples/llama-2/lora.yml`</mark>
   * This command attempts to run a Python module (<mark style="color:yellow;">`axolotl.cli.preprocess`</mark>) with a specific configuration file as its argument.
2. **Initial Traceback**:
   * The Python interpreter starts by <mark style="color:yellow;">trying to execute the module but encounters an issue in the process.</mark>
3. **Import Chain**:
   * The error arises in a chain of imports starting from your script's initial import statement. Python attempts to import various modules and packages needed for the script to run.
4. **Specific ImportError**:
   * The final error, <mark style="color:yellow;">`ImportError`</mark>, occurs when Python tries to import <mark style="color:yellow;">`flash_attn_2_cuda`</mark> from the <mark style="color:yellow;">`flash_attn`</mark> package.
   * The error message specifically states `undefined symbol: _ZN3c104cuda9SetDeviceEi`. This indicates a missing or incompatible symbol in the compiled CUDA extension.
5. [https://github.com/Dao-AILab/flash-attention/issues/620](https://github.com/Dao-AILab/flash-attention/issues/620)

#### <mark style="color:green;">Troubleshooting Steps</mark>

1. **Verify CUDA Installation**:
   * Ensure that CUDA is correctly installed on your system and is compatible with the versions required by `flash_attn`.
   * Check the CUDA version against the version required by <mark style="color:yellow;">`flash_attn`</mark>. If there's a mismatch, consider upgrading or downgrading CUDA.
2. **Check PyTorch and flash\_attn Compatibility**:
   * Verify that the installed PyTorch version is compatible with `flash_attn`. Incompatibilities between CUDA, PyTorch, and `flash_attn` can lead to such errors.
3. **Reinstall flash\_attn**:
   * Try reinstalling the `flash_attn` package. Sometimes, recompiling the package can resolve symbol mismatch errors.
   * Use the command <mark style="color:blue;">`pip install flash-attn --force-reinstall`</mark> to reinstall.
4. **Check Environment Variables**:
   * Ensure that your <mark style="color:yellow;">`LD_LIBRARY_PATH`</mark> environment variable includes the paths to the CUDA libraries.
5. **Inspect Python Environment**:
   * Verify that you are using the correct Python environment where all required dependencies are installed. Sometimes, conflicts in environments can cause such issues.
6. **Check for System Updates**:
   * Occasionally, system updates or changes to the compiler or related libraries can cause incompatibilities. Ensure your system is up to date.
7. **Consult Documentation or Community Forums**:
   * Check the documentation for `flash_attn` and related packages for any known issues or troubleshooting tips.
   * Seek help from relevant community forums or issue trackers for `flash_attn` and related projects.
8. **Test in a Clean Environment**:
   * If possible, try to run the script in a clean Python environment with only necessary packages installed. This can help rule out conflicts with other packages.

</details>

<details>

<summary><mark style="color:green;">Using the Upload File Function</mark></summary>

The <mark style="color:yellow;">`upload file`</mark> function from the Hugging Face Hub library is used to upload files to a repository on the Hugging Face Hub. This function is quite versatile, supporting various parameters to customize the upload process. Here's a breakdown of the parameters and what they mean:

1. <mark style="color:blue;">**path\_or\_fileobj (str, Path, bytes, or IO)**</mark><mark style="color:blue;">:</mark> This is the source of the file you want to upload. It can be a <mark style="color:yellow;">path to a file on your local machine</mark>, a binary data stream, a file object, or a buffer.
2. <mark style="color:blue;">**path\_in\_repo (str)**</mark><mark style="color:blue;">:</mark> This specifies where in the repository the file should be placed. For example, if you want to place a file in a folder called 'checkpoints', you would use something like `"checkpoints/weights.bin"`.
3. <mark style="color:blue;">**repo\_id (str)**</mark><mark style="color:blue;">:</mark> The identifier for the repository to which you are uploading. This usually follows the format `"username/repository-name"`.
4. <mark style="color:blue;">**token (str, optional)**</mark><mark style="color:blue;">:</mark> Your authentication token for the Hugging Face Hub. If you have already logged in using `HfApi.login`, this will default to the stored token. If not provided, the function will attempt to use a stored token from a previous login.
5. <mark style="color:blue;">**repo\_type (str, optional)**</mark><mark style="color:blue;">:</mark> Indicates the type of repository. It can be `"dataset"`, `"space"`, or `"model"`. If you are uploading to a dataset or a space, specify accordingly. The default is `None`, which is interpreted as a model.
6. <mark style="color:blue;">**revision (str, optional)**</mark><mark style="color:blue;">:</mark> Specifies the git revision (like a branch name or commit hash) from which the commit should be made. The default is the head of the "main" branch.
7. <mark style="color:blue;">**commit\_message (str, optional)**</mark><mark style="color:blue;">:</mark> A short summary or title for the commit you are making. Think of this as the headline of your changes.
8. <mark style="color:blue;">**commit\_description (str, optional)**</mark><mark style="color:blue;">:</mark> A more detailed description of the changes you are committing.
9. <mark style="color:blue;">**create\_pr (boolean, optional)**</mark><mark style="color:blue;">:</mark> Determines whether to create a Pull Request for the commit. Defaults to `False`. If `True`, a PR will be created based on the specified `revision`.
10. <mark style="color:blue;">**parent\_commit (str, optional)**</mark><mark style="color:blue;">:</mark> The hash of the parent commit to which your changes will be added. This is used to ensure that you are committing to the correct version of the repository, especially useful in concurrent environments.
11. <mark style="color:blue;">**run\_as\_future (bool, optional)**</mark><mark style="color:blue;">:</mark> If set to `True`, the upload process will run in the background as a non-blocking action. This returns a `Future` object that can be used to check the status of the upload.

The `path_in_repo` parameter in the `api.upload_file` function from the `huggingface_hub` library specifies the destination path within the repository on the Hugging Face Hub where the file will be uploaded. This is essentially the relative path in the repository where the file will be placed.

In this example command:

```python
api.upload_file(
    path_or_fileobj="/path/to/trained_model_weights.bin",
    path_in_repo="model_weights.bin",
    repo_id="username/my_ml_model",
    repo_type="model"
)
```

* <mark style="color:yellow;">`path_or_fileobj="/path/to/trained_model_weights.bin"`</mark>: This is the path to the file on your local machine. It indicates where the file is currently stored in your local file system.
* <mark style="color:yellow;">`path_in_repo="model_weights.bin"`</mark>: This determines where within your Hugging Face Hub repository the file will be saved. In this case, you are instructing the function to upload your file directly to the root of the repository and <mark style="color:yellow;">name it</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`model_weights.bin`</mark>. If you wanted to place this file inside a folder within your repository, you would specify a path like `"`<mark style="color:yellow;">`folder_name/model_weights.bin`</mark>`"`.
* <mark style="color:yellow;">`repo_id="username/my_ml_model"`</mark>: This identifies the specific repository on the Hugging Face Hub where the file should be uploaded. It's a combination of your username (or organization name) and the repository name.
* <mark style="color:yellow;">`repo_type="model"`</mark><mark style="color:yellow;">:</mark> This indicates the type of repository you are uploading to. In this case, it's a model repository.

</details>
