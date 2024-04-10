---
title: Information theory basics
date: 2024-04-08
tags:
  - evergreen
enableToc: false
---

In this webpage, we will be talking about the basics behind information theory. Before you start, you need to have basic understanding of probability theory and [[notes/distribution|distributions]]. This page is crucious to understand the basics of how any neural network **can** model any distribution.


## Entropy

Entropy is a measure of the uncertainty associated with a random variable. It is a measure of the average amount of information produced by a stochastic source of data. The concept of entropy was introduced by Claude Shannon in his 1948 paper "A Mathematical Theory of Communication".

$$ H(X) = - \sum_{x \in X} p(x) \log P(x) $$

where $H(X)$ is the entropy of the random variable $X$ and $P(x)$ is the probability mass function of $X$.

**Example of [[notes/distribution#Bernoulli distribution|Bernoulli distribution]]**

$$ H(X) = - p \log p - (1-p) \log (1-p) $$

**Now why does this term mean entropy?**

The name entropy comes from thermo-dynamics. In thermo-dynamics, entropy is a measure of the disorder of a system. In information theory, entropy is a measure of the uncertainty of a random variable. 

The logarithm provides a lot of intresting combinations which map to how data is representing. The base of the logarithm is usually 2 but this can be changed to match any role. a base 2 uses bits, a base 10 uses dits, base 256 uses bytes and a base $e$ uses nats (information content of an event when the probability is $\frac{1}{e}$ ).

## Properties

* Entropy is always positive or zero. It is zero when the random variable is deterministic.

* Entropy is maximized when all outcomes are equally likely. This is because the entropy is a measure of uncertainty and when all outcomes are equally likely, the uncertainty is maximized.

* Entropy is minimized when one outcome is certain. This is because the entropy is a measure of uncertainty and when one outcome is certain, the uncertainty is minimized.

* Entropy is additive. This means that the entropy of the sum of two random variables is the sum of the entropies of the two random variables. $$ H(X,Y) = H(X) + H(Y) $$

* Permutation invariance. The entropy of a random variable is invariant under permutations of the outcomes of the random variable. This means that the entropy of a random variable is the same as the entropy of the random variable with the outcomes permuted.

* Subadditivity. The entropy of the sum of two random variables is less than or equal to the sum of the entropies of the two random variables. $$ H(X+Y) \leq H(X) + H(Y) $$

This properties are nice, but what happens if i have two functions how do i measure the information content of the two functions? 

### Simple explanation 

Let us assume, you are a weather outpost and you have to send an message to the weather station. 

* If the message can be "sunny" or "rainy", then the entropy is 1 bit.
* If the message can be "sunny" or "partially sunny" or "partially rainy" or "rainy", then the entropy is $\log_2(4)$ = 2
* Let is now take the examples where the sunny and rainy is a probability distribution:
    * If the message can be "sunny" with 0.75 probability and "rainy" with 0.25 probability. You get a message rainy, then the number of bits you require is 2 bits(1/4 possible outcomes). If you message as sunny, then you require 0.41 bits(3/4 possible outcomes). The average number of bits required is:
     * When it is sunny = P(sunny)* Bits(of sunny) =  $0.75 * 0.41$
     * When it is rainy = P(rainy)* Bits(of rainy) =  $0.75 * 2$
     * Average bits = $0.75 * 0.41 + 0.25 * 2 = 0.81$ bits
     * This means if you stay in Doha the average number of bits required to send a message is lower as it is always sunny but in Seattle where the weather is unpredictable, you require more bits to send the message.
     * This is called Cross-Entropy

* If the message "sunny" or "partially sunny" or "partially rainy" or "rainy" with probabilities 0.40, 0.30, 0.20, 0.10 respectively. Let us assume, you have telekenis. You can accuratly know the number of bits required. You calculate that $0.4\log(0.4) + 0.3\log(0.3) + 0.2\log(0.2) + 0.1\log(0.1) $ = 1.84 bits. But you are computer, you have to represent it as binary so you send 2 bits (00 for sunny, 01, partially sunny, 10 for partially rainy and 11 for rainy). This is your cross-entropy. Therefore your telekenis is saving 0.16 bits. This is called Kullback-Leibler divergence.
    

## Mutual Information

Mutual information is a measure of the amount of information that one random variable contains about another random variable. It is a measure of the reduction in uncertainty of one random variable due to the knowledge of another random variable.

Geometric meaning: "mutual information as distance to product distributions"

> You and your wife got a message, you have to respond together. Your message was 2 bits long and your wife's message was 3 bits long. sus. You notice that the message is similar. Being a nerd, you know that 0.75 bits is shared ( This is called mutual information). Now you both respond with 4.25 bits (This is the entropy). Both happy jpeg.

Some properties of mutual information:
* Symmetry: $I(X;Y) = I(Y;X)$
* Non-negativity: $I(X;Y) \geq 0$
* The amount of entropy reduction is the mutual information between the two random variables. $H(Y|X) - H(X) = I(X;Y)$

Now, we have two cases where the mutual information:
*  $P_{Y|X} → max( I(X;Y))$ is the capacity of the set of distributions
*  $P_{X} → min( I(X;Y))$ is the lossy compression

Now the natural question is, how do we maximize the capacity? The key point here is the data mirrors the prediction, we have no noise. Maximizing the capacity. From this, we can naturally say that a medium where we are receiving hardly any noise and maximizing the information, we are maximizing the capacity.

Another intutive way to relate to ML is the difference between cross entropy to KL divergence. **Cross entropy is the average number of bits required to send a message, KL divergence is the number of bits saved if you know the distribution.**

#### Data Processing Inequality


**Post-processing cannot increase information**

Data processing inequality is an information theoretic concept that states that the information content of a signal cannot be increased via a local physical operation. This can be reffered as the "intrinsic information" of the signal. It is not necessary, we are able to decipher the message, but the information content of the message is not changed. (Skill Issue)

In real life, we come across multiple examples of the opposite. Data processing helps us to decipher the message. So post processing can "increase" the information content, but this is an miss-understanding. The information content of the message is not changed, but you ability to decipher the message is increased(skill issue). This is a change in a relative basis, not an absolute basis.

If we have a basic markov chain, $ X \to Y \to Z$, i.e $Z$ and $Y$ contain the same information about $X$.

$$ {\displaystyle I(X;Y)\geqslant I(X;Z),} $$

A natural conclusion of this is noise inside a channel $P_{Y|Z}$ must reduce the information that Y carries about the data X, regardless of how smart the look up X → Y is.


## Capacity = information radius



## Extremization of mutual information for memoryless sources and channels

## Information measures and probability of error, corresponding rates

## Optimal compressor

## Slepian worlf coding

## Compression with Side Information at both compressor and decompressor

## Arithmetic coding

## Optimal compressors for a class of sources

## Redundancy

## Information Projection

## Sanoc theorem

## Energy per bit

## Normalized bit

## Lossy compression

## Scalar quantization

## Distortion problems


## Convexity 

Convex set is defined as the subset S of some vector space which is convex if $ x,y \in S \implies \lambda x + \alpha y \in S$ for all $0 \leq \lambda \leq 1$.

Convex functions: $f : S \to \mathbb{R}$ is:
* Convex if $f(\alpha_1 x + \alpha_2 y) \leq \alpha_1 f(x) + \alpha_2 f(y)$ for all $x,y \in S$ and $0 \leq \alpha \leq 1$.
* Strictly Convex if $f(\alpha_1 x + \alpha_2 y) < \alpha_1 f(x) + \alpha_2 f(y)$ for all $x,y \in S$ and $0 \leq \alpha \leq 1$.
* Strictly concave if $-f$ is strictly convex.


## Jensen's inequality

If $f$ is convex, then $f(E[X]) \leq E[f(X)]$ for any random variable $X$.

Essentially, the left side is the average input and right side the average output. This theorem says that for a convex functions the average input is always less than or equal to the average output.

Think of a graph which is a simple $ y=x$ line. The average input is the average of the x-axis and the average output is the average of the y-axis. As of right now, moving the line up or down will not change the average outputs scale.

Now as you bend it, the average input will be the same, but the average output will be pushed up. When we bend it more (higher curvature), the differences will increases.

There is a very funny example of this:

> \> Man walks into the bar. \
> \> Says to the bartender, "One average drink for the average height and weight man" \
> \> Everyonelaughing.jpeg \
> \> The bartender says "You are a little fat" \
> \> Bro doesn't know why, doesn't realize weight is related to volume. Volume is roughly the third power of height. So if you are taller, you are expected to be way more heavier \
> \> Realizes the joke and laughs "I am not fat, I am just convex" 

## References

* [Jensen's inequality](https://truetheta.io/concepts/machine-learning-and-other-topics/jensens-inequality/)