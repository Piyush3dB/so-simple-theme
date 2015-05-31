---
layout: post
title: "A more elegant way of looking at Correlation"
excerpt: "Intuition behind the correlation metric"
categories: articles
tags: [signal processing]
comments: true
share: true
---



It took me a while to understand the inner working of the correlation metric does and why it works.  In this post I'm going to present my intuitive understanding of [signal correlation](http://en.wikipedia.org/wiki/Cross-correlation) and how I relate it to the idea of statistical correlation, more commonly known as the [Pearson product-moment correlation coefficient](http://en.wikipedia.org/wiki/Pearson_product-moment_correlation_coefficient).

 

I'm going to use the terms signal, time series and data set interchangeably.  

Correlation is a measure of similarity between two signals, and from a Signal Processing view a crude measure of similarity is the cross energy of the two signals:


$$
\sum_{n=0}^{N-1} x[n] y[n]
$$

where $$ N $$ is the length of the signals.  It turns out the obove formula has a geometric interpretation in terms of the dot product formula:

$$
\sum_{n=0}^{N-1} x[n] y[n] = \vec{x} \cdot \vec{y} = \mid  \vec{x} \mid \mid  \vec{y} \mid  cos(\theta) 
$$

where the magnitude is defined as $$ \mid  \vec{x} \mid = \sqrt{ \sum_{n=0}^{N-1} x[n]^2 } $$ and the same for $$\mid \vec{y} \mid $$.

The dot product takes $$ \mathbb{R}^{N} \times \mathbb{R}^{N} $$ to $$ \mathbb{R}^{1} $$ That is, two length $$ N $$ signals are mapped to a scalar.  The formula is essentially saying

`(similarity between x and y)  = (magnitude of x) (magnitude of y) (cos of angle between x and y) `

The procedure is easily visualised if $$N=2$$ in $$\mathbb{R}^{2}$$ space:

<figure>
	<a href="/images/dotProd.png"><img src="/images/dotProd.png" alt="image"></a>
	<figcaption><a href="http://jackschaedler.github.io/circles-sines-signals/dotproduct.html" title="Geometric Interpretation of the Dot Product">Geometric Interpretation of the Dot Product</a>.</figcaption>
</figure>

It turns out the $$cos(\theta) $$ term is actually the correlation value after all.

If $$x[n]$$ and $$y[n]$$ are the same then their vector representations $$\vec{x}$$ and $$\vec{y}$$ will be parallel to each other and pointing in the same direction.  They would have an angle $$\theta = 0^{\circ}$$ and therefore a maximum positive similarity because $$cos(\theta) = 1$$.  At the other end of the scale their vector representations would again be parallel but pointing in opposite directions to each other.  They would have a maximum negative similarity since angle $$\theta = 180^{\circ} \Rightarrow cos(\theta) = -1$$.  Therefore all other orientations of vectors will give a similarity metric falling between the most positive and most negative values, and $$cos(\theta)$$ in the range $$ [-1, 1] $$.  From this observation the natural interpretation of the presence of the $$cos(\theta)$$ term is that it gives some measure of how parallel the vectors are to eachother, which is in fact the correlation between $$x[n]$$ and $$y[n]$$.

`(correlation between x and y) = (cos of angle between vector representations of x and y)`

So the crude measure of similarity we started off with, the cross energy, is 'refined' by applying correction terms determined by the magnitude of both signals. This formula is the the well known definition of [cosine similarity](http://en.wikipedia.org/wiki/Cosine_similarity).

$$
corr_{x,y} = cos(\theta) = \frac{\vec{x} \cdot \vec{y} }{\mid \vec{x} \mid \mid \vec{y} \mid}
$$

Another way to look at the formula is to observe that a vector divided by its magnitude is a unit vector pointing in the direction of the original vector.  This operation is the well known 'normalisation' procedure of the signal.  So in simpler terms, the correlation of two signals is the dot product of their respective normalised signals, or in other words the dot product of their unit vectors.

$$
corr_{x,y} = \frac{\vec{x}}{\mid \vec{x} \mid} \cdot \frac{\vec{y}}{\mid \vec{y} \mid}
$$

The normalisation essentially converts signals $$\vec{x}$$ and $$\vec{y}$$ to a common unit system (the unit vector) and the implication of this is the correlation value always falls in the meaningful range $$[-1, 1]$$.

What about the definition of statistical correlation which appears to have a different formulation:

$$
corr_{x,y} = \frac{cov_{x,y}}{\sigma_{x} \sigma_{y}}
$$

With some algebra we can show the the formula is not all that different from the above thinking because with a bit of algebra we can show

$$
\begin{eqnarray}
\frac{cov_{x,y}}{\sigma_{x} \sigma_{y}} & = & \frac{\frac{1}{N} \sum_{n=0}^{N-1} (x[n] - \bar{x} )(y[n] - \bar{y}) }{ \sqrt{\frac{1}{N} \sum_{n=0}^{N-1} (x[n]-\bar{x})^2 } \sqrt{\frac{1}{N} \sum_{n=0}^{N-1} (y[n]-\bar{y})^2 }} \\ 

& = & \frac{\frac{1}{N} \sum_{n=0}^{N-1} (x[n] - \bar{x} )(y[n] - \bar{y}) }{ \frac{1}{\sqrt{N}} \sqrt{ \sum_{n=0}^{N-1} (x[n]-\bar{x})^2 }  \frac{1}{\sqrt{N}}\sqrt{ \sum_{n=0}^{N-1} (y[n]-\bar{y})^2 }} \\

& = & \frac{ \sum_{n=0}^{N-1} (x[n] - \bar{x} )(y[n] - \bar{y}) }{  \sqrt{ \sum_{n=0}^{N-1} (x[n]-\bar{x})^2 }  \sqrt{ \sum_{n=0}^{N-1} (y[n]-\bar{y})^2 }} \\

& = & \frac{\overrightarrow{x - \bar{x}} \cdot \overrightarrow{y - \bar{y}} }{ \mid \overrightarrow{x - \bar{x}} \mid \mid \overrightarrow{y - \bar{y}} \mid} \\

& = & \frac{\overrightarrow{x - \bar{x}}   }{ \mid \overrightarrow{x - \bar{x}} \mid } \cdot \frac{ \overrightarrow{y - \bar{y}} } {\mid \overrightarrow{y - \bar{y}} \mid} \\

& = & corr_{x,y}

\end{eqnarray}
$$

The extra manipulation of signals $$x[n]$$ and $$y[n]$$ by subtraction of their means $$\bar{x}$$ and $$\bar{y}$$ is just part of the procedure of converting them to a common unit system (mean adjusted) before applying the normalisation to convert into the permitted unit system (unit vector) so that dot may be correctly computed.












