---
description: Sourced from the Axolotl documentation with permission
cover: broken-reference
coverY: 0
---

# Template-free prompt construction

Template-free prompt construction with the <mark style="color:yellow;">`input_output`</mark> format

### <mark style="color:blue;">Background</mark>

#### <mark style="color:green;">Masking Inputs</mark>

One of the most popular features of [axolotl](https://github.com/OpenAccess-AI-Collective/axolotl) is setting the following configuration value:

```bash
train_on_inputs: false
```

If you declare a [dataset formats](https://github.com/OpenAccess-AI-Collective/axolotl?tab=readme-ov-file#dataset) such as <mark style="color:yellow;">`alpaca`</mark> or <mark style="color:yellow;">`chatml`</mark>, axolotl knows what is an input (i.e. human) vs. an output (i.e. the assistant) and _<mark style="color:yellow;">masks the input labels</mark>_ so that your model can focus on _<mark style="color:yellow;">**predicting the outputs only.**</mark>_

#### <mark style="color:green;">You may not want prompt templates</mark>

However, there are many situations where you don’t want to use one of these formats or templates.  This is because they can:

* Add unnecessary boilerplate to your prompts.
* Create artifacts like special delimiters <mark style="color:yellow;">`<|im_start|>`</mark> that can quickly become footguns if you don’t include them correctly at inference time.
* Enforce a _chat_ interface when you do not want one. Sometimes you just want to fine-tune a model to a very specific task and do NOT want multi-turn conversations, roles, etc.
* Limit you to only certain roles that the template allows.

### <mark style="color:blue;">The</mark> <mark style="color:yellow;">`input_output`</mark> <mark style="color:blue;">format</mark>

You can construct your prompts without a template by using the <mark style="color:yellow;">`input_output`</mark> format, by setting <mark style="color:yellow;">`type: input_output`</mark> in your configuration file like this:

#### <mark style="color:green;">**config.yml**</mark>

```bash
train_on_inputs: false # Mask segments of your data
datasets:
  - path: output.jsonl
    type: input_output  # use template free prompt construction
```

Unlike <mark style="color:yellow;">`type: completion`</mark>, which is also template-free, <mark style="color:yellow;">`type: input_output`</mark> allows you to mask segments of your text. More details on how this works are described below.

### <mark style="color:blue;">Usage</mark>

This is how you can use the <mark style="color:yellow;">`input_output`</mark> format:

#### <mark style="color:green;">Prepare Data</mark>

To use the <mark style="color:yellow;">`input_output`</mark> format, collect your data in the following format into a [<mark style="color:blue;">jsonl file</mark>](broken-reference) (below is the first row from the file <mark style="color:yellow;">`output`</mark><mark style="color:yellow;">.jsonl\`</mark> pretty printed):

```bash
$ head -n1 output.jsonl | python -m json.tool

{.cell-output .cell-output-stdout}
    {
        "segments": [
            {
                "label": true,
                "text": "<s>Hello\n"
            },
            {
                "label": true,
                "text": "hi there!. "
            },
            {
                "label": false,
                "text": "goodbye "
            },
            {
                "label": true,
                "text": "farewell</s>"
            }
        ]
    }
```

Set <mark style="color:yellow;">`label:false`</mark> when you want to mask a segment of text so that the model isn’t trained on it. Some things to keep in mind:

{% hint style="warning" %}
&#x20;<mark style="color:blue;">**EOS, BOS, spaces, newlines etc. are entirely up to you.**</mark>&#x20;

Axolotl concatenates all the segments <mark style="color:yellow;">as-is.</mark>&#x20;

The tokenizer doesn’t add anything additional. Notice how I added spaces, newlines, `<s>` (BOS), and `</s>` (EOS) myself.&#x20;

Make sure you check the materialised output to validate that the prompt is getting assembled how you like.
{% endhint %}

#### <mark style="color:green;">Use</mark> <mark style="color:green;"></mark><mark style="color:green;">`type:`</mark>` `<mark style="color:yellow;">`input_output`</mark>

Let’s materialise data with our <mark style="color:yellow;">`output.jsonl`</mark> file by setting <mark style="color:yellow;">`type: input_output`</mark> in our axolotl config:

```bash
# training_config.yaml
base_model: mistralai/Mistral-7B-v0.1
data_seed: 49
seed: 49

datasets:
  - path: output.jsonl
    type: input_output
val_set_size: 0.1

sequence_len: 896
sample_packing: false

micro_batch_size: 2
gradient_accumulation_steps: 3
eval_batch_size: 2
num_epochs: 1
learning_rate: 0.0002

train_on_inputs: false
special_tokens:
  bos_token: "<s>"
  eos_token: "</s>"
  unk_token: "<unk>"
```

You can use the following command to materialise your data. The <mark style="color:yellow;">`--debug`</mark> flag will print the tokens, along with the labels so you can verify that the correct items are being ignored:

{% code overflow="wrap" %}
```bash
$ python -m axolotl.cli.preprocess training_config.yaml --debug

[2024-03-05 23:36:46,969] [INFO] [axolotl.check_example_labels:35] [PID:607731] [RANK:0] <s>(1, 1) Hello(22557, 22557)
(13, 13) hi(12014, 12014) there(736, 736) !(28808, 28808) .(28723, 28723) (28705, 28705) good(-100, 1179) bye(-100, 17664) (-100, 28705) fare(19111, 19111) well(5458, 5458) </s>(2, 2)
```
{% endcode %}

The format is <mark style="color:yellow;">`decoded_token`</mark><mark style="color:yellow;">(</mark><mark style="color:yellow;">`label`</mark><mark style="color:yellow;">,</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`token_id`</mark><mark style="color:yellow;">)</mark>, for example, <mark style="color:yellow;">`<s>(1, 1)`</mark> means that the token is <mark style="color:yellow;">`<s>`</mark>, the label is <mark style="color:yellow;">`1`</mark> and the token\_id is <mark style="color:yellow;">`1`</mark>. When the label is <mark style="color:yellow;">`-100`</mark> then that token is ignored for training.

#### <mark style="color:green;">Check the prompts</mark>

Here is another way to check the materialised output:

```bash
from transformers import AutoTokenizer
from datasets import load_from_disk
import yaml

directory = !ls last_run_prepared/
with open('training_config.yaml', 'r') as f:
    cfg = yaml.safe_load(f)
model_id = cfg['base_model']
tok = AutoTokenizer.from_pretrained(model_id)
ds = load_from_disk(f'last_run_prepared/{directory[0]}/')
```

```
>>> row = ds[0]
>>> print(tok.decode(row['input_ids']))
<s> Hello
    hi there!.  goodbye  farewell</s>
```

We can check that the right tokens are ignored by comparing the labels to each token:

```bash
import pandas as pd
pd.DataFrame([{'token': tok.decode(i), 'label': l, 'id':i} for i,l in
              zip(row['input_ids'], row['labels'])])
```

| token | label | id    |
| ----- | ----- | ----- |
| 0     | \<s>  | 1     |
| 1     | Hello | 22557 |
| 2     |       | 13    |
| 3     | hi    | 12014 |
| 4     | there | 736   |
| 5     | !     | 28808 |
| 6     | .     | 28723 |
| 7     |       | 28705 |
| 8     | good  | -100  |
| 9     | bye   | -100  |
| 10    |       | -100  |
| 11    | fare  | 19111 |
| 12    | well  | 5458  |
| 13    | \</s> | 2     |

If we look at the input data, the above table seems correct!&#x20;

The jsonl version is repeated below for reference:

```bash
$ head -n1 output.jsonl | python -m json.tool

{.cell-output .cell-output-stdout}
    {
        "segments": [
            {
                "label": true,
                "text": "<s>Hello\n"
            },
            {
                "label": true,
                "text": "hi there!. "
            },
            {
                "label": false,
                "text": "goodbye "
            },
            {
                "label": true,
                "text": "farewell</s>"
            }
        ]
    }
```
