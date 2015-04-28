---
layout: post
title: Consistency with Parseval's theorem
excerpt: Energy conservation property
categories: blog
tags: [signal processing]
comments: true
---

<script src="https://gist.github.com/Piyush3dB/0e377979a4e941021922.js"></script>

This bit of Python code evaluates a complex signal's consistency with Parseval's Theorem.  The Theorem essentially states that is that the total energy contained in a signal $$x[n]$$ summed across samples $$n$$ is equal to the total energy of the signal's Fourier Transform $$X[k]$$ summed across all of its frequency components $$k$$.

$$
\sum_{n=0}^{N-1} | x[n] |^2  =   \frac{1}{N} \sum_{k=0}^{N-1} | X[k] |^2 
$$
