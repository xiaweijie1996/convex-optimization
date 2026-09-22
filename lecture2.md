## Affine set

For two distinct points $x_1, x_2$, the points of the form

$$
x=\theta x_1+(1-\theta)x_2, \qquad \theta\in\mathbb{R}
$$

form the **line** through $x_1$ and $x_2$. (Restricting to $\theta\in[0,1]$
gives only the **line segment** between them.)

A set $C$ is **affine** if it contains the line through any two distinct
points in the set, i.e. for any $x_1,x_2\in C$ and $\theta\in\mathbb{R}$,

$$
\theta x_1+(1-\theta)x_2\in C.
$$

Intuitively, an affine set is "flat": along with any two points it contains
the entire line through them, not just the segment between them.

**Example:** the solution set of a system of linear equations,
$C=\{x\mid Ax=b\}$, is affine. Conversely, every affine set can be written
this way. (Note: an affine set need not pass through the origin — it is a
subspace only when it does.)

## Convex set

A set $C$ is **convex** if it contains the line *segment* between any two
points in the set, i.e. for any $x_1,x_2\in C$ and $0\leq\theta\leq1$,

$$
\theta x_1+(1-\theta)x_2\in C.
$$

So convexity only requires closure under $\theta\in[0,1]$, whereas an affine
set requires closure under all $\theta\in\mathbb{R}$. This makes every
affine set convex, but not every convex set affine — e.g. a ball or a
polyhedron is convex but not affine.

## Convex combination and convex hull

A **convex combination** of $x_1,\ldots,x_k$ is any point of the form

$$
x=\theta_1x_1+\theta_2x_2+\cdots+\theta_kx_k,
$$

where

$$
\theta_i\geq0,
\qquad
\theta_1+\cdots+\theta_k=1.
$$

The **convex hull** of a set $S$, denoted $\operatorname{conv}S$, is the set of
all convex combinations of points in $S$:

$$
\operatorname{conv}S
=
\left\{
\sum_{i=1}^k\theta_i x_i
\;\middle|\;
x_i\in S,\ \theta_i\geq0,\ \sum_{i=1}^k\theta_i=1
\right\}.
$$

Equivalently, $\operatorname{conv}S$ is the smallest convex set containing
$S$.

## Convex cone

A **conic combination**, or **nonnegative combination**, of
$x_1,\ldots,x_k$ is any point of the form

$$
x=\theta_1x_1+\theta_2x_2+\cdots+\theta_kx_k,
\qquad \theta_i\geq0.
$$

Unlike a convex combination, the coefficients do not have to sum to one.

A **convex cone** is a set that contains every conic combination of its
points. Thus, if $x_1,x_2\in K$ and $\theta_1,\theta_2\geq0$, then

$$
\theta_1x_1+\theta_2x_2\in K.
$$

In particular, a nonempty convex cone contains the origin and is closed under
nonnegative scaling and addition.
