---
title: "Implement a sentence completion feature using GPT"
date: 2024-01-01
tags: [AI, AutoComplete, GPT]
---
# Purpose
Implement a feature that predicts the next word in a sentence based on the user's input using LLM.

# Background
Apple's CoreML framework can be used to run large language models (LLMs) on iOS devices. This requires some pre-processing steps.

# Model introduction
There are two ways to introduce a model into CoreML.

- Model conversion:
  - Use the coremltools.convert() function.
  - May require additional steps depending on the model type.
  - Experimental and may not be stable.

- Model reproduction:
  - Use the coremltools.neural_network.builder function.
  - Requires manually configuring the neural network.
  - Allows for more fine-tuning.
  - More complex to implement.

# Preparation
1. To get an NLP model, search for a model on the Hugging Face: https://huggingface.co/models website.
2. Choose a text generation type OpenAI gpt2 model.
3. Install the Python, PyTorch, TensorFlow, Transformers, and Jupyter Notebook tools.

# Implementation

## Model conversion

1. Import the Model
```python
from transformers import GPT2LMHeadModel
```

2. Declare a function for input/output
```python
class FinishMySentence(torch.nn.Module):
def __init__(self, model=None, eos=198):
super(FinishMySentence, self).__init__()
self.eos = torch.tensor([eos])
self.next_token_predictor = model
self.default_token = torch.tensor([0])

def forward(self, x):
sentence = x
token = self.default_token
while token != self.eos:
predictions, _ = self.next_token_predictor(sentence)
token = torch.argmax(predictions[-1, :], dim=0, keepdim=True)
sentence = torch.cat((sentence, token), 0)

return sentence
```

3. Pre-process model
```python
token_predictor = GPT2LMHeadModel.from_pretrained("gpt2", torchscript=True).eval()
random_tokens = torch.randint(10000, (5,))
traced_token_predictor = torch.jit.trace(token_predictor, random_tokens)
model = FinishMySentence(model=traced_token_predictor)
scripted_model = torch.jit.script(model)
```

4. Convert model
```python
mlmodel = ct.convert(
scripted_model,
# Range for the sequence dimension to be between [1, 64]
inputs=[ct.TensorType(name="context", shape=(ct.RangeDim(1, 64),), dtype=np.int32)],
)
```

This could lead us to error below. So we switch to Model reproduction
```python
ValueError: Op "136" (op_type: fill) Input shape="135" expects tensor or scalar of dtype from type domain ['int32'] but got tensor[0,fp32]
```

## Model reporoduction

1. Get the model
```python
lm_head_model = GPT2LMHeadModel.from_pretrained("gpt2")
model = lm_head_model.transformer
```

2. Create builder
```python
builder = neural_network.NeuralNetworkBuilder(
    input_features,
    output_features,
    mode=None,
    disable_rank5_shape_mapping=True,
)
```

3. Create Model
```python
mlmodel = coremltools.models.MLModel(builder.spec)
```

## Model tuning
- Adjust sequence length, neural network generation.
- Adjust bias and weight.
- Adjust topK and number of tokens for inference.

# Applying CoreML Model
## Preparation
Import the created CoreML model into the Xcode project. 
Add token resources for tokenizing.

## Implementation
Use an incomplete sentence as input for model inference. 
Select one word from the candidates and use it as output. 
Add the output value to the incomplete sentence and repeat the inference.

## Conclusion
There are various tools supporting the ecosystem for NLP introduction, such as HuggingFace and JupyterNotebook, making it relatively easy. 
There may be frequent build failures depending on the versions of each library. It is important to establish an isolated environment when creating the model. 
For CoreML, there is a lack of resources, which may lead to spending a long time resolving issues.

## References
[Converting a Natural Language Processing Model](https://coremltools.readme.io/docs/convert-nlp-model)

[coremltools - neural_network.builder](https://apple.github.io/coremltools/source/coremltools.models.neural_network.html)

[swift-coreml-transformers](https://github.com/huggingface/swift-coreml-transformers)



