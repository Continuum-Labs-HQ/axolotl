---
description: General Introduction
---

# Downloading models

We can download the model to our local host from the Huggingface Model Hub.

If you are unfamiliar with the Huggingface Model Hub, the Youtube video below provides a rundown.

{% embed url="https://www.youtube.com/watch?t=2s&v=XvSGPZFEjDY" %}
Worth watching despite the moustache
{% endembed %}

<details>

<summary><mark style="color:green;">Summary of Huggingface Model Hub</mark></summary>

Navigating the Hugging Face Model Hub:

1. Access the model hub by clicking on the <mark style="color:yellow;">"Models" tab</mark> in the <mark style="color:yellow;">upper right corner</mark> of the Hugging Face landing page.
2. The model hub interface is divided into several parts:
   * <mark style="color:blue;">Left side:</mark> Categories for tailoring model search
     * <mark style="color:green;">Tasks:</mark> Various tasks such as NLP, computer vision, and speech recognition
     * <mark style="color:green;">Libraries:</mark> Model backbones (PyTorch, TensorFlow, JAX) and high-level frameworks (transformers, etc.)
     * <mark style="color:green;">Datasets:</mark> Filter models trained on specific datasets
     * <mark style="color:green;">Languages:</mark> Filter models that handle selected languages
     * <mark style="color:green;">License:</mark> Choose the license under which the model is shared
   * <mark style="color:blue;">Right side:</mark> Available models on the hub, ordered by downloads by default
3.  Clicking on a model <mark style="color:yellow;">opens its model card</mark>, which contains crucial information:

    * Description, intended use, limitations, and biases
    * Code snippets for model usage
    * Training procedure, data processing, evaluation results, and copyrights
    * Inference API on the right for testing the model with user inputs



    The "Files and versions" tab displays the model repositories' architecture, branches, commit history.

</details>

### <mark style="color:blue;">The Model Card</mark>

Model cards are files that accompany the models and provide handy information.   Under the hood, model cards are simple Markdown files with additional metadata.&#x20;

Model cards are essential for discoverability, reproducibility, and sharing.  You can find a model card as the <mark style="color:yellow;">`README.md`</mark> file in any model repository.

The model card should describe:

* the model
* its intended uses and potential limitations, including biases and ethical considerations
* the training parameters and experimental info&#x20;
* which datasets were used to train your model
* the model’s evaluation results

### <mark style="color:blue;">Downloading Models from Hugging Face Hub</mark>

The Hugging Face Hub provides several ways to download and use models, depending on your requirements and the tools you are using. This documentation will guide you through the different methods available.

### <mark style="color:blue;">Using Git</mark>

All models on the Model Hub are stored as Git repositories, _<mark style="color:yellow;">**which means you can clone them locally using Git commands.**</mark>_ To clone a model, follow these steps:

If you have not already, install Git LFS (Large File Storage) by running:

```bash
git lfs install
```

Clone the model repository using the following command:

```bash
git clone git@hf.co:<MODEL ID>
```

Replace <mark style="color:yellow;">`<MODEL ID>`</mark> with the actual model ID.  For example:

```bash
git clone git@hf.co:bigscience/bloom
```

If you have write access to a particular model repository, you can also commit and push revisions to the model.  We provide instructions on how to [<mark style="color:blue;">upload models here.</mark>](broken-reference)

By following these methods, you can easily download and use models from the Hugging Face Hub in your projects, whether you're using integrated libraries, the Hugging Face Client Library, or Git directly.
