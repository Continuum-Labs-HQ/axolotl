---
description: Base Model + Model Type + Tokenizer Type
cover: broken-reference
coverY: 0
---

# Available Models

Axolotl provides 24 different models for fine tuning. &#x20;

Below are a selection of the different models available for training on the axolotl platform for your reference:

<details>

<summary><mark style="color:purple;">Cerebras Model</mark></summary>

Cerebras has released Cerebras-GPT, a suite of seven GPT models, open-sourced to foster accessible advanced AI models. These models, ranging from 111 million to 13 billion parameters, were trained using the Chinchilla formula for optimal compute efficiency. Notably, Cerebras-GPT models boast faster training times, lower costs, and reduced energy consumption compared to other publicly available models.

**Training and Architecture**

The models were trained on the CS-2 systems of the Andromeda AI supercomputer, leveraging a simple, data-parallel weight streaming architecture. This approach allowed for rapid training, avoiding complexities of model partitioning. A new scaling law, derived from this training, predicts model performance based on the compute budget, a significant contribution to AI research.

**Accessibility and Usage**

Cerebras-GPT models are fully open-source, available on Hugging Face and GitHub under the Apache 2.0 license. This release includes all models, weights, and checkpoints, with detailed training methods and performance results documented in a paper. The Cerebras CS-2 systems are also accessible on-demand via Cerebras Model Studio.

**Large Language Models (LLMs) Landscape**

Cerebras-GPT addresses the growing trend of large, closed-source LLMs like OpenAI's GPT-4, which often lack transparency in model architecture and training details. Cerebras-GPT, conversely, is open and reproducible, aiming to make LLMs more accessible for both research and commercial applications.

**Compute-Optimal Training**

The Chinchilla recipe, which dictates using 20 data tokens per model parameter, guided the training of Cerebras-GPT models. This method contrasts with models trained on fixed data amounts regardless of size, leading to Cerebras-GPT achieving lower loss per compute unit across all model sizes.

**Model Performance and Scaling Law**

Cerebras-GPT models show state-of-the-art efficiency on common downstream language tasks. The scaling law established by Cerebras offers a predictive measure of model loss before training, optimizing the training process for various model sizes using the open Pile dataset.

**Training Infrastructure**

Training large models like Cerebras-GPT typically requires complex and technical infrastructure, especially on GPUs. However, Cerebras used standard data parallelism on its CS-2 systems, avoiding the need for intricate model parallelism. This simplicity allows researchers to focus more on model design than on distributed systems engineering.

**Conclusion**

Cerebras' release of Cerebras-GPT and its training infrastructure aims to democratize large model training and research. By providing efficient training methods, open-source models, and accessible infrastructure, Cerebras contributes to the advancement of the generative AI industry.

</details>

<details>

<summary><mark style="color:purple;">Code-Llama</mark></summary>

Code Llama, released on August 24, 2023, is a large language model (LLM) developed for coding tasks. It's built upon Llama 2 and fine-tuned specifically for generating and discussing code. The model is made freely available for both research and commercial purposes.

**Capabilities and Features**

* **Enhanced Coding Abilities**: Code Llama can generate and interpret code from both code and natural language prompts. It's proficient in code completion and debugging, supporting popular programming languages like Python, C++, Java, PHP, Typescript, C#, and Bash.
* **Model Variants**: Three sizes of Code Llama are available, with 7B, 13B, and 34B parameters. These models have been trained on 500 billion tokens of code and code-related data.
* **Fill-in-the-Middle (FIM) Capability**: The 7B and 13B models can insert code into existing snippets, aiding tasks like code completion.
* **Serving and Latency**: The models are designed to cater to varying needs. The 7B model works on a single GPU, while the 34B model offers superior results with higher latency. The smaller models are faster, suitable for real-time tasks.

**Specialised Versions**

* **Code Llama – Python**: A Python-specific variation, further fine-tuned on 100 billion tokens of Python code, catering to the significant role of Python in AI and code generation.
* **Code Llama – Instruct**: This variant is instruction fine-tuned to better comprehend and respond to natural language instructions, making it ideal for generating helpful and safe code responses.

**Use Cases and Impact**

Code Llama aims to streamline developer workflows, focusing on efficiency and reducing repetitive tasks. It's intended for a broad range of sectors, including research, industry, open-source projects, NGOs, and businesses. The release is part of an effort to foster innovation and safety in AI, with the community encouraged to explore, evaluate, and enhance the model's capabilities.

</details>

<details>

<summary><mark style="color:purple;">Falcon</mark></summary>

Falcon LLM is a suite of generative large language models (LLMs) designed to advance various applications, featuring models with different parameter sizes and a high-quality dataset.

**Falcon 40B**

