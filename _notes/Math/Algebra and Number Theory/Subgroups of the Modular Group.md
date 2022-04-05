---
title: Subgroups of the Modular Group
tags: Modular-Forms Algebra Number-Theory
season : spring
---


$\newcommand{\Z}{\mathbb{Z}}\newcommand{\GL}{\text{GL}}\newcommand{\SL}{\text{SL}}\newcommand{\PSL}{\text{PSL}}$
In the [[_notes/Math/Algebra and Number Theory/Modular Group\|previous note]], we defined the (full) modular group. We now wish to investigate several kinds of key subgroups of $\SL_2(\Z)$. 

# Congruence Subgroups
We begin by exploring the **principle congruence subgroups**. Fix $n$ a natural number, and define $\Gamma(n)$ as the set

$$ \Gamma(n) = \left\{\begin{pmatrix}a&b\\ c&d\end{pmatrix}\in\SL_2(\Z)\mid a,d\equiv 1\bmod n, c,d\equiv 0\bmod n\right\}.$$

We call $\Gamma(n)$ the principle congruence subgroup of level $n$. Observe that $\Gamma(n)$ is the kernel of the map $\pi_n : \SL_2(\Z) \to \SL_2(\Z/n\Z)$, which is given as the mapping

$$ \begin{pmatrix}a & b \\ c & d\end{pmatrix}\mapsto \begin{pmatrix}a & b \\ c & d\end{pmatrix} \bmod n$$

Now, a **congruence subgroup** $\Gamma \subset \SL_2(\Z)$ is any subgroup of $\SL_2(\Z)$ such that $\Gamma(n)\subset \Gamma \subset \SL_2(\Z)$, for some $n$ natural. 

# Hecke Subgroup
The *Hecke* congruence subgroup $\Gamma_0(n)$ is defined as 

$$ \Gamma_0(n) = \left\{\begin{pmatrix}a&b \\ c&d\end{pmatrix}\in\SL_2(\Z)\mid c\equiv 0\bmod n\right\}.$$

It is immediate that this is indeed a congruence subgroup, as $\Gamma(n)\subset \Gamma_0(n)$. Finally, the last subgroup of note is $\Gamma_1(n)$, given as 

$$ \Gamma_1(n) = \left\{\begin{pmatrix}a&b \\ c&d\end{pmatrix}\in\SL_2(\Z)\mid c\equiv 0\bmod n, d\equiv 1 \bmod n\right\}.$$

It is again immediate that $\Gamma_1(n)$ is as congruence subgroup, as $\Gamma(n) \subset \Gamma_1(n)$. In fact, we have a tower of subgroup inclusions,

$$ \Gamma(n) \subset \Gamma_1(n) \subset \Gamma_0(n).$$

# Index of Congruence Subgroups
An important fact about these subgroups is that they are all finite index! To see this, we begin by computing the index of $\Gamma(n)$. In the proceeding sections, we find the index of each of these subgroups.
## Index of Principle Congruence Subgroups of Level N
Recall that $\Gamma(n) = \ker(\pi_n)$, for $\pi_n$ the map defined prior. Recall from the First Isomorphism Theorem that $\frac{\SL_2(\Z)}{\Gamma(n)} \cong \SL_2(\Z/n\Z)$. It follows that $[\SL_2(\Z) : \Gamma(n)] = |\SL_2(\Z/n\Z)|$. It now suffices to find $|\SL_2(\Z/n\Z)|$. We proceed in four steps. 

### Step One

The first key observation is that $\SL_2(\Z/n\Z)\cong \SL_2(\Z/p_1^{n_1}\Z\times\dots\times \Z/p_k^{n_k}\Z)$ by the Chinese Remainder theorem (recall that the Chinese remainder theorem states that $\Z/n\Z \cong \Z/p_1^{n_1}\Z\times\dots\times\Z/p_k^{n_k}\Z$, where $n=p_1^{n_1}\dots p_k^{n_k}$ is the prime factorization of $n$). Moreover, we find a further isomorphism, namely

$$ \SL_2(\Z/n\Z)\cong \SL_2(\Z/p_1^{n_1}\Z\times\dots\Z/p_k^{n_k}\Z)\cong \SL_2(\Z/p_k^{n_k}\Z)\times\dots\times\SL_2(\Z/p_k^{n_k}\Z)$$
Thus, to find the order of $\SL_2(\Z/n\Z)$, we must find the order of $\SL_2(\Z/p^k\Z)$ for $p$ prime and $k$ natural. We begin with the simplest case: $k=1$. 
### Step Two
We wish to find $|\SL_2(\Z/p\Z) |$ for $p$ prime. We begin by finding $\GL_2(\Z/p\Z)$. Recall that any element in $\GL_2(\Z/p\Z)$ is a matrix with non-zero determinant. To have this, we must have that the column vectors $$u := \begin{pmatrix}a \\ c \end{pmatrix}$$ and $$v := \begin{pmatrix}b \\ d \end{pmatrix}$$ are linearly independent, and neither is the zero vector. We know there is $p^2-1$ options for $u$, as there are $p$ elements in $\Z/p\Z$, and we must exclude the zero vector. Now, to be linearly independent, $v$ cannot be a scalar multiple of $v$, which eliminates $p$ possibilities. Thus, there is $p^2-p$ possible linearly independent vectors for $v$. Thus, $|\GL_2(\Z/p\Z)|=p^2(p^2-p)$.

