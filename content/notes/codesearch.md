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