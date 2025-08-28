 # Musical Embedding to search and compare songs


 Used the tokenizer from Meta's [musicgen](https://arxiv.org/abs/2306.05284 "Simple and Controllable Music Generation
") paper, [EnCodec](https://arxiv.org/abs/2210.13438 "High Fidelity Neural Audio Compression")

This can be used to turn songs into vectors with latent meanings, allowing for numerical comparisons. The notebook [![Tests](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1QdDaOKfA511GYTFcLeIPoXlAHUyYv3Rf?usp=sharing/] describes my methods for optimizing and researching different comparison methods. The best seems to be Dynamic Time Warping, a way of comparing time-series data without it necessarily being compared one-to-one. 

Then, I used Gradio to create a web app that would test and compare songs with a complete UI and a simple UX. It allowed for much easier tests. To run this app, try this notebook :  [![Music Demo](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1dNkSbyZalexnFI3QZ7aJErE22YEZ5pkH?usp=sharing]