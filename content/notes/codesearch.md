---
title: Program Synthesis
date: 2024-06-21
---

Program Synthesis is the task of automatically finding programs from the underlying programming language that satisfy user intent expressed in some form of constraints. This is very different from the traditional typical compiler which takes in high-level code and converts it to machine code. In program synthesis, We usually search in the space of programs to find the one that satisfies the constraints. This is a very active area of research and has many applications in software engineering, programming languages, and AI.

Program synthesis is a ridiculously hard problem. In its most general case ( Turing complete programming language), the possible space is all possible programs that can be computed. Even with a small number of constraints, the search space can grow exponentially. User Intent is another hard sub-problem to solve. The specification of the program can be ambiguous, incomplete, or even incorrect. The user might not know exactly what they want, or they might not be able to express it in a way that the synthesizer can understand.

## Parts of Program Synthesis

A synthesizer is typically characterized by three key dimensions: the kind of constraints that it accepts as expression of user intent, the space of programs over which it searches, and the search technique it employs. Lets define these three dimensions:

### User Intent

A logical specification is a logical relation between inputs and outputs of a program. Some users can express their needs through traces, examples, psudocode, or natural language. The synthesizer should be able to understand these constraints and search for a program that satisfies them.

### Program Space

The program space defines the set of possible programs that the synthesizer considers. This space is typically defined by a domain-specific language (DSL) or a subset of a general-purpose programming language. The choice of program space significantly impacts the efficiency and effectiveness of the synthesis process.
Key aspects of the program space include:

* Syntax: The allowed structures and constructs in the language
* Semantics: The meaning and behavior of the language constructs
* Expressiveness: The range of programs that can be represented
* Size: The number of possible programs in the space

### Search Technique

The search technique is the algorithm used to explore the program space and find a program that satisfies the user's intent. Common search techniques include:

* Enumerative search: Systematically generate and test candidate programs
* Constraint solving: Convert the synthesis problem into a logical constraint satisfaction problem
* Version space algebra: Maintain and refine a compact representation of the space of consistent programs
* Neural-guided search: Use machine learning models to guide the search process
* Deductive synthesis: Apply logical inference rules to derive a program from the specification

The choice of search technique depends on factors such as the size and structure of the program space, the nature of the user intent specification, and the desired performance characteristics of the synthesizer.

## Papers to focus on:

* [Program synthsis](https://www.microsoft.com/en-us/research/wp-content/uploads/2017/10/program_synthesis_now.pdf)
  * Personally a good read to get started. Not to technical, but the basics are there
* [DreamCoder](https://arxiv.org/abs/2006.08381)
  * Must read, starts with wake and sleep learning algorithms and goes into rough details
* [Stitch](https://arxiv.org/abs/2211.16605)
  * Figures out some shortcoming of DreamCoder and adds more step to increase the speed of synthesis
  * [Github Repo](https://github.com/mlb2251/stitch/tree/main) has really good documentation and implementation (RU). Focus on the abstraction part of program synthesis.
* [Abstract Beam](https://arxiv.org/pdf/2405.17514) 
  * Has a method to improve tradtional search which involves creating abstractions and then searching in the abstraction space. 

Although these papers are great, the number of papers compared to other areas of ML are very low.

I would recommend focusing on Math based papers especially the ones which work with LEAN

* [GPT-f](https://arxiv.org/abs/2009.03393)
* [Formal mathematics statement continious learning](https://arxiv.org/abs/2202.01344)
* [Deepseek prover 1/1.5](https://github.com/deepseek-ai/DeepSeek-Prover-V1.5)
* [Alphageometry](https://www.nature.com/articles/s41586-023-06747-5)
* [Autoformalization](https://arxiv.org/abs/2205.12615)
* [Baldur](https://arxiv.org/pdf/2303.04910)

*Personal opinion: program synthesis is a more of a engineering problem than a research problem. You have to rely more on the search part of symbolic execution. Be very doubtfull of papers whose results look abnormally great, most of the times the sheer inference compute is not shared*