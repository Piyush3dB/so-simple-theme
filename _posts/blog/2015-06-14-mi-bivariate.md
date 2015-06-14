---
layout: post
title: Expected Mutual Information of a contingency table
excerpt: Linking joint counts to probabilities and mutial information
categories: blog
tags: [information theory]
comments: true
---

Let $$V_X=\{x_i\}_{i=1}^n$$ and $$V_Y=\{y_j\}_{j=1}^p$$ be sets of input and output class identifiers with a joint relationship.  

We can define a count matrix $$N_{XY}$$ where $$N_{XY}=N_{XY}(x_i,y_j)=N_{ij}$$ represents the number of times the joint event $$(X=x_i, Y=y_j)$$ occurs.

Then $$N_{XY}$$ is essentially a the count based contingency table, and one may apply information theoretic analysis to such a representation of a bivariate distribution.

A question appeared on [stack overflow](http://math.stackexchange.com/questions/438078/mutual-information-for-clustering) a while back concerning the mutual information metric of input and output classes.  Specifically how does one link the Expected Mutual Information expression

$$
MI_{P_{XY}} = \sum_{x,y} P_{X,Y}(x,y) \log{\frac{P_{X,Y}(x,y)}{P_X(x)P_Y(y)}}
$$

to this which commonly appears in the academic literature?

$$
MI_{P_{XY}} =\sum_{i,j} \frac{N_{ij}}{N_T} \log{\frac{N_T}{N_iN_j}}N_{ij}
$$

If we let marginal and joint counts

$$
N_i=\sum_{j}N_{ij}
$$
 
$$
N_j=\sum_{i}N_{ij}
$$

$$
N_T=\sum_{i,j}N_{ij}
$$
 
 
and use these to define define marginal and joint probabilities 

$$
P_X(x) = \frac{N_i}{N_T}
$$

$$
P_Y(y) = \frac{N_j}{N_T}
$$

$$
P_{X,Y}(y) = \frac{N_{ij}}{N_T}
$$

then by substitution the expressions for $$MI_{P_{XY}}$$ are equivalent.

It's also worth pointing out $$ \log{\frac{N_T}{N_iN_j}}N_{ij} $$ represents the Pointwise Mutual Information which is the information content of a particular joint count, as opposed to the  Expected Mutual Information $$MI_{P_{XY}}$$ which represents the average information content of the entire joint distribution.

