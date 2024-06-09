---
title: Information Indexing
date: 2024-06-09
---


> Looking for good content in a world where machines can mass produce content 

In this page, i have some disparate notes on information indexing and how smarter LMs break the traditional search engine paradigm. I have recently been puzzled how would search look in a world where information is vast but attention is not. Recent advancements in LLMs have made me question the traditional search engine paradigm can even survive with the sparsity of concentration. We have to think what is means to search and who/what are we searching. This post will go through how would an ideal search system look like regardless of the consumer, what makes the search system special for us and then finally how would you model a search system that is 


As someone who works in item search, it is seemingly trivial when you have a fixed index and safeguards in place to ensure quality. However, the world is not so simple. The web is a hivemind of rouge ai's and cognitive human thoughts wrapped with exabytes of data waiting to be indexed.  

Dive deeper into the world of information retrieval, plung into the depths of the web, drop your anchors of abilities limited by reality and experience life through artificiality of the web.


![Cyberpunk netrunner](lucy.png)
> Obligatory cyberpunk netrunner image

## Arbitrator of truth

Relevance is defined as when an object (link, website, item and truth) is thought as relevant to the needs of the user. Thus the arbitrator of truth is the user. The user is the one who decides what is relevant and what is not. This opens a pandora's box of oppurtunities and problems, as the user is not a single entity but a collective of individuals with different needs and wants. 

Even though two user can submit the same query, the assesments of the truth can be widely different. The relevance for each document can change when the user's needs change. You can think of search being *reflexive*. **Every query changes the user and the user changes the systems understanding of the query**.

How would you model a structure of a space and what conditions would you impose to ensure the space represents this underlying structure? 

## Divide and Conquer

Let us break the whole system into smaller parts. We can think of the system as a series of interconnected parts that work together. From the five axiom theory, we get the following axioms:

1. Definability:
   * The compilation of responses relevant to a topic can be delegated only to the extent to which the inquirer can define the topic in terms of concepts and concept relations.
2. Order: 
   * Any compilation of responses relevant to a topic is an order-creating process. 
3. Sufficient degree of order:
   * The demands made on the degree of order increase as the size of the collection andlor the frequency of searches increases. 
4. Representational predictability: 
   * The accuracy of any directed search for relevant texts (especially the recall ratio) depends on the predictability of the modes of expression for concepts and concept relations in the search file.
5. Representational fidelity: 
   * The accuracy of any directed search for relevant texts (especially the precision ratio) depends on the fidelity with which concepts and concept relations are expressed in the search file.



## References 

[The Geometry of information retrieval](https://www.semanticscholar.org/paper/The-geometry-of-information-retrieval-Rijsbergen/99614334a3e9b809e43384777409af7eccde3db6)

[The Five Axiom Theory of Indexing and Information Supply](https://www.semanticscholar.org/paper/The-five-axiom-theory-of-indexing-and-information-Fugmann/4735408f352a59dc1b925e6909af8f9db4675726)