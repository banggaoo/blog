---
title: "Creating a question bot with open source LLM Llama 2"
date: 2023-07-21
tags: [AI, LLM]
---
## Background
Recently, Meta released the latest LLM Model, [Llama 2](https://ai.meta.com/llama/)
It is a hot topic with a license that can be used for commercial purposes.

## Goal
Try Llama 2

## Preparation
### Get approval to use the Model
Go to Meta’s [Use request page](https://ai.meta.com/resources/models-and-libraries/llama-downloads/)
Once approved, model can be downloaded

### Building a development environment
Use the Hugging Face platform for application development
Go to the [Model page](https://huggingface.co/meta-llama/Llama-2-7b-chat-hf) and request access to Hugging Face using the email address you entered when requesting to use the model.
Install PyTorch, Transformers

### CLI preparation
[Issuance of Hugging Face access token](https://huggingface.co/settings/tokens)
Install Hugging Face CLI. Enter token when installing

## Implementation
Using Hugging Face sample code

### Write code
```python
from transformers import AutoTokenizer
import transformers
import torch

# Llama import
model = "meta-llama/Llama-2-7b-chat-hf"

tokenizer = AutoTokenizer.from_pretrained(model)

# Create inference pipeline
pipeline = transformers.pipeline(
     "text-generation",
     model=model,
     torch_dtype=torch.float16;
     device_map="auto",
)

# input part
sequences = pipeline(
     'What is Entropy?',
     do_sample=True;
     top_k=10;
     num_return_sequences=1;
     eos_token_id=tokenizer.eos_token_id,
     max_length=200;
)

# output part
for seq in sequences:
     print(f"Result: {seq['generated_text']}")
```

### Execution and Verification
Execute the above code in the CLI environment to download the model and run inference
Check answers according to questions in the input section
```shall
llama-hf %python3 hf.py
Loading checkpoint shards: 100%|██████████████████| 2/2 [00:21<00:00, 10.80s/it]
Xformers is not installed correctly. If you want to use memory_efficient_attention to accelerate training use the following command to install Xformers
pip install xformers.
/opt/homebrew/lib/python3.11/site-packages/transformers/generation/utils.py:1270: UserWarning: You have modified the pretrained model configuration to control generation. This is a deprecated strategy to control generation and will be removed soon, in a future version. Please use a generation configuration file (see https://huggingface.co/docs/transformers/main_classes/text_generation )
   warnings.warn(
Result: What is Entropy?

Entropy is a measure of disorder or randomness in a system. It is a fundamental concept in thermodynamics and statistical mechanics, and it has many applications in science and engineering. In this answer, we will explore the concept of entropy, its definition, types, and examples.
What is Entropy?

Entropy is a measure of the amount of thermal energy unavailable to do work in a system. In other words, it is a measure of the amount of energy that is "lost" as a result of friction, heat transfer, and other inefficiencies in a system. The second law of thermodynamics states that the total entropy of a closed system will always increase over time, which means that the amount of energy available to do work will always decrease over time.
Entropy can be defined in terms of the number of microstates in a system. A microstate is a specific arrangement of
```
For Mac, [MPS compatibility issue](https://developer.apple.com/metal/pytorch/) may occur, which can be resolved by installing the prerelease version of PyTorch.

## Evaluation
Even the 7B model with the fewest parameters shows not bad performance. For the 70B model, it is said to be at GPT 3.5 level.
In the case of the 7B model, it is not difficult to run inference in M2 Max MacStudio. Hardware acceleration support

[Llama 2 Demo](https://huggingface.co/chat/)
[Implementation of sentence auto-completion function using GPT](https://banggaoo.github.io/blog/2024/01/01/Implement_sentence_completion_using_GPT.html)