Now, to find the order of $|\SL_2(\Z/p\Z)|$, consider the determinant map $\det : GL_2(\Z/p\Z) \to (\Z/p\Z)^{\*}$. The group $(\Z/p\Z)^{\*}$ has order $p-1$, and by the first isomorphism theorem, we know that $|\GL_2(\Z/p\Z)|=|\SL_2(\Z/p\Z)||(\Z/p\Z)^{\*}|$, thus $|\SL_2(\Z/p\Z)|=p(p^2-1)$. 
### Step Three
We now proceed by induction. Suppose $|\SL_2(\Z/p^n)| = p^{3n-2}(p^2-1)$. We now aim to show that $|\SL_2(\Z/p^{n+1}\Z)| = p^{3n+1}(p^2-1)$. Consider the map $\pi : \SL_2(\Z/p^{n+1}\Z) \to \SL_2(\Z/p^n)$, given by simply taking a matrix modulo $p^n$. We aim to show that the kernel has cardinality $p^3$. Consider that the kernel is the set of matrices with entries $a,b,c,d\in\Z$, where $a\equiv d \equiv 1 \bmod p^n$, and $c\equiv d \equiv 0 \bmod p^n$. 

Thus, we can rewrite $a = 1+t_1p^n, d=1+t_4p^n, b= t_2p^n, d=t_3p^n$. We can look at the determinant of any of these matrices, and we find that we have a system that must satisfy 
$(1+t_1)(1+t_4)+t_2t_3 \equiv 1 \bmod p^n$. If we expand this, we have $1+t_1+t_4+t_1t_4+t_2t_3\equiv 1\bmod p^n$, which implies that $t_1 \equiv -t_4\bmod p^n$. 

This is particularly important, as before, we have $p^4$ possible matrices to consider, as we had tour free terms, but now, since $a \equiv -d$, we only have three free terms, meaning that the kernel must have order $p^3$. 

We conclude with another application of the First Isomorphism Theorem, finally yielding that $|\SL_2(\Z/p^{n+1}\Z)| = p^{3n+1}(p^2-1)$, and the result is shown.
### Step Four
Finally, we return to our group of interest, $\Gamma(n)$. Since $[\SL_2(\Z) : \Gamma(n)] = |\SL_2(\Z/n\Z)|$, we find the prime factorization $n=p_1^{n_1}\dots p_k^{n_k}$, and find the order of each of the $\SL_2(\Z/p_1^{n_1}\Z)$, each of which is $p_k^{3n_k-2}(p_k^2-1)$, and take their product, yielding

$$ [\SL_2(\Z) : \Gamma(n)] = \prod_{p\mid n}p^{3n-2}(p^2-1)=n^3\prod_{p\mid n}\left(1-\frac{1}{p^2}\right).$$

## Index of Hecke Subgroup
To find the index of the Hecke subgroup of level $n$, we recall that for $H_1 \subset H_2 \subset G$ for $H_1,H_2$ subgroups of $G$, we have that

$$ [G : H_1] = [G : H_2][H_2 : H_1].$$
Applying this to $\Gamma(n), \Gamma_1(n),$ and $\SL_2(\Z)$, we have that
$$ [\SL_2(\Z) : \Gamma(n)] = [\SL_2(\Z) : \Gamma_1(n)][\Gamma_1(n) : \Gamma(n)]$$
Now, consider the homomorpism $\varphi : \Gamma_1(n) \to \Z/n\Z$, given by taking the $b$ entry of this matrix modulo $n$. Observe that the kernel of this map is $\Gamma(n)$, thus, by the First Isomorphism Theorem, we have that $[\Gamma_1(n) : \Gamma(n)] = |\Z/n\Z|$, where $\Z/n\Z$ has $n$ elements. Thus, returning to our chain above, we can substitute the known orders, yielding

$$ n^3\prod_{p|n}\left(1-\frac{1}{p^2}\right) = Kn$$

Thus, $K = n^2\prod_{p\mid n}\left(1-\frac{1}{p^2}\right)$, finally giving that $[\SL_2(\Z):\Gamma_1(n)] = n^2\prod_{p\mid n}\left(1-\frac{1}{p^2}\right)$.

## Index of $\Gamma_0$ 
To find the index of $\Gamma_0(n)$ in $\SL_2(\Z)$, we begin by considering the map $\phi : \Gamma_0(n) \ to (\Z/n\Z)^{\*}$, defined by taking the $d$ entry modulo $n$. Observe that the kernel of this map is $\Gamma_1(n)$. Now, recall that $|(\Z/n\Z)^{\*}| = \varphi(n)$, where $\varphi(n)$ is Euler's totient function. Recall the formula for $\varphi(n)$ is given by

$$\varphi(n) = n\prod_{p\mid n}\left(1-\frac{1}{p}\right). $$

Since $[\SL_2(\Z) : \Gamma_1(n)] = [\SL_2(\Z) : \Gamma_0(n)][\Gamma_0(n) : \Gamma_1(n)]$, and $[\Gamma_0(n):\Gamma_1(n)] = \varphi(n)$ by the First Isomorphism Theorem, it follows that

$$ n^2\prod_{p\mid n}\left(1-\frac{1}{p^2}\right)=K\left(n\prod_{p\mid n}\left(1-\frac{1}{p}\right)\right).$$

Thus,  we divide the lefthand side by the righthand side to find the order. Clearly, the leading coefficient must be $n$, but we need to be careful with our product. To be specific, we have that the product is over

$$ \frac{1-\frac{1}{p^2}}{1-\frac{1}{p}} = \frac{p^2-1}{p-1}=\frac{(p+1)(p-1)}{p-1}=p+1.$$
Thus, our final computation is 

$$ [\SL_2(\Z) : \Gamma_0(n)] = n\prod_{p\mid n}\left(1+\frac{1}{p}\right).$$
