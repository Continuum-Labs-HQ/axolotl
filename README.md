---
description: Once the model has been downloaded, the dataset is next
cover: broken-reference
coverY: 0
---

# Download the dataset

The next step is to <mark style="color:yellow;">download the dataset.</mark> This document provides a high-level overview of how datasets work on Huggingface and then provide specific instructions on how to <mark style="color:blue;">download dataset into the Axolotl platform.</mark>

### <mark style="color:blue;">The HuggingFace Hub has numerous datasets</mark>

<details>

<summary><mark style="color:green;">HuggingFace Dataset Summary</mark></summary>

The Hugging Face Hub hosts a wide array of datasets for various tasks like translation, speech recognition, and image classification. These datasets are stored in Git repositories and contain scripts for data download and split generation.

1. <mark style="color:blue;">**Dataset Viewer**</mark><mark style="color:blue;">:</mark> Many datasets, like GLUE, feature a Dataset Viewer to preview data.
2. <mark style="color:blue;">**Repository Structure**</mark><mark style="color:blue;">:</mark> Each dataset repository has a specific structure for efficient data handling. Adhering to this structure ensures the dataset page on the Hub will have a Viewer.
3. <mark style="color:blue;">**Search and Filter**</mark><mark style="color:blue;">:</mark> Datasets can be searched and filtered by language, tasks, and licenses on the Hub.
4. <mark style="color:blue;">**Privacy Settings**</mark><mark style="color:blue;">:</mark> Dataset visibility can be toggled between private and public. For organization-owned datasets, these settings apply to all members.
5. <mark style="color:blue;">**Dataset Cards**</mark>: Each dataset is documented with a `README.md` file in the repository, acting as a dataset card. This card provides context and usage instructions and can include metadata like license, language, size, and tags for easy discovery.
6. <mark style="color:blue;">**Metadata in Dataset Cards**</mark><mark style="color:blue;">:</mark> Metadata added to the dataset card enables interactions on the Hub, like filtering and discovering datasets, and displaying licenses.
7. <mark style="color:blue;">**Linking to Papers**</mark><mark style="color:blue;">:</mark> Including a paper link on arXiv in the dataset card adds the dataset to relevant tags and facilitates finding models citing the same paper.
8. <mark style="color:blue;">**Gated Datasets**</mark><mark style="color:blue;">:</mark> Creators can control access to their datasets. Users must agree to terms and share contact information to access these datasets. Dataset owners can view user access reports.
9. <mark style="color:blue;">**Customizing User Access Prompts**</mark><mark style="color:blue;">:</mark> The access request dialog can be customized with additional text and checkbox fields for specific user agreements.
10. <mark style="color:blue;">**Manual Approval of Access**</mark><mark style="color:blue;">:</mark> Dataset authors can choose to manually review and approve access requests. An API is available for managing access requests.
11. <mark style="color:blue;">**Notifications**</mark><mark style="color:blue;">:</mark> Default notification settings send daily emails for new access requests. These can be customized for real-time updates or sent to a specific email.
12. <mark style="color:blue;">**Additional Customization**</mark><mark style="color:blue;">:</mark> Text in the gate's heading and button can be customized to suit specific requirements.

</details>

### <mark style="color:blue;">Uploading datasets for future use</mark>

<details>

<summary><mark style="color:green;">Uploading Huggingface Datasets</mark></summary>

Hugging Face's Hub allows for uploading and sharing of a wide range of datasets. Here's a summary of the key points for uploading datasets:

1. <mark style="color:blue;">**Account Creation**</mark><mark style="color:blue;">:</mark> Start by creating a Hugging Face Hub account.
2. <mark style="color:blue;">**Upload Using the Hub UI**</mark><mark style="color:blue;">:</mark> This user-friendly interface allows even non-developers to upload datasets.
3. <mark style="color:blue;">**Creating a Repository**</mark><mark style="color:blue;">:</mark> A repository is where your dataset files and their revision history are stored. It supports multiple dataset versions.
4. <mark style="color:blue;">**Uploading a Dataset**</mark><mark style="color:blue;">:</mark> After creating a repository, you can upload dataset files through the "Files and versions" tab. <mark style="color:green;">The Hub supports various file formats like .csv, .mp3, and .jpg</mark>.
5. <mark style="color:blue;">**Dataset Card Creation**</mark><mark style="color:blue;">:</mark> This is crucial for helping users discover and understand your dataset. It involves selecting important metadata tags and writing detailed documentation about your dataset.
6. <mark style="color:blue;">**Dataset Viewer**</mark><mark style="color:blue;">:</mark> For public datasets, the Dataset Viewer allows users to preview the data before downloading.
7. <mark style="color:blue;">**Using the huggingface\_hub Client Library**</mark><mark style="color:blue;">:</mark> This library offers advanced features for managing repositories and uploading datasets.
8. <mark style="color:blue;">**Using Other Libraries**</mark><mark style="color:blue;">:</mark> Libraries like 🤗 Datasets, Pandas, Dask, or DuckDB can also upload files to the Hub.
9. <mark style="color:blue;">**Using Git**</mark><mark style="color:blue;">:</mark> Dataset repositories, being Git repositories, allow the use of Git to push data files to the Hub.
10. <mark style="color:blue;">**Supported File Formats**</mark><mark style="color:blue;">:</mark> The Hub supports a variety of file formats, including CSV, JSON, Parquet, Text, Images, and Audio files. Compressed files in formats like ZIP, GZIP, and others are also supported.
11. <mark style="color:blue;">**Downloading Datasets**</mark><mark style="color:blue;">:</mark> The Hub also facilitates the downloading of datasets.

