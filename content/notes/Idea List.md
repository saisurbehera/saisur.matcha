---
title: Idea List
date: 2023-10-04
tags:
  - dreams
enableToc: false
---
Open ideas, if you would want to collaborate on any of these, please let me know. I have done some progress in them but not detailed enoughs


- Light L16 stiching algorithm
	- Replace the method of laplacian blending with a more advanced method. Specifically try Alpha blending and cyclendrical blending
- Automatic Minecraft Player and Crafter
	- Show videos of builds and recreate them in your world 
- Nvidia Omniverse 3D asset creation
	- Create a 3D assets and place it in a 3d Location 
	- Programatic world generation
	- Sora doesn't follow geometries, omniverse can help fix
- Objaverse Search
	- 3D asset search is broken. It doesn't have any open source ranking algorithm.
- RAG at scale 
	- Problem: RAG doesn't scale well. The embeddings overlap and the search return non-relevant results 
- Tokenizer:
	- BPE has [some](https://gwern.net/gpt-3#bpes) [limitations](https://arxiv.org/pdf/2403.00417.pdf). A particularly common word may get a unique BPE while a longer word will be encoded as 2 or 3 BPEs, and a completely novel word will be encoded by letter BPE as a fallback. 
	- Read some blogs from Gwern, [Karpathy](https://twitter.com/karpathy/status/1657949234535211009) and [Nostalgebraist](https://nostalgebraist.tumblr.com/post/189212709059/bpe-blues)
	- A lot of ideas to borrow from the hutter prize.
	- Train couple of GPT models with different tokenizers and see how they perform. [100$](https://tomekkorbak.com/2022/10/10/compute-optimal-gpt2/) per run.