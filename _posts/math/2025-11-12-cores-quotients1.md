---
layout: post
title:  "Cores and Quotients of Integer Partitions - Part 1"
---

{%- include mathjax.html -%}

## Introduction to Integer Partitions

An $\textit{integer partition}$ $\lambda = (a_1, a_2, \ldots, a_m)$ of $n$ is a nonincreasing finite sequence of integers such that $\sum_{i=1}^m a_i = n$. The number of partitions for each integer was primarily studied by Srinivasa Ramanujam and is applied in various fields such as representation theory, theoretical physics, and statistics.

Each element of a partition is called its $\textit{part}$, and following the above notation, we have $l(\lambda) = m$ and $\mid \lambda \mid = n$. Note that for a given positive integer $n$, the largest partition is $(1,1, \ldots 1)$, $n$ times and smallest partition is $(n)$. Therefore, $1 \leq l(\lambda) \leq n$ for any partition $\lambda  $ of $n$. 

<br>

For a partition $\lambda = (a_1, a_2, \ldots, a_m)$, define 
$$
\mathcal{Y}(\lambda) = \{(i,j) \in \mathbb{N} \times \mathbb{N} \mid 1 \leq i \leq m, \, 1 \leq j \leq a_i\},
$$ visualized by the $\textit{Young diagram}$ or $\textit{Ferrer's diagram}$, as shown for example partition $(5,3,2,1)$.
<div style="text-align: center;">
$$
\begin{aligned}
\begin{array}{lllll}
\blacksquare & \blacksquare & \blacksquare & \blacksquare & \blacksquare \\
\blacksquare & \blacksquare & \blacksquare \\
\blacksquare & \blacksquare \\
\blacksquare
\end{array}
\end{aligned}
$$
</div>
For $(i,j) \in \mathcal{Y}(\lambda)$, we get 
$$
\mathfrak{h}_{ij}(\lambda)
=
\left\{(i', j') \in \mathcal{Y}(\lambda)\;\middle|\;
\left.
\begin{array}{l}
i = i' \text{ and } j' \ge j, \\[4pt]
j = j' \text{ and } i' > i
\end{array}
\right.
\right\},
$$

the $(i,j)\textit{-hook}$ in $\lambda$. The following diagram shows the $(1,2)$-hook of $(5,3,2,1)$: 
<div style="text-align: center;">
$$
\begin{array}{lllll}
\blacksquare & \times & \times & \times & \times \\
\blacksquare & \times & \blacksquare \\
\blacksquare & \times \\
\blacksquare
\end{array}
$$
</div>

<br>

The $(i,j)\textit{-hooklength}$ of $\lambda$, is $h_{ij}(\lambda) = \mid \mathfrak{h}_{ij}(\lambda) \mid$. The $(1,2)$-hooklength of $(5,3,2,1)$ is $6$. A $\textit{p-hook}$ is a hook of a partition with hooklength divisible by the natural number $\textit{p}$.

------------

## Cores and Quotients of Integer Partitions


We now define the $\textit{p-core}$ and $\textit{p-quotient}$ algebraically, after which we tie the combinatorial and algebraic interpretation of the two.

A $\beta$-set 
$$
X = \{ h_1, \ldots h_t \}
$$ is a finite increasing subset of whole numbers such that the last term can be zero. If 
$$
s \in \mathbb{N}_0 (= \mathbb{N} \cup \{ 0 \}),
$$
define transposing $X$ as 
$$
X^{+s} = \{h_1+s, \ldots h_t + s, s - 1, s- 2, \ldots 2, 1, 0\}. 
$$
 The partition associated with $\beta$-set $X$ is $P(X) = (h_1 - (t-1), h_2 - (t-2) \ldots h_t)$. $X$ is a $\beta$-set for partition $\lambda$ if $\lambda=P(X)$. Given a partition $\lambda$, we get a $\beta$-set $X_\lambda$ for $\lambda$ by getting the first column hooklengths of $\lambda$. Hence, all sets $X_\lambda^{+s}$, where $s \in \mathbb{N}_0$ is a $\beta$-set for $\lambda$. The following image shows the relation between a partition and its $\beta$-sets.

<figure style="text-align: center;">
  <img src="{{ '/images/beta-set-partition.png' | relative_url }}" alt="description" width="100%">
  <figcaption>Figure 1: Relationship between a partition and its $\beta$-set.</figcaption>
</figure>

Now, for a $\beta$-set $X$ for a partition $\lambda$, fix a positive integer $p$ and define 
$$
X_i^{(p)} = \{a \in \mathbb{N}_0 \, \mid \, ap + i \in X\}
$$ and $$
X_{(p)} = \bigcup_{i=0}^{p-1} \{ ap+i \, \mid \, 0 \leq a \leq \mid X_i^{(p)} \mid \}.
$$
 The $\textit{p-core}$ of $\lambda$ is $\lambda_{(p)} = P(X_{(p)})$ and $\textit{p-quotient}$ is $\lambda^{(p)} = (\lambda_0, \ldots, \lambda_{p-1})$, where $\lambda_i = P(X_i^{(p)})$.

Combinatorially speaking, we understand $p$-cores and $p$-quotients by:

1. The $p$-core of a partition $\lambda$ corresponds to the partition obtained after removing from $\lambda$, all hooks with hooklength divisible by $p$ (called $p$-hooks). Interested readers can refer to the source of text for a bead and runner explanation of this equivalence.[^1]

2. Removing 1-hook from any of the partitions in $\lambda^{(p)}$ is equivalent to removing a $p$-hook from $\lambda$. Hence, the number of $p$-hooks to be removed from $\lambda$ to get the $p$-core is $\mid \lambda_0 \mid + \ldots + \mid \lambda_{p-1} \mid$ and $\mid \lambda \mid = \mid \lambda_{(p)} \mid + p^*(\mid \lambda_0 \mid + \ldots + \mid \lambda_{p-1} \mid)$.[^1]

A $p$-core of $n$ ($\in \mathbb{N}$) is a partition of $n$ without $p$-hooks and a $p$-quotient of $n$ is a tuple $(\lambda_0, \ldots \lambda_{p-1})$ satisfying $\sum_i \mid \lambda_i \mid = n$.

------------

## Cores, Quotients and Partitions Bijection

The main result of this article states that given a $p$-core $\kappa$ and $p$-quotient $(\lambda_0, \ldots \lambda_{p-1})$, a unique partition $\lambda$ can be constructed such that its $p$-core is $\kappa$ and $p$-quotient is $(\lambda_0, \ldots \lambda_{p-1})$. The crux of the proof of this statement is as follows:

1. We can first choose a $\beta$-set $Y$ for $\kappa$ such that $p \,\, \mid \, \, \mid Y \mid$ and that for all $0 \leq i \leq p - 1$, $Y_{i}^{(p)}$ has at least $l(\lambda_i)$ elements. Such a choice is possible, as we can first construct a $\beta$-set for $\kappa$, and transpose until $p \,\, \mid \, \, \mid Y \mid$. Then, we can take $\max(l(\lambda_i))$ and transpose $Y$ until the second condition is satisfied.

2. Then, choose $\beta$-sets $X_0, \ldots, X_{p-1}$ for $\lambda_0, \ldots, \lambda_{p-1}$ such that $\mid X_i \mid = \mid Y_i^{(p)} \mid$. Such a choice is possible, as, if $\mid X_i \mid < \mid Y_i^{(p)} \mid$, we transpose $ \mid X_i \mid$. The other way round is not possible due to the second condition on $Y_i^{(p)}$. The smallest size possible on $\mid X_i \mid$ is $l(\lambda_i)$ which is also the same bound for $\mid Y_i^{(p)} \mid$.

3. Consider 
$$
X' = \bigcup_{i=0}^{p-1} \{xp + i \, \mid \, x \in X_i\}.
$$
We first observe that $X_i^{(p)'}$ are $X_i$ for all $i$. Hence, the $p$-quotient of the partition $P(X')$ is $(\lambda_0, \ldots, \lambda_{p-1})$.

4. Moreover, 
   $$
   X'_{(p)} = \bigcup_{i=0}^{p-1} \{ap+i \, \mid \, 0 \leq a \leq \mid X_i^{(p)'} \mid \} \implies \\
   \bigcup_{i=0}^{p-1} \{ap+i \, \mid \, 0 \leq a \leq \mid X_i^{(p)} \mid \} \implies \\
   \bigcup_{i=0}^{p-1} \{ap+i \, \mid \, 0 \leq a \leq \mid Y_i^{(p)} \mid \} = \kappa.
   $$ 

   Hence, the $p$-core of the partition $P(X')$ is $\kappa$.

5. $P(X')$ is the unique partition we are looking for. It is unique, as if there existed another partition $\mu$ with the same $p$-core and $p$-quotient, applying the definition of the same by brute force yields $\mu = P(X')$.






[^1]: The main source of text used as a reference in this exposition can be found [here.](https://web.math.ku.dk/~olsson/manus/comb_rep_all.pdf)