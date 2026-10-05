---
layout: default
title: Musical Embeddings
permalink: /projects/musicAI.html
---

[All projects]({{ '/projects/' | relative_url }})

# Musical Embeddings to Search and Compare Songs

I used [EnCodec](https://arxiv.org/abs/2210.13438 "High Fidelity Neural Audio Compression"), the audio tokenizer used in Meta's [MusicGen](https://arxiv.org/abs/2306.05284 "Simple and Controllable Music Generation"), to turn songs into vectors for numerical comparisons.

The research notebook describes my methods for optimizing and researching different comparison methods. The best approach I found was Dynamic Time Warping, a way of comparing time-series data without requiring a one-to-one alignment.

[![Open research notebook in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1QdDaOKfA511GYTFcLeIPoXlAHUyYv3Rf?usp=sharing)

I then used Gradio to create a web app for testing and comparing songs through a simple interface. To try the app, run the demo notebook:

[![Open music demo in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1dNkSbyZalexnFI3QZ7aJErE22YEZ5pkH?usp=sharing)
