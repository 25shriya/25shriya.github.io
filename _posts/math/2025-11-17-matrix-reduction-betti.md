---
layout: post
title:  "Matrix Reduction and Betti Numbers of a Triangulated Space"
---

{%- include mathjax.html -%}
## Preliminary Definitions

A $k$-$\textit{simplex}$ is the set 
$$
\{(x_0, \ldots, x_k) \in \mathbb{R}^{k+1} \, \mid \, \sum_{i=0}^k x_i = 1\}.
$$
This can be better understood as the generalization of the notion of triangles/tetrahedrons to higher dimensions.

A $k$-$\textit{simplicial complex, } \mathcal{K}$ is a set of simplices, whose elements are called $\textit{faces}$ and:

1. Every subset (which is a simplex itself, called the $face$ of a simplex) of a simplex from $\mathcal{K}$ is also in $\mathcal{K}$, and

2. Every pair of non-empty faces of $\mathcal{K}$ intersects at a simplex of both faces.

A $p$-$\textit{chain}$ is a sum of $p$-simplices in simplicial complex $\mathcal{K}$, a $p$-simplex itself. 

The $p$-boundary of a $p$-simplex is the sum of its $(p-1)$ dimensional faces. A $p$-$\textit{cycle}$ is a $p$-chain whose boundary is $0$. The group of all $p$-cycles in a simplicial complex is represented by $\mathsf{Z}_p$, and its rank by $z_p$.

A $p$-$\textit{boundary}$ of a simplicial complex is a $p$-chain which is the boundary of a $(p+1)$-chain. The group of all $p$-boundaries is represented by $\mathsf{B}_p$, and its rank by $b_p$.

Note that, $n_p = z_p + b_{p-1}$, where $n_p$ is the number of $p$-simplices and $\beta_p = z_p - b_p$, where $\beta_p$ is the $p^{th} \textit{ Betti number,}$ the rank of the $p^{th}$-homology of the triangulated space.

Every topological space that is [triangulable](https://en.wikipedia.org/wiki/Triangulation_(topology)) has a simplicial complex associated with it.

------------

## Euler-Poincaré Theorem

The $\textit{Euler relation for planar graphs}$ states that $v - e + f = c + 1$ for a graph with $v$ vertices, $e$ edges, $f$ faces and $c$ connected components. This is used to study and classify planarity of graphs extensively in algorithm development, computational geometry and in many other subfields of theoretical computer science and mathematics.

The generalization of the above relation is the $\textit{Euler-Poincaré Theorem}$ for topological spaces and the chosen simplixial complex. This theorem states that the Euler characteristic of a topological space is the alternating sum of its Betti numbers.

Formally speaking, we say that the Euler characteristic of a triangulated space with Betti numbers $\beta_i$ is $\sum_{p \geq 0} (-1)^{(p)} \beta_p$. Constructing the $p^{th} \textit{ boundary matrix}$ for these spaces and reducing them to their $\textit{Smith normal form}$ yields (reduced) Betti numbers of the triangulated space.

It is worthy to note that the Euler characteristic is also the alternating sum of number of $p$-simplices, $\sum_{p \geq 0} (-1)^{(p)} n_p$, although, $n_p \neq \beta_p$ for any $p$.

------------

## Defining and Reducing the $p$-Boundary Matrix

The $p^{th}$ boundary matrix is defined (modulo $2$) for a simplicial complex $K$ as follows: for each dimension $(p-1) \times p$, we have $\partial_p = [a_{i}^{j}]$, where:

1. $1 \leq i \leq n_{p-1}$, where $n_{p-1}$ is the number of $p-1$ simplices in $K$,

2. $1 \leq j \leq n_p$ defined similarly,

3. $a_i^{j} = 1$ if the $i^{th}$ $(p-1)$-simplex is a face of the $j^{th}$ $p$-simplex, and

4. $a_i^{j} = 0$ otherwise.

A series of row and column operations can be defined on this matrix which reduces it to the Smith normal form. We know that $n_p = b_{p-1} + z_p$. The former is the leftmost $b_{p-1}$ nonzero columns of the reduced matrix which generate the group 
$$
\mathsf{B}_{p-1}
$$ and the latter is the last $z_p$ zero columns of the reduce matrix, which generate 
$$
\mathsf{Z}_p.
$$ Once we reduce each boundary matrix to its normal form, we get their ranks. Then, we must calculate $\beta_p = z_p - b_p = n_p - b_{p-1} - b_p$. Since the rank of $\partial_{p}$ is $b_{p-1}$ and rank of $\partial_{p+1}$ is $b_p$, we obtain $\beta_p = n_p - \text{rank}({\partial_p}) - \text{rank}(\partial_{p+1})$.

Here is the SageMath code written by me to get the required Betti numbers:

```python
from sage.all import * 

# Initialization
N = eval(input("Enter simplicial complex: ")) 
simplicial_complex = SimplicialComplex(N)
faces = simplicial_complex.faces()
ranks = []
betti_numbers = []
nps = []

for p in range(simplicial_complex.dimension()):
    if p == 0:  # Exceptional Case of p = 0
        rows = 0
        cols = len(faces[0])
        req_list = []
    else:  # Initializing matrix
        rows = len(faces[p-1])
        cols = len(faces[p])
        temp = [0]*cols
        req_list = [temp[:] for i in range(rows)]
    p_1_simplices = sorted(list(faces[p-1]))
    p_simplices = sorted(list(faces[p]))
    for i in range(rows):  
        # Defining boundary matrix as per conditions given
        for j in range(cols):
            if p_1_simplices[i] in p_simplices[j].faces():
                req_list[i][j] = 1
            else:
                req_list[i][j] = 0
    # Initializing boundary matrix along with required field
    p_boundary_matrix = matrix(ZZ.quotient(2), req_list)
    reduced_p_boundary_matrix = p_boundary_matrix.smith_form()
    ranks.append(reduced_p_boundary_matrix[0].rank())
    nps.append(cols)

for p in range(simplicial_complex.dimension()):
    if p+1 < len(ranks):  # applying Betti number formula
        betti_numbers.append(nps[p] - ranks[p] - ranks[p+1])
    else:
        betti_numbers.append(0)

for p in range(simplicial_complex.dimension()):
    if p == 1:
        print("First Betti Number: ", betti_numbers[p])
    elif p == 2:
        print("Second Betti Number: ", betti_numbers[p])
    elif p == 3:
        print("Third Betti Number: ", betti_numbers[p])
    else:
        print(p, "th Betti Number: ", betti_numbers[p])
print("Betti numbers higher than this are 0")
```

I found an [interesting repository](https://github.com/kc-howe/Betti-Numbers) coded in NumPy that performs the above computation. The primary source of reference for this article was [Computational Topology by Edelsbrunner](https://webhomes.maths.ed.ac.uk/~v1ranick/papers/edelcomp.pdf). 





