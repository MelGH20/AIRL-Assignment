# AIRL-Assignment
# Vision Transformer on CIFAR-10 (Colab)

How to run in Colab:
1. Upload this file to Colab or paste the cells into separate notebook cells.
2. Run cells in order. Make sure Runtime > Change runtime type > GPU.


Best model config (example):
- image_size=32, patch_size=4, embed_dim=256, depth=8, num_heads=8
- optimizer: AdamW lr=3e-4, weight_decay=0.05
- epochs: 60, batch_size: 256


Tiny results table (example):
| Model | Epochs | Val Accuracy |
|---|---:|---:|
| ViT (above) | 60 | ~0.86 (example — your run may vary) |


Analysis:
- Patch size tradeoffs: smaller patches (4x4) increase token count and may help on small images but increase compute. Larger patches (8x8) reduce tokens but lose locality.
- Depth/width: increasing depth helps if model capacity matches dataset; width (embed_dim) grows parameter count faster and helps if overfitting controlled with augmentation and weight decay.
- Augmentations: random crop + flip + normalization helped substantially. Consider RandAugment / CutMix for further gains.
- Optimizer/schedule: AdamW + cosine annealing worked well; a warmup can stabilize training for larger LR.
- Overlapping patches: using stride < patch_size can add overlapping context but increases tokens and compute.


