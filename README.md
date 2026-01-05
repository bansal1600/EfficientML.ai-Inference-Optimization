# EfficientML.ai-Inference-Optimization
This repo contains all my notes &amp; project for building LLM more efficient
1. Lecture-1 (https://www.youtube.com/watch?v=6cAmS-_vEh8&list=PL80kAHvQbh-pT4lCkDT53zT8DKmhE0idB&index=2)
  *  the growing gap between AI computing demand and hardware supply, necessitating techniques like:
      * Model compression by exploiting sparsity and quantization.
      * Efficient inference hardware and systems to run compressed models directly.
   
  * Language Models: Highlighting the power and computational intensity of Large Language Models (LLMs) like ChatGPT, discussing techniques to scale up (distributed training) and scale down (faster inference) deep learning. It introduces Light Transformer and quantization techniques to reduce model size for tasks like neural machine translation, and explains zero-shot and few-shot learning capabilities of LLMs and their computational cost. The video illustrates Chain of Thought prompting to make LLMs smarter without retraining, and showcases the immense cost of training LLMs and the need for efficient computing due to rapidly outdated hardware. It also introduces static sparse attention and token pruning to remove redundant words in sentences for efficiency, and demonstrates running LLaMA 7B parameter models on a MacBook Air using 4-bit quantization and efficient inference engines, mentioning the TinyChat open-source project for local LLM deployment.

2. Lecture 2 (https://www.youtube.com/watch?v=ieg0RJb7TeI&list=PL80kAHvQbh-pT4lCkDT53zT8DKmhE0idB&index=4)

