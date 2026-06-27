+++
title = "A Brief Introduction to ZeroGrad"
date = "2026-06-27T19:31:35+05:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = "Hassan"
authorTwitter = "" #do not include @
cover = ""
tags = ["Project", "SysML"]
keywords = []
description = "Building a custom autograd engine in C++20 with static memory planning."
showFullContent = false
readingTime = true
hideComments = false
+++

# ZeroGrad - A custom autograd engine in C++20 with static memory planning

## Background
**ZeroGrad** is a summer project that I have started working on in the past few days. It's primarily a SysML project where I plan to implement much of the math and mechanics behind ML libraries from scratch with a twist of systems programming.

## Explanation of the Project
If you've taken a Calculus or possibly an ML-adjacent class, you might've learnt about automatic differentiation and more specifically **backpropagation**. It's one of the methods used to train neural networks to find the gradients of a loss function with respect to the input parameters. This, combined with gradient descent allows to iteratively refine our parameters to minimize the loss function. All the neurons (in all the layers) of the neural network are then trained which constitutes 'training the whole neural network'.

![Automatic Differentiation](/images/autodiff.png)

This is a pretty basic thing and all big ML libraries like PyTorch implement this. Now, my goal is to implement an autograd engine similar to that of PyTorch (but a lot more humble) in C++, which is already a nice engineering exercise, but the **static memory planning** is where the novelty comes in.

## The Novelty
PyTorch and other ML libraries when building the computational graph use general purpose allocators which are dynamic i.e. memory is allocated on the heap. This is because they work on both fixed and variable architecture neural networks.

However, if we strictly limit our engine to **fixed** neural network architectures then it's possible to implement static memory planning, greatly improving performance and resource utilization. Therefore, the latter part of the project will be focused on implementing static memory management and comparing its different approaches to PyTorch.

## Tech Stack
The following tools and technologies will be used for this project:
* **C++20:** PyTorch's backend itself is majorly built in C++. Also, many modern C++ concepts such as move semantics, smart pointers and lambdas are crucial for efficiency. Let's also not forget the static memory planning implementation.
* **Python:** To run PyTorch for comparisons, and also to run training loops in Python as well.
* **PyBind11:** Instead of re-writing the engine I wrote in C++ in Python, this will act as a bridge between C++ and Python, allowing me to 'port' or expose my C++ classes to Python.
* **Catch2:** This is a testing framework for C++. Before commiting any major changes and to verify the correctness of my implementations, this will play a major role.
* **Valgrind / heaptrack:** To ensure no memory is leaked and to track heap allocations.
* **perf:** CPU profiling and benchmarking

## Major Goals
For now, following are the major goals of the project:
1. To implement `Scalar` and `Tensor` classes and be able to run neural network training loops using gradient descent.
2. To make the engine richer with the ability to work on convolutional neural networks.
3. To implement an arena allocator and experiment with different static memory planning algorithms.

## Conclusion
This project is going to be a deep dive into the intersection of machine learning math and low-level systems memory management. I'll be updates on the project as I go!