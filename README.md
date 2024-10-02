---
base_model: google/gemma-2-9b-it
library_name: peft
license: apache-2.0
datasets:
- neo4j/text2cypher-2024v1
language:
- en
pipeline_tag: text2text-generation
tags:
- neo4j
- cypher
- text2cypher
---

# Model Card for Model ID

<!-- Provide a quick summary of what the model is/does. -->



## Model Details

### Model Description

This model serves as a demonstration of how fine-tuning foundational models using the Neo4j-Text2Cypher(2024) Dataset ([link](https://huggingface.co/datasets/neo4j/text2cypher-2024v1)) can enhance performance on the Text2Cypher task.\
Please note, this is part of ongoing research and exploration, aimed at highlighting the dataset's potential rather than a production-ready solution.


**Base model:** google/gemma-2-9b-it \
**Dataset:** neo4j/text2cypher-2024v1

An overview of the finetuned models and benchmarking results are shared at [Link](TODO Link to Blogposts)


<!-- - **Developed by:** [More Information Needed]
- **Funded by [optional]:** [More Information Needed]
- **Shared by [optional]:** [More Information Needed]
- **Model type:** [More Information Needed]
- **Language(s) (NLP):** [More Information Needed]
- **License:** [More Information Needed]
- **Finetuned from model [optional]:** [More Information Needed] -->

<!-- ### Model Sources [optional]

<!-- Provide the basic links for the model. -->

<!-- - **Repository:** [More Information Needed]
- **Paper [optional]:** [More Information Needed]
- **Demo [optional]:** [More Information Needed] -->

<!-- ## Uses -->

<!-- Address questions around how the model is intended to be used, including the foreseeable users of the model and those affected by the model. -->

<!-- ### Direct Use -->

<!-- This section is for the model use without fine-tuning or plugging into a larger ecosystem/app. -->
 
<!-- [More Information Needed] -->

<!-- ### Downstream Use [optional] -->

<!-- This section is for the model use when fine-tuned for a task, or when plugged into a larger ecosystem/app -->

<!-- [More Information Needed] -->

<!-- ### Out-of-Scope Use
 -->
<!-- This section addresses misuse, malicious use, and uses that the model will not work well for. -->

<!-- [More Information Needed] -->

## Bias, Risks, and Limitations

<!-- This section is meant to convey both technical and sociotechnical limitations. -->

We need to be cautious about a few risks:
* In our evaluation setup, the training and test sets come from the same data distribution (sampled from a larger dataset). If the data distribution changes, the results may not follow the same pattern.
* The datasets used were gathered from publicly available sources. Over time, foundational models may access both the training and test sets, potentially achieving similar or even better results.

Also check the related blogpost:[Link](TODO Link to Blogposts)

<!-- ### Recommendations -->

<!-- This section is meant to convey recommendations with respect to the bias, risk, and technical limitations. -->

<!-- Users (both direct and downstream) should be made aware of the risks, biases and limitations of the model. More information needed for further recommendations. -->

<!-- ## How to Get Started with the Model

Use the code below to get started with the model.

[More Information Needed] -->

 ## Training Details

<!-- ### Training Data --> 

<!-- This should link to a Dataset Card, perhaps with a short stub of information on what the training data is all about as well as documentation related to data pre-processing or additional filtering. -->

<!-- [More Information Needed]-->

### Training Procedure

<!-- This relates heavily to the Technical Specifications. Content here should link to that section when it is relevant to the training procedure. -->
Used RunPod with following setup:

* 1 x A100 PCIe
* 31 vCPU 117 GB RAM
* runpod/pytorch:2.4.0-py3.11-cuda12.4.1-devel-ubuntu22.04
* On-Demand - Secure Cloud
* 60 GB Disk
* 60 GB Pod Volume
* ~16 hours
* $30

<!-- #### Preprocessing [optional]

[More Information Needed]
 -->

#### Training Hyperparameters

<!-- - **Training regime:** -->
<!--fp32, fp16 mixed precision, bf16 mixed precision, bf16 non-mixed precision, fp16 non-mixed precision, fp8 mixed precision -->
* lora_config = LoraConfig(
    r=64,
    lora_alpha=64,
    target_modules=target_modules,
    lora_dropout=0.05,
    bias="none",
    task_type="CAUSAL_LM",
)
* sft_config = SFTConfig(
    dataset_text_field=dataset_text_field,
    per_device_train_batch_size=4,
    gradient_accumulation_steps=8,
    dataset_num_proc=16,
    max_seq_length=1600,
    logging_dir="./logs",
    num_train_epochs=1,
    learning_rate=2e-5,
    save_steps=5,
    save_total_limit=1,
    logging_steps=5,
    output_dir="outputs",
    optim="paged_adamw_8bit",
    save_strategy="steps",
)
<!-- #### Speeds, Sizes, Times [optional] -->

<!-- This section provides information about throughput, start/end time, checkpoint size if relevant, etc. -->

<!-- [More Information Needed] -->

<!-- ## Evaluation -->

<!-- This section describes the evaluation protocols and provides the results. -->

<!-- ### Testing Data, Factors & Metrics -->

<!-- #### Testing Data -->

<!-- This should link to a Dataset Card if possible. -->

<!-- [More Information Needed] -->

<!-- #### Factors -->

<!-- These are the things the evaluation is disaggregating by, e.g., subpopulations or domains. -->

<!-- [More Information Needed]

#### Metrics -->

<!-- These are the evaluation metrics being used, ideally with a description of why. -->

<!-- [More Information Needed]

### Results

[More Information Needed]

#### Summary -->



<!-- ## Model Examination [optional]
 -->
<!-- Relevant interpretability work for the model goes here -->

<!-- [More Information Needed]

## Environmental Impact -->

<!-- Total emissions (in grams of CO2eq) and additional considerations, such as electricity usage, go here. Edit the suggested text below accordingly -->

<!-- Carbon emissions can be estimated using the [Machine Learning Impact calculator](https://mlco2.github.io/impact#compute) presented in [Lacoste et al. (2019)](https://arxiv.org/abs/1910.09700).

- **Hardware Type:** [More Information Needed]
- **Hours used:** [More Information Needed]
- **Cloud Provider:** [More Information Needed]
- **Compute Region:** [More Information Needed]
- **Carbon Emitted:** [More Information Needed]

## Technical Specifications [optional]

### Model Architecture and Objective

[More Information Needed]

### Compute Infrastructure

[More Information Needed]

#### Hardware

[More Information Needed]

#### Software 

[More Information Needed]

## Citation [optional]-->

<!-- If there is a paper or blog post introducing the model, the APA and Bibtex information for that should go in this section. -->

<!-- **BibTeX:**

[More Information Needed]

**APA:**

[More Information Needed]

## Glossary [optional] -->

<!-- If relevant, include terms and calculations in this section that can help readers understand the model or model card. -->

<!-- [More Information Needed]

## More Information [optional]

[More Information Needed]

## Model Card Authors [optional]

[More Information Needed]

## Model Card Contact

[More Information Needed] -->
### Framework versions

- PEFT 0.12.0