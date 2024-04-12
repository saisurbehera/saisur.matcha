---
title: Compression
date: 2024-04-11
tags:
  - sapling
enableToc: false
---

> My 🥰 favorite part of information theory 🥰

The main engineering goal of compression is to represent a given any sequence $x_i, x_2, \ldots, x_n$ with fewer bits than the original sequence. The main idea is to remove redundancy in the data. Reducing the number of bits is generally impossible, unless the source imposes certain constraints on the data. 

A simple example of this is the english language. If we see two different novels, model the distribution of the alphabet in both novels, we can see that the distribution of the alphabet is similar in both novels. This is because the english language has a certain structure and the distribution of the alphabet is similar in most cases. The goal of compression is to exploit this "similarity".

There are three main types of compress for a random variable $X$:
* Lossy compression: The original data can be perfectly reconstructed from the compressed data. $ X \to W \to \hat{X}$, this would imply $E[(X - \hat{X})^2] \leq$ distortion. Distortion can be thought as the error in the reconstruction.
* Lossless compression: The original data can be perfectly reconstructed from the compressed data. $ X \to W \to \hat{X}$, this would imply $X = \hat{X}$.
* Near-lossless compression: The original data can be approximately reconstructed from the compressed data. $ X \to W \to \hat{X}$, this would imply $E[(X - \hat{X})^2] \leq \epsilon$.

## Fixed Length almost lossless compression



