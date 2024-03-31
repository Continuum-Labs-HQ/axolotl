---
cover: broken-reference
coverY: 0
---

# Popular Datasets

This is an analysis of the most popular datasets.  You can skip this section if you want to move forward to downloading the dataset for your fine tuning run.

### <mark style="color:blue;">Alpaca Cleaned</mark>

The cleaned Alpaca Dataset is a _<mark style="color:yellow;">**curated and cleaned version of the original dataset**</mark>_ used to train the Alpaca Large Language Model (LLM).&#x20;

The original dataset, generated using GPT-3, had several issues that impacted its quality and usefulness for training machine learning models. The cleaned version addresses these problems to improve the performance of models trained on this data.

{% embed url="https://huggingface.co/datasets/yahma/alpaca-cleaned" %}
Alpaca Cleaned Dataset
{% endembed %}

#### <mark style="color:green;">Key points</mark>

1. The cleaned dataset fixes issues such as hallucinations, merged instructions, empty outputs, missing code examples, incorrect answers, and unclear instructions.
2. On April 8, 2023, the remaining uncurated instructions (around 50,000) were replaced with data from the GPT-4-LLM dataset. Curation of the new data is ongoing.
3. The average prompt length in the cleaned dataset is longer than the original, with many prompts exceeding 256 tokens. It is recommended to set the maximum prompt length to at least 512 or higher during fine-tuning.

This cleaned dataset aims to provide a higher-quality resource for training and fine-tuning LLMs, ultimately leading to better-performing models with reduced hallucinations.

### <mark style="color:blue;">Open Orca</mark>

The OpenOrca dataset is a collection of augmented [FLAN Collection data](https://arxiv.org/abs/2301.13688). Currently \~1M GPT-4 completions, and \~3.2M GPT-3.5 completions.&#x20;

It is tabularised in alignment with the distributions presented in the ORCA paper and currently represents a partial completion of the full intended dataset, with ongoing generation to expand its scope.&#x20;

{% embed url="https://huggingface.co/datasets/Open-Orca/OpenOrca" %}
Open Orca Dataset
{% endembed %}

{% embed url="https://arxiv.org/abs/2306.02707" %}
Orca Paper
{% endembed %}

{% embed url="https://arxiv.org/abs/2301.13688" %}
Flan Collection
{% endembed %}

### <mark style="color:blue;">Financial Phrase Databank</mark>

The Financial Phrase Bank dataset is a collection of approximately 5,000 English sentences from financial news articles, annotated for sentiment analysis. The sentences are labeled as positive, negative, or neutral based on their potential impact on stock prices, from an investor's perspective.

{% embed url="https://huggingface.co/datasets/financial_phrasebank" %}
Financial Phrase Bank dataset&#x20;
{% endembed %}

Key features of the dataset:

* Contains 4,840 sentences from English financial news
* Sentences are labeled as 'positive', 'negative', or 'neutral'
* Annotations were performed by 16 people with financial background
* Available in four configurations based on annotator agreement percentages: 50%, 66%, 75%, and 100%
* No predefined train/validation/test split
* Sourced from a subset of 10,000 articles covering various companies, industries, and news sources
* Annotators were from the same institution (Aalto University School of Business)

This dataset is useful for training and benchmarking sentiment analysis models in the financial domain.&#x20;
