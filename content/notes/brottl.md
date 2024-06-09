---
title: Brotli Compression 
date: 2024-05-09
---



## Parts of the paper
> This choice is motivated by the fact that the distribution of the frequency of a symbol is strongly influenced by its kind (whether it is a length, a distance, or a literal), its context (i.e., its neighboring symbols), and its position in the text. Briefly (since we will give further details in the next sections), each meta-block stores in the header the collection of Huffman codes that are used to compress the commands contained in its data part.

length, distance, and literal.


> For example, if the files to be compressed have mixed content (such as HTML pages, JSON snippets, etc.), then block boundaries might mark the beginning and the end of the different homogeneous parts, and clustering could group together file parts that express homogeneous content spread all around these files.

> For lengths, all values laying in blocks with the same block id are encoded using the same huffman code. For distances and literals, the choice of the huffman code to use does not depend solely on the block id but also on their context, so each cluster of blocks employs not just one huffman code but a set of huffman codes of canonical type,


> substrings that are equal except for small differences such as substitution, insertion, or deletion of few characters

> Brotli then deploys relative (copy) distances which express the delta between the current copy- distance and the previous copy-distance in the compressed stream. In this way a run of slightly different distances in the compressed stream is changed into a run of relative distances, which should take less compressed space.

> short copies do typically occur close to the current position to be matched, whereas long copies are typically found farther in the input text

> This implies that small distances have higher frequencies than long distances, but the latter typically refer to longer copies than the former. In terms of space occupancy, this means that far&long copies are able to amortize the bit cost incurred by long distances because they squeeze long phrases


In summary, any reference to the dictionary is represented as a triplet that
specifies the length of the copy (between 4 and 24), the index of the dictionary word
(according to the previously mentioned escape values), and the index of the word
transformation to be applied.

