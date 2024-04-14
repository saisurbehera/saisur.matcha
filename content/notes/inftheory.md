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

The mutual information can be understood as the expectation of the KL divergence.

#### Data Processing Inequality


**Post-processing cannot increase information**

Data processing inequality is an information theoretic concept that states that the information content of a signal cannot be increased via a local physical operation. This can be reffered as the "intrinsic information" of the signal. It is not necessary, we are able to decipher the message, but the information content of the message is not changed. (Skill Issue)

In real life, we come across multiple examples of the opposite. Data processing helps us to decipher the message. So post processing can "increase" the information content, but this is an miss-understanding. The information content of the message is not changed, but you ability to decipher the message is increased(skill issue). This is a change in a relative basis, not an absolute basis.

If we have a basic markov chain, $ X \to Y \to Z$, i.e $Z$ and $Y$ contain the same information about $X$.

$$ {\displaystyle I(X;Y)\geqslant I(X;Z),} $$

A natural conclusion of this is noise inside a channel $P_{Y|Z}$ must reduce the information that Y carries about the data X, regardless of how smart the look up X → Y is.


#### Capacity = information radius

This is the maximum amount of information (usually measured in bits per second) that can be transmitted through a channel, given the limitations imposed by noise and other impairments. The formal definition of channel capacity $C$ is given by the maximum mutual information between the input and output of the channel.

$$ C = \max_{P_{X}} I(X;Y) $$

where $P_{X}$ is the input distribution of the channel and $I(X;Y)$ is the mutual information between the input and output of the channel. In summary what is a distribution that maximizes the mutual information between the input and output of the channel.

Capacity can be thought as the radius of the set of distributions where distances are measured in terms of divergence. Another way to think about this is the radius of the small divergence ball that encompasses all distribution.

Now, one natural question comes is for what input we get the maximum mutual information. A input distribution $P_x$ that results in the maximum mutual information between the input and output of the channel is called the *capacity achieving input distribution*.

Some real life examples are:
* **Binary Symmetric Channel (BSC)**: For a binary symmetric channel with bit-flip probability $p$, the capacity-achieving input distribution is when each input bit (0 or 1) is equally likely (i.e., each has a probability of 0.5). This maximizes the mutual information between the input and the output.
* **Additive White Gaussian Noise (AWGN) Channel**: For an AWGN channel, where the noise added to the signal is Gaussian, the capacity-achieving input distribution is a Gaussian distribution. The mean and variance of this distribution depend on the power constraints of the channel.

#### Shanon Limit 

The Shannon limit is the theoretical maximum rate at which data can be transmitted over a communication channel without error. 

$$ C = B \log_2(1 + \frac{S}{N}) $$

where $C$ is the channel capacity, $B$ is the bandwidth of the channel, $S$ is the signal power, and $N$ is the noise power. This makes a lot of intutive sense, the more the bandwidth, the more the information that can be transmitted. The more the signal power, the more the "value" information that can be transmitted. The more the noise power, the less the "mutual" information that can be transmitted.



## Products Channels and Sources

The distinction between the behavior of mutual information in a system with a **product channel** and one with a **product source** reflects fundamentally different aspects of how information is processed and transmitted in information systems. To explore this, let's differentiate the concepts and contextualize their implications in terms of information theory.

### Product Channel

A **product channel** consists of multiple independent sub-channels where the input $X$ can be split into separate components $X_1, X_2, \dots, X_n$ that are transmitted independently through respective sub-channels to outputs $Y_1, Y_2, \dots, Y_n$. The key property here is that each sub-channel functions independently of the others, leading to the mutual information between the overall input and output being the sum of the mutual information of the individual pairs:

$$ I(X; Y) = I(X_1; Y_1) + I(X_2; Y_2) + \dots + I(X_n; Y_n) $$

This setup maximizes the overall mutual information by maximizing each component independently, reflecting an optimal use of the channel capacity without interference.

### Product Source

A **product source**, on the other hand, refers to a scenario where the source itself produces outputs that are statistically independent across its components. Here, $X = (X_1, X_2, \dots, X_n)$ is such that each component $X_i$ is generated independently of the others. The key focus for a product source relates to how the source's independence properties influence the design and choice of the channel for minimizing mutual information, particularly in contexts like privacy, security, or noise minimization.

### Mutual Information Minimization in Product Source

When it comes to a product source, the goal might shift towards minimizing mutual information for various reasons, such as ensuring privacy or reducing predictability of the transmitted information from the observed output. The statement, "For a product source, the MI-minimizing channel is a product channel," implies that:

1. **Preservation of Independence**: Using a product channel maintains the independence of the components of the input in the output. Since each $X_i$ is processed independently, the outputs $Y_i$ derived from them through the channel do not introduce any new dependencies among the components. This is crucial in scenarios where the addition of inter-component dependencies could inadvertently increase mutual information.

2. **Channel Design**: If the objective is to minimize mutual information (perhaps to obscure the data or protect privacy), designing the channel such that it respects the independence of the source components and does not allow for cross-channel influences is vital. This could mean, for example, using noise addition or other transformations that treat each $X_i$ independently, thus ensuring that any information leaked through the channel does not compound through interactions between different components.

### Practical Example

In a security-sensitive communication system, suppose a device sends multiple types of data (e.g., location, temperature, user activity) separately. If privacy is a concern, designing the transmission channel to treat each type of data independently (product channel) ensures that an eavesdropper learning about one type of data (say, temperature) gains no information about the other types (like location or activity), thus minimizing the total mutual information leakage across these diverse data streams.

In summary, while the product channel maximizes mutual information by exploiting independence to enhance channel capacity, a product source paired with a product channel can be used strategically to minimize mutual information, thereby reducing the amount of information an eavesdropper can infer about the original source data from the channel output. This dual approach highlights the adaptability of information theory principles across different objectives—maximizing capacity or preserving privacy.

## Entropy rate

The entropy rate is a concept in information theory that measures the average amount of information produced by a stochastic process per time unit. It is often used in the context of random processes or time series data, where the values are not identically distributed or there are dependencies between successive observations.

For a stochastic process $X_t$ where $t$ represents discrete time steps, the entropy rate $H(X)$ is defined as the limit of the avergae entropy of the first n random variables divided by n as n approaches infinity:

$$ H(X) = \lim_{n \to \infty} \frac{1}{n} H(X_1, X_2, \dots, X_n) $$

The entropy rate for vareity of processes:
* Independent Identically Distributed (IID) Process: If $X_i$ are IID, the entropy rate is the same as the entropy of a single random variable.
* Markov Process: For a Markov process, where the next state depends only on the current state (not on the history), the entropy rate is the entropy of the next state given the current state once the process has reached its steady-state distribution.
* Ergodic Process: For an ergodic process, the entropy rate can be calculated by considering a long sequence from a single sample path, as it will converge to the same value as the average over many sample paths.

[[notes/compression|Compression]]

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