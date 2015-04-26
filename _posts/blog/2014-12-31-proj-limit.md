---
layout: post
title: "The projection space of multi-dimensional data"
excerpt: "Pairwise analysis on multidimensional datasets"
categories: blog
---

Under the framework of multi-dimensional signal processing, the decomposition of a data set proceeds via projections onto eigenfunctions of a desired transform.  Projections may be of the form where ordering is important, such as in Matching Pursuit or Periodicity Transform, or where ordering does not matter as in Gabor or Hilbert Transform.  For a dataset of $$N$$ dimensions, the signal processing on random projections proceeds in groups of $$n$$ at a time where $$n \leq N$$.

It turns out that the number of unique projections of dimension $$n\in N$$ is given by the binomial coefficient $$N \choose n$$, and the total number of unique projections $$d$$ up to $$n$$ dimensions is

$$
\sum_{d=1}^{n \in N} { n \choose d } = \sum_{d=1}^{n \in N} {\frac{n!}{d!(n-d)!}}
$$

This expression gives an upper bound on the total number of processing operations for an exhaustive analysis where ordering of dimensions doesn't matter.

If however ordering does matter then permutations need to be taken into account which means every combination is permuted $$d!$$ number of times.  The upper bound becomes

$$
d!\sum_{d=1}^{n \in N} { n \choose d } = \sum_{d=1}^{n \in N} {\frac{n!}{(n-d)!}}
$$

A log plot of the two functions for dimension up to 100 shows the number of processing operations not only increases exponentially, but also ordered projections introduce many orders of magnitude in computational requirement.


<figure class="center">
	<a href="/images/ProjLimits.png"><img src="/images/ProjLimits.png" alt="image"></a>
	<figcaption>Figure 1: System with phase noise and subsequent filtering.</figcaption>
</figure>

The point of this is to show that an exhaustive decomposition of multi-dimensional data will be a point on or below one of these curves depending on the transform applied.  Usually a brute force analysis of all projections need not be performed if the required ones can be identified.

