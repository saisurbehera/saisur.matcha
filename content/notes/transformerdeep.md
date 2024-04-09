---
title: Transformers from first principles
date: 2024-04-07
tags:
  - evergreen
enableToc: false
---

In this page, we will implement [Attention is all you need](https://arxiv.org/pdf/1706.03762.pdf), from scratch. This is a very simple implementation and is not optimized for speed. The goal is to understand the architecture of the transformer. If you are a basic understanding of linear algrebra and python, you should be able to follow along.

Subcomponents of the transformer which need to be coded out in seperate sections:

## Architecture
* [[notes/layerexplain|Layer]]
    * [[notes/layerexplain#Kaiming initialization |Kaiming Initialization]]
* Feed Forward network 
* Attention Block
* Self Attention Block
* Multi Head Attention Block
* Embedding Layer
* Positional Encoding
* Layer normalization
* Batch normalization
* Activation functions
* Masking
* Dropout
* Encoder
* Decoder
* Transformer
* Tokenizers

## Training
* Optimizers
* Loss functions
* Regularization
* Weight decay
* Learning rate schedulers

## Decoding
* Beam search
* Greedy search
* Temperature sampling
* Evaluation metrics

>  I am speed. - Lightning McQueen

### Deep Learning go brrrrrrr
* Gradient Checkpointing
* Mixed Precision Training
* Distributed Training
    * Model Parallelism
    * Data Parallelism
* Quantization
* Pruning
* Knowledge Distillation
* Transfer Learning
* Fine Tuning
* Pretraining

There are several topics which are required to have a basic **intution** about why is it learning. Here are some topics, I will be covering which go behind why does this blob of code learn:

* [[notes/inftheory|Information Theory]]
* [[notes/distribution|Distributions]]
