# Kaya SLM

Kaya is a ~15M parameter small language model built completely from scratch 
in PyTorch — no HuggingFace Transformers, no pretrained weights, no shortcuts. 
Every component was hand-coded: the attention mechanism, positional embeddings, 
feedforward blocks, residual connections, training loop, and a custom BPE 
tokenizer trained from scratch on the corpus itself.

## Why I built this
I wanted to deeply understand how language models actually work — not just use 
APIs or fine-tune existing ones, but build every single piece from scratch and 
watch a model learn language token by token from random initialization.

## Architecture
| Component         | Detail                          |
|-------------------|---------------------------------|
| Architecture      | Decoder-only Transformer (GPT)  |
| Parameters        | ~15M                            |
| Transformer Blocks| 6                               |
| Attention Heads   | 6 (Multi-Head Self-Attention)   |
| d_model           | 384                             |
| d_ff              | 1536 (4× expansion)             |
| Context Length    | 256 tokens                      |
| Vocab Size        | 8000 (custom BPE tokenizer)     |
| Activation        | ReLU                            |
| Normalization     | LayerNorm                       |
| Dropout           | 0.2                             |

## What was built from scratch
- Causal self-attention with masking
- Multi-head attention projection
- Feedforward blocks with residual connections
- Token + positional embeddings
- BPE tokenizer trained on TinyStories corpus (vocab 8000)
- Full training loop with AdamW, gradient clipping, LR scheduling
- Checkpoint saving and resuming from Drive

## Training
| Phase        | Detail                                          |
|--------------|-------------------------------------------------|
| Dataset      | TinyStories — 2.1M stories (roneneldan/TinyStories) |
| Pretraining  | Cross-entropy next-token prediction             |
| Fine-tuning  | 404 instruction-formatted story pairs, 4 epochs |
| Hardware     | NVIDIA T4 (Google Colab free tier)              |
| Framework    | PyTorch                                         |
| Optimizer    | AdamW (lr=5e-5, weight_decay=0.01)              |

## Loss Curve
| Epoch | Avg Loss |
|-------|----------|
| 1     | 3.4576   |
| 2     | 2.1380   |
| 3     | 1.6751   |

Loss dropped from **4.94 → 1.67** across training — a clean, steady 
convergence with no instability, trained entirely on free-tier hardware.

## Sample Output
**Prompt:** "Once upon a time, a brave little owl lived in a misty forest. One day,"

**Output:** "a little bird named Polly flew to the owl and said, 'Can you talk?' 
The owl was very surprised. He saw Tweetie looking sad and asked her what 
happened. Together they searched high in a tall tree until they finally 
found their way home."

## Author
Aditya | B.Tech CSE  | Teerthanker Mahaveer University, 2027  
AI Engineer @ The Aghron Forum  
GitHub: github.com/adityatiwari049

Linkedin : https://www.linkedin.com/in/adityatiwaryman7/