This summary provides a comprehensive overview of how to effectively utilize the Hugging Face Hub for uploading and managing datasets, emphasizing its accessibility and support for a wide range of file formats.

</details>

### <mark style="color:blue;">Download a Huggingface dataset</mark>

Downloading datasets from the Hugging Face Hub can be accomplished through several methods.  We will be using the 'git clone' method:

### <mark style="color:blue;">**Using Git**</mark>

* All datasets on the Hub are stored as Git repositories, allowing for cloning directly to the local machine.
* This method is particularly useful for large datasets or when you require the entire dataset repository.
* Before cloning, ensure Git Large File Storage (LFS) is installed with <mark style="color:yellow;">`git lfs install`</mark><mark style="color:yellow;">.</mark>
* Clone the dataset using the command:

```bash
git clone git@hf.co:datasets/<dataset ID>
```

* Replace <mark style="color:yellow;">`<dataset ID>`</mark> with the actual ID of the dataset you wish to clone (e.g., <mark style="color:yellow;">`git clone git@hf.co:datasets/allenai/c4`</mark>).
* If you have write-access to the dataset repository, you can also commit and push revisions.
* To push changes or access private repositories, add your SSH public key to your user settings on Hugging Face.

<details>

<summary>Reference: <mark style="color:green;">Using the Fast Download Library</mark></summary>

The <mark style="color:yellow;">`HF_HUB_ENABLE_HF_TRANSFER`</mark> environment variable, when set to <mark style="color:yellow;">`True`</mark>, enhances the speed of uploads and downloads from the Hugging Face Hub by utilizing a Rust-based package called <mark style="color:yellow;">`hf_transfer`</mark><mark style="color:yellow;">.</mark> Here's a summary of its functionality and considerations:

<mark style="color:blue;">**Enhanced Speed**</mark>

By default, Hugging Face Hub employs Python-based functions like <mark style="color:yellow;">`requests.get`</mark> and <mark style="color:yellow;">`requests.post`</mark> for uploads and downloads. While reliable, these methods may not be the most efficient for high-bandwidth machines. `hf_transfer` is a Rust-based package that optimizes bandwidth usage by <mark style="color:yellow;">splitting large files into smaller parts and transferring them concurrently with multiple threads</mark>. This approach has the potential to double the transfer speed.

<mark style="color:blue;">**Installation**</mark>

To use <mark style="color:yellow;">`hf_transfer`</mark>, you must install it separately from PyPI (Python Package Index) and set the environment variable <mark style="color:yellow;">`HF_HUB_ENABLE_HF_TRANSFER`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">to</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`1`</mark>. This enables the Rust-based transfer logic for faster operations.

<mark style="color:blue;">**Limitations**</mark>

It is essential to be aware of certain limitations when using <mark style="color:yellow;">`hf_transfer`</mark><mark style="color:yellow;">:</mark>

* Debugging may be challenging since it is not purely Python-based.
* <mark style="color:yellow;">`hf_transfer`</mark> lacks some user-friendly features such as resumable downloads and proxy support. These omissions are intentional to maintain the simplicity and speed of the Rust logic.

<mark style="color:blue;">**Default State**</mark>

<mark style="color:yellow;">`f_transfer`</mark> is not enabled by default in Hugging Face Hub, meaning that you need to explicitly set <mark style="color:yellow;">`HF_HUB_ENABLE_HF_TRANSFER`</mark> to <mark style="color:yellow;">`True`</mark> if you wish to utilize its enhanced transfer capabilities.

In summary, <mark style="color:yellow;">`HF_HUB_ENABLE_HF_TRANSFER`</mark> is an environment variable that, when activated, leverages the Rust-based <mark style="color:yellow;">`hf_transfer`</mark> package to significantly improve upload and download speeds from the Hugging Face Hub. However, it's important to be aware of its limitations, including potential debugging challenges and the absence of certain features, as it is not the default transfer method in Hugging Face Hub.

</details>
