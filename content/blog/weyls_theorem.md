+++
title = "Weyl's Theorem"
date = 2024-12-08
updated = 2024-12-10
[taxonomies]
tags = ["Math", "Lie algebra"]
+++

## Claim

Let $L$ be a semisimple Lie algebra over $\mathbb{F}$, $V$ a finite dimensional linear space, $\phi: L \to \mathfrak{gl}(V)$ a representation. Then, $\phi$ is completely reducible.

## Proof

We show every submodule $W \subset V$ has a complement, i.e. $\exists X \subset V$ submod, s.t. $V = W \oplus X$ using induction over $\dim{W}$.

### Case 1: $\dim V/W = 1$

The action of $L$ on $V/W \cong \mathbb{F}$ is trivial.

#### Case 1-a: $W$ is reducible

Let $0 \neq W' \subsetneq W$ be a submodule, then $W/W' \subset V/W'$ submod, $\dim((V/W') / (W/W')) = \dim(V/W) = 1$.

Since $\dim (W/W') < \dim W$, we can use the induction hypothesis to conclude $W/W'$ has a complement, i.e.
$\exists \tilde{W}/W' \subset V/W'$ submod, s.t. $V/W' = W/W' \oplus \tilde{W}/W'$.

Further, $\dim W' < \dim W$ and $\dim (\tilde{W}/W') = 1$.

Applying induction hypothesis again to get $\exists X \subset \tilde{W}$ submod, s.t. $\tilde{W} = W' \oplus X$.

Then,

- $\dim X = 1, \dim W = \dim V - 1.$ Therefore, $\dim V = \dim W + \dim X$
- $W \cap X = W \cap (X \cap W') = (W \cap W') \cap X \subset W' \cap X = 0.$

$\therefore V = W \oplus X$

#### Case 1-b: $W$ is irreducible

We can assume $\phi$ is faithful, since if not, $\phi' : L/\ker \phi \to \mathfrak{gl}(V)$ is so.

Let $c := c_\phi$ be the Casimir element of $\phi$. Then $v \mapsto cv$ is an L-mod endmorphism.  
($\because \forall x \in L, \forall v \in V, c (\phi(x).v)= \phi(x) (cv)$)

- $\ker c \subset V$ is an L-submod.
- $c$ maps $V$ into $W$. In particular, $\mathrm{Tr}_{V/W} (c) = 0$
  - The action of $L$ on $V/W \cong \mathbb{F}$ is trivial, so $L.V \subset W$, i.e. $\forall x \in L, \phi(x) V \subset W$. Therefore, $cV \subset W$

- $c$ acts as a nonzero scalar on $W$
  - $W$ is irred, $c$ is the Casimir element, Shur's lemma.
  - $\mathrm{Tr}_V(c) \neq 0, \mathrm{Tr} _{V/W}(c) = 0$ Therefore, $\mathrm{Tr}_W (c) \neq 0.$

Hence,

- $\dim \ker c= \dim V - \dim W = 1$
  - $c: V \to W$ is a surjective L-mod morphism.
- $W \cap \ker c = 0$

i.e. $V = W \oplus \ker c$

### Case 2: General case

Let $\mathrm{Hom}(V, W)$ be the set of linear maps from $V$ to $W$. Then, $\mathrm{Hom}(V, W)$ is an L-mod with action
$$(x.f)(v) := x.f(v) - f(x.v)$$

Let

- $\mathcal{V} := \set{f \in \mathrm{Hom}(V, W);  f|_W \text{is a scalar mult.}}$.
- $\mathcal{W} := \set{f \in \mathcal{V}; f|_W = 0} \subset \mathcal{V}$.

Then

- $\mathcal{V}, \mathcal{W}$ are L-mods. Further, $L.\mathcal{V} \subset \mathcal{W}$
  - Let $f|_W = a 1_W \in \mathcal{V}$. Then, $\forall x \in L, \forall w \in W, (x.f)(w) = x.f(w) - f(x.w) = x.(aw) - a(x.w) = 0, \therefore x.f|_W = 0$
- $\dim (\mathcal{V} / \mathcal{W}) = 1$
  - $\mathcal{W} = \ker(f \space s.t. \space f|_W = a1_W \mapsto a)$, and the morphism is surjective.

Applying case 1, there exists $f: V \to W$ linear, s.t.
$$\mathcal{V} = \mathcal{W} \oplus \langle f \rangle$$
We can choose $f$ to satisfy $f|_W = 1_W$ by scaling $f$ if needed.

Since $L.\mathcal{V} \subset \mathcal{W}$, $L.f = 0$ i.e. $\forall x \in L, \forall v \in V, x.f(v) - f(x.v) = (x.f)(v) = 0.$  
$\therefore f$ is an L-morphism.  
$\therefore \ker f \subset V$ is an L-submod.

- $\ker f \cap W = 0$
  - $f|_W = 1_W$
- $\dim V = \dim W + \dim \langle f \rangle$
  - $f: V \to W$ is surjective.

$\therefore V = W \oplus \ker f$

## Reference

[Introduction to Lie Algebras and Representation Theory](https://link.springer.com/book/10.1007/978-1-4612-6398-2)
