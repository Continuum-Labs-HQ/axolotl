---
description: Downloading methods
---

# Huggingface Datasets

Hugging Face datasets can be downloaded and loaded using various methods.&#x20;

Here's a summary:

<mark style="color:blue;">**From Hugging Face Hub Without a Loading Script**</mark>

You can load datasets directly from any dataset repository on the Hub using the <mark style="color:yellow;">`load_dataset()`</mark> function. Provide the repository namespace and dataset name to load the dataset.

<mark style="color:blue;">**Local Loading Script**</mark>

If you have a local HuggingFace Datasets loading script, you can load the dataset by specifying the local path to the loading script file or the directory containing it.

<mark style="color:blue;">**Local and Remote Files**</mark>

Datasets stored as CSV, JSON, TXT, Parquet, or Arrow files on your computer or remotely can be loaded using the <mark style="color:yellow;">`load_dataset()`</mark> function. Specify the file type and the path or URL to the data files.

<mark style="color:blue;">**In-memory Data**</mark>

You can create a dataset directly from in-memory data structures like Python dictionaries and Pandas DataFrames using functions like <mark style="color:yellow;">`from_dict()`</mark> and <mark style="color:yellow;">`from_pandas()`</mark><mark style="color:yellow;">.</mark>

<mark style="color:blue;">**Offline**</mark>

Datasets can be loaded offline if they are stored locally or if you have previously downloaded them.

<mark style="color:blue;">**Specific Slice of a Split**</mark>

You can load specific slices of a dataset split by using the <mark style="color:yellow;">`split`</mark> parameter in the <mark style="color:yellow;">`load_dataset()`</mark> function.

<mark style="color:blue;">**Multiprocessing**</mark>

For datasets consisting of several files, you can speed up the downloading and preparation using the <mark style="color:yellow;">`num_proc`</mark> parameter to set the number of processes for parallel execution.

<mark style="color:blue;">**SQL**</mark>

Datasets can be read from SQL databases using <mark style="color:yellow;">`from_sql()`</mark> by specifying the URI to connect to your database.

<mark style="color:blue;">**Arrow Streaming Format**</mark>

The Huggingface Datasets library can load local Arrow files directly using <mark style="color:yellow;">`Dataset.from_file()`</mark><mark style="color:yellow;">.</mark> This method memory-maps the Arrow file without preparing the dataset in the cache.

<mark style="color:blue;">**Python Generator**</mark>

A dataset can be created from a Python generator with <mark style="color:yellow;">`from_generator()`</mark><mark style="color:yellow;">.</mark> This method supports loading data larger than available memory and can also define a sharded dataset.

### <mark style="color:blue;">Key Features and Functionalities</mark>

* **Flexibility**: The library <mark style="color:yellow;">**can handle datasets stored in various formats and locations, including local and remote repositories, and in-memory data.**</mark>
* **Dataset Splits**: Data can be <mark style="color:yellow;">**mapped to specific splits like 'train', 'test', and 'validation'**</mark> using the `data_files` parameter. This parameter accepts file paths mapped to split names.
* **Version Control**: You can load different versions of a dataset based on Git tags, branches, or commits using the `revision` parameter.
* **Subset Loading**: For large datasets, you have the option to load only a subset of files, which is useful for large datasets like C4 (around 13TB).
* **Pattern Matching**: Load files that match specific patterns or from specified directories within a dataset repository.
* **No Loading Script Required**: The library allows loading datasets without the need for a custom loading script, simplifying the process.

### <mark style="color:blue;">Custom Datasets</mark>

* **Custom Dataset Repositories**: Users can create their dataset repositories on the Hugging Face Hub, facilitating easy sharing and loading of datasets.
