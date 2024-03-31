---
cover: broken-reference
coverY: 0
---

# Downloading Phi 2.0

#### <mark style="color:blue;">Click on this link below to review Phi 2.0 at the Huggingface model repository:</mark>

{% embed url="https://huggingface.co/microsoft/phi-2" %}

The screen cut below is from the Huggingface Models Database - specifically Phi 2.0.

To download the model, <mark style="color:yellow;">left click on the vertical three dots</mark> next to the "TRAIN" button. &#x20;

You can click on the diagram below to see the three vertical dots:

<figure><img src="broken-reference" alt=""><figcaption></figcaption></figure>

When you <mark style="color:yellow;">left click</mark> the three vertical docks you can see the instructions to download the model to your local host.

<figure><img src="broken-reference" alt=""><figcaption><p>Instructions on how to download a Huggingface model</p></figcaption></figure>

Enter the command below at your prompt:

```bash
git clone https://huggingface.co/microsoft/phi-2
```

If you don't want to download the entire model files due to bandwidth issues,  you can set the environmental variable as per below _<mark style="color:yellow;">**prior to downloading the model**</mark>_ using the git clone command,.

```bash
GIT_LFS_SKIP_SMUDGE=1
```

Setting `GIT_LFS_SKIP_SMUDGE=1` tells Git LFS to <mark style="color:yellow;">skip the automatic downloading of the actual content of large files</mark> tracked by LFS when cloning a repository.&#x20;

Instead, <mark style="color:yellow;">only the pointer files are cloned.</mark>&#x20;

The "smudge" process is what usually replaces these pointers with the actual file content during cloning. &#x20;

By running this command, you clone the <mark style="color:yellow;">`microsoft/phi-2`</mark> repository without immediately downloading the large files tracked by LFS.  If you later decide that you need these large files, you can use Git LFS commands to fetch them.

If you do download all the files using the git clone command you should see the following folder and associated files in your VS Code IDE:

<figure><img src="broken-reference" alt=""><figcaption><p>Phi 2.0 downloaded files</p></figcaption></figure>

With the model downloaded to your local directory, the next step is to <mark style="color:yellow;">download the dataset</mark> you wish to use for fine tuning the model.