* **Specifications**: Falcon 40B, with 40 billion parameters, was trained on one trillion tokens.
* **Ranking**: It was the top-ranked open-source AI model on Hugging Face’s leaderboard for two months post-launch.
* **Accessibility**: Offered royalty-free, Falcon 40B democratizes AI technology.
* **Multilingual Support**: Supports multiple languages including English, German, Spanish, French, Italian, and others.
* **Usage**: Serves as a base model for fine-tuning according to specific needs.
* **Call for Proposals**: Invited proposals for innovative use cases, with selected ones receiving investment in training compute.
* **Efficiency**: Uses less training compute compared to GPT-3, Chinchilla AI, and PaLM-62B.
* **Data Quality**: Trained on around five trillion tokens from diverse sources, with a focus on high-quality data extraction.

**Falcon 180B**

* **Specifications**: Falcon 180B is a more powerful model with 180 billion parameters, trained on 3.5 trillion tokens.
* **Performance**: Tops the Hugging Face Leaderboard and excels in reasoning, coding, proficiency, and knowledge tests.
* **Comparison**: Ranks closely behind OpenAI's GPT 4 and on par with Google's PaLM 2 Large, despite being smaller in size.
* **Availability**: Available for both research and commercial use, subject to Terms & Conditions and Acceptable Use Policy.

</details>

<details>

<summary><mark style="color:purple;">Mistral</mark></summary>

Mistral AI has released Mistral 7B, a highly efficient and powerful language model with 7.3 billion parameters. It stands out for its performance in various benchmarks, surpassing larger models in the Llama series.

**Key Features and Performance**

* **Benchmarking**: Mistral 7B outperforms the Llama 2 13B in all benchmarks and competes closely with Llama 1 34B. It approaches CodeLlama 7B's performance in coding tasks while maintaining proficiency in English tasks.
* **Efficiency**: Uses Grouped-query attention (GQA) and Sliding Window Attention (SWA), enhancing inference speed and handling longer sequences more efficiently.
* **Licensing**: Released under the Apache 2.0 license, allowing unrestricted use, including local deployment and cloud-based implementation.

**Accessibility and Deployment**

* Mistral 7B can be downloaded and used anywhere with a reference implementation.
* It is deployable on major cloud platforms like AWS, GCP, and Azure, using vLLM inference server and skypilot.
* Also available on HuggingFace.

**Fine-Tuning and Customization**

* Mistral 7B is easy to fine-tune for specific tasks. A fine-tuned model for chat, demonstrating superior performance compared to Llama 2 13B chat, is provided.

**Technical Advancements**

* **Sliding Window Attention**: Each layer attends to the previous 4,096 hidden states, resulting in a linear compute cost. This mechanism allows higher layers to access information further in the past, enhancing model performance.
* **Local Attention**: Employs fixed attention span with rotating buffers in the cache, reducing memory usage during inference.

**Benchmark Details**

* Mistral 7B was evaluated across various themes like commonsense reasoning, world knowledge, reading comprehension, math, and code.
* On reasoning, comprehension, and STEM reasoning benchmarks, Mistral 7B performs comparably to a hypothetical Llama 2 model three times its size.
* Notably, it performs well on all evaluations except knowledge benchmarks, where it matches the performance due to its parameter limit.

**Fine-tuning for Chat Applications**

* Mistral 7B Instruct, fine-tuned on public datasets from HuggingFace, shows excellent generalization capabilities. It outperforms all 7B models on MT-Bench and compares favorably to 13B chat models.

</details>

<details>

<summary><mark style="color:purple;">XJen 7b</mark></summary>

Salesforce has introduced XGen-7B, a significant addition to the realm of open-source generative AI models. This large language model (LLM) stands out for its extended context support, allowing for more comprehensive interactions.

**Key Features of XGen-7B**

* **Model Size**: XGen-7B has 7 billion parameters, indicative of its extensive capabilities.
* **Context Window**: A notable feature is its 8K context window, which enables it to handle larger prompts and generate longer responses. This context window represents the combined size of input and output text.
* **Tokenization**: It uses the OpenAI tokenizing system, similar to models like GPT-3 and GPT-4, for converting text into tokens.
* **Performance**: Salesforce claims that XGen-7B achieves results comparable to or better than other state-of-the-art models of similar size.

**Variants of XGen-7B**

Salesforce has released three variants of the XGen-7B model:

1. **XGen-7B-4K-base**: Supports a 4K context window.
2. **XGen-7B-8K-base**: Trained with additional data for an 8K context length.
3. **XGen-7B-{4K,8K}-inst**: Trained on instructional data for applications like chatbots, using reinforcement learning from human feedback (RLHF) techniques.

**Licensing and Usage**

* The first two variants, XGen-7B-4K-base and XGen-7B-8K-base, are released under the Apache 2.0 open-source license, allowing for commercial use.
* The instructional variant is available only for research purposes.

**Training and Capabilities**

* Salesforce used a mix of datasets, including RedPajama, Wikipedia, and their own Starcoder, for training XGen-7B.
* The model supports 22 languages, making it multilingual.
* XGen-7B excels in Massive Multitask Language Understanding, answering multiple-choice questions across various knowledge domains.
* It also performs well in conversations, long-form Q\&A, and summarization.

**Limitations**

Salesforce acknowledges that XGen-7B shares common limitations of LLMs, such as potential biases, toxicity, and hallucinations.

</details>



###
