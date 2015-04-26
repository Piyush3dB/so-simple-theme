---
layout: post
title: "A note on the Gardner Sampling Error Detector"
excerpt: "Different forms of the error detector formula"
categories: blog
---


The Gardner Sampling (or Timing) Error Detector is a blind timing recovery algorithm originally proposed by Gardner in [1].  For every sampling operation, the algorithm requires two samples that are located mid way between strobes, and a third sample occuring at the current strobe.  A block diagram of the Gardner TED is shown in the figure.

<figure class="center">
	<a href="/images/gardnerted.png"><img src="/images/gardnerted.png" alt="image"></a>
	<figcaption>Figure 1: Gardner timing error detector.</figcaption>
</figure>



A variation in the formula for the Gardner TED quoted in some Journal papers.  For instance, the original form of the Gardner TED as in [1] is written as

$$
\begin{eqnarray}
e[n] & = & y_{I}[n-0.5]\left(y_{I}[n]- y_{I}[n-1] \right) \\ 
& = & + y_{Q}[n-0.5]\left(y_{Q}[n]- y_{Q}[n-1] \right) 
\end{eqnarray}
$$

Where-as more recent papers such as [2] quote the Gardner TED as

$$
e[n] = Re\left \{ \left( y[n] - y[n-1] \right)y^{*}[n-0.5] \right \} 
$$

It turns out the two forms are essentially the same, which can be shown with a bit of algebraic manipulation.  For our notation let $$ y[.] = y_{I}[.]+jy_{Q}[.] $$ denote a complex number and it's complex conjugation  $$y^{*}[.] = y_{I}[.]-jy_{Q}[.] $$.

Starting with the form in [2] and expanding

$$
\begin{eqnarray}
e_{IQ}[n]&=&\left(y[n]-y[n-1]\right)y^{*}[n-0.5] \\ 
&=&\left( y_{I}[n]+jy_{Q}[n] - y_{I}[n-1] -jy_{Q}[n-1] \right)y^{*}[n-0.5] \\ 
&=&\left( \left(y_{I}[n]- y_{I}[n-1] \right) +j \left(y_{Q}[n]-y_{Q}[n-1] \right) \right) \left(y_{I}[n-0.5]-jy_{Q}[n-0.5] \right) \end{eqnarray} 
$$

All that is required is to collect the real parts in the above expression.  The identity $$(a+jb)(c-jd)=(ac+bd) + j(bc-ad)$$ can be applied with the real part being $$Re\left\{(a+jb)(c-jd)\right\}=ac+bd$$.

Choosing

$$
\begin{array}
\\
a=\left(y_{I}[n]- y_{I}[n-1] \right)\\  
b=\left(y_{Q}[n]-y_{Q}[n-1] \right)\\  
c=y_{I}[n-0.5]\\  
d=y_{Q}[n-0.5]\\
\end{array}
$$

we have

$$
\begin{eqnarray}
Re \left\{ e_{IQ}[n] \right\} &=& y_{I}[n-0.5]\left(y_{I}[n]- y_{I}[n-1] \right) + y_{Q}[n-0.5]\left(y_{Q}[n]- y_{Q}[n-1] \right) 
\\ &=& e[n]
\end{eqnarray} 
$$

This is the expanded form in [1]. Therefore both forms of the Gardner TED are equivalent and have the same error calculation.


References
----------

[1] F. M. Gardner, [_"A BPSK/QPSK timing-error detector for sampled receivers"_](http://ieeexplore.ieee.org/xpl/freeabs_all.jsp?arnumber=1096561), IEEE Transactions on Communication, Vol COM-34, pp 423 – 429, May 1986.

[2] Leng et al, [_"A modified gardner detector for multilevel PAM/QAM system"_](http://ieeexplore.ieee.org/xpl/articleDetails.jsp?reload=true&arnumber=4657912), Communications, Circuits and Systems, 2008. ICCCAS 2008. International Conference on, pp 891 – 895 , October 2008.
