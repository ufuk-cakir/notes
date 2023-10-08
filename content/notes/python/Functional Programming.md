---
title: Functional Programming
tags:
  - python
---
The main idea of functional programming is to organize the code around the use of functions. Each function should perform only one clearly defined task and needs to be pure. Everything in the code happens through functions and parameters. The functionality of the code breaks down into neat, single-responsible and reusable function

# Pure Functions
A pure function is one that returns the same output for a given set of inputs, without having side effects, similar to a mathmatical function.
- Pure Functions return the same output for a given set of inputs: this may sound obvious, but some functions may use and change global variables (e.g a checking condition, or a global counter), which would return different values based on the global variable. Pure functions, however, should not rely on global variables
- Pure functions have no side effects: Pure functions only act on the input parameters they get and dont read or set variables outside the function. They dont affect other parts of the code
- Pure Functions only use the parameters that are passed