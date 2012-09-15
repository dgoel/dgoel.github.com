---
layout: post
title: "Curious Pattern"
date: 2012-09-07 00:18
comments: true
sharing: true
categories: [mathematics]
---

A while ago I came across this curious pattern on [Futility Closet](http://www.futilitycloset.com/2012/01/08/math-notes-76/):

1/998001 = 0.000001002003004005006007008009010011012013014015016017018019020
0210220230240250260270280290300310320330340350360370380390400410420430440450
4604704804905005105205305405505605705805906006106206306406506606706806907007
1072073074075076077078079080081082083084085086087088089090091092093094095096
0970980991001011021031041051061071081091101111121131141151161171181191201211
22123124125126127128129130131132133134135136137138139140...996997999...

i.e.
1/998001 = 0.000 001 002 003 004 005 006 007 008 009 010 011 012 013 014 015
016 017 018 019 020 021 022 023 024 025 026 027 ... 996 997 999 ...

Looking at this, few questions popped into my head:  
**Q1**. *What causes this pattern to occur?*  
**Q2**. *Why is 998 missing from the sequence (notice that 999 appears after 997 and not 998)?*  
**Q3**. *What happens after 999, does the pattern break down, does it repeat?*  

So I sat down with a pen and paper and started exploring.

It's easy to write down the following fraction in a closed form using [Taylor Series](https://en.wikipedia.org/wiki/Taylor_series):

$$
\begin{align}
\frac{1}{999} &= 10^{-3} * \frac{1}{1 - 10^{-3}} \\
              &= 10^{-3} * \sum_{n = 0}^{\infty} (10^{-3})^{n} \\
              &= \sum_{n = 1}^{\infty} 10^{-3n}
\end{align}
$$

Now, we can write down 1\998001 as the sqaure of 1\999. And by now, you must have
guessed where I'm going with this.

$$
\begin{align}
\frac{1}{998001} &= \frac{1}{999} * \frac{1}{999} \\

                 &= \sum_{n = 1}^{\infty} 10^{-3n} * \sum_{k = 1}^{\infty} 10^{-3k} \\
                 
                 &= \sum_{n = 1}^{\infty}\sum_{k = 1}^{\infty}10^{-3 (k + n)} \\
\end{align}
$$
    

For $k > 0$ and $n > 0$, $(k + n)$ can have $(k + n - 1)$ combinations. Hence,
the term $10^\{-3\(k + n\)\}$ will appear $\(k + n - 1\)$ times in the expression. Hence, we can write down the fraction in a simple (*yet mischievous*) closed form:

$$
\frac{1}{998001} = \sum_{p = 1}^{\infty}(p - 1)10^{-3p}
$$

Let's see if we can answer the questions now.  

**A1**. The closed form expression is self-explanatory here. 

**A2**. In order to see why 998 is missing, we need to expand the closed form expression for values of $p$ in the neighborhood of 998.

$$
\begin{align}

\sum_{p = 998}^{p = 1002}(p - 1)10^{-3p} &= 10^{-3(998)} * [997 + 998 * 10^{-3} + 999 * 10^{-6} \\
                                         & \qquad \qquad \qquad + 1000 * 10^{-9} + 1001 * 10^{-12}] \\
                                         &= 10^{-3(998)} * [997 + 999 * 10 ^{-3} + 1001 * 10^{-12}] \\
\end{align}
$$

Note that the middle three terms combine together to absorb the term including 998 as the multiplier. Hence, it's missing from the pattern.

**A3**. In order to answer the third question, we need to re-visit the above expansion. Since 999 term appears after 997, a 6-digit void gets created because the 999 term absorbs three terms. But, at the same time, $p$ exceeds 999 and hence the next term can't fit in it's designated spot of three digits. As a result, it overflows and ends up using one digit in the 6-digit void. ... and the pattern resumes after a short hiccup. Beautiful!   

For the sake of completion, this is how the pattern looks-like near 999: 996 997 999 000 001 002 003 ...

