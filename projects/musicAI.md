 # Musical Embedding to search and compare songs


 Used the tokenizer from Meta's [musicgen](https://arxiv.org/abs/2306.05284 "Simple and Controllable Music Generation
") paper, [EnCodec](https://arxiv.org/abs/2210.13438 "High Fidelity Neural Audio Compression")

This can be used to turn songs into vectors with latent meanings, allowing for numerical comparisons. The notebook [![Tests](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/weiji14/deepbedmap/] describes my methods for optimizing and researching different comparison methods. The best seems to be Dynamic Time Warping, a way of comparing time-series data without it necessarily being compared one-to-one. 

