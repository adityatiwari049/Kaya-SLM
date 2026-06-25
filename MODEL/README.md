# Kaya SLM

A small language model (~10M parameters) built from scratch using a GPT-style decoder-only transformer architecture, trained on the TinyStories dataset.

## Architecture
- Parameters : ~10M
- d_model     : 384
- Layers      : 6
- Heads       : 6
- Vocab Size  : 8000 (custom BPE tokenizer)
- Context Len : 256 tokens

## Training Data
[roneneldan/TinyStories](https://huggingface.co/datasets/roneneldan/TinyStories)

## How to Load
```python
import torch
from tokenizers import Tokenizer

tokenizer = Tokenizer.from_file("tokenizer.json")

# initialize your model class first, then:
model.load_state_dict(torch.load("kaya_weights.pt", map_location="cpu"))
model.eval()
```

## Author
Aditya | B.Tech CSE (Data Science) | TMU 2027
