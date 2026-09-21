# Convex Optimization — Lecture 1

## 1. Mathematical optimization

A mathematical optimization problem has the form

$$
\begin{aligned}
\operatorname{minimize}_{x \in \mathbb{R}^n} \quad & f_0(x) \\
\text{subject to} \quad & f_i(x) \le b_i, \qquad i=1,\ldots,m.
\end{aligned}
$$

Here:

- $x=(x_1,\ldots,x_n)$ is the **decision variable**;
- $f_0:\mathbb{R}^n\to\mathbb{R}$ is the **objective function**;
- $f_i(x)\le b_i$ are the **constraints**.

An optimal solution $x^\star$ is a feasible point with the smallest objective value.

## 2. Least squares

For an overdetermined system $Ax\approx b$, the least-squares problem is

$$
\operatorname{minimize}_x \; \|Ax-b\|_2^2.
$$

If $A$ has full column rank, the unique solution is

$$
x^\star=(A^\mathsf{T}A)^{-1}A^\mathsf{T}b.
$$

More generally, a minimum-norm solution is $x^\star=A^\dagger b$, where $A^\dagger$ is the Moore–Penrose pseudoinverse.

## 3. Linear programming

A linear program (LP) has a linear objective and linear constraints:

$$
\begin{aligned}
\operatorname{minimize}_x \quad & c^\mathsf{T}x \\
\text{subject to} \quad & a_i^\mathsf{T}x \le b_i, \qquad i=1,\ldots,m.
\end{aligned}
$$

## 4. Convex optimization

A function $f$ is convex if, for all $x,y$ in its domain and every $\theta\in[0,1]$,

$$
f\!\left(\theta x+(1-\theta)y\right)
\le
\theta f(x)+(1-\theta)f(y).
$$

A standard convex optimization problem is

$$
\begin{aligned}
\operatorname{minimize}_x \quad & f_0(x) \\
\text{subject to} \quad & f_i(x)\le 0, \qquad i=1,\ldots,m,\\
& Ax=b,
\end{aligned}
$$

where $f_0,\ldots,f_m$ are convex and the equality constraints are affine. For a convex problem, every locally optimal solution is globally optimal.

## 5. Example: optimal illumination

Suppose $m$ lamps illuminate $n$ small, flat surface patches. Let $p_j$ denote the power of lamp $j$. The illumination at patch $k$ is modeled as

$$
I_k=\sum_{j=1}^{m}a_{kj}p_j,
\qquad
a_{kj}=r_{kj}^{-2}\max\{\cos\theta_{kj},0\},
$$

where $r_{kj}$ is the distance from lamp $j$ to patch $k$, and $\theta_{kj}$ is the incidence angle. Thus, illumination depends linearly on the lamp powers.

Given a desired illumination $I_{\mathrm{des}}>0$ and a maximum lamp power $p_{\max}$, we want uniform illumination while satisfying

$$
0\le p_j\le p_{\max}, \qquad j=1,\ldots,m.
$$

The logarithmic objective below also requires $I_k>0$ for every patch; equivalently, it assigns infinite cost when a patch receives no illumination.

### 5.1 Relative-error objective

A natural objective minimizes the largest multiplicative illumination error:

$$
\begin{aligned}
\operatorname{minimize}_p \quad &
\max_{k=1,\ldots,n}\left|\log I_k-\log I_{\mathrm{des}}\right| \\
\text{subject to} \quad & 0\le p_j\le p_{\max},
\qquad j=1,\ldots,m.
\end{aligned}
$$

Because

$$
\exp\!\left(\left|\log(I_k/I_{\mathrm{des}})\right|\right)
=
\max\left\{\frac{I_k}{I_{\mathrm{des}}},
\frac{I_{\mathrm{des}}}{I_k}\right\},
$$

the problem has the equivalent convex formulation

$$
\begin{aligned}
\operatorname{minimize}_p \quad &
f_0(p)=\max_{k=1,\ldots,n}h\!\left(\frac{I_k}{I_{\mathrm{des}}}\right) \\
\text{subject to} \quad & 0\le p_j\le p_{\max},
\qquad j=1,\ldots,m,
\end{aligned}
$$

with

$$
h(u)=\max\{u,1/u\}, \qquad u>0.
$$

The function $h$ is convex on $u>0$, and the pointwise maximum of convex functions is convex. Therefore, $f_0$ is convex.

### 5.2 Possible solution approaches

1. **Uniform power:** set $p_j=p$ for every lamp and optimize the single scalar $p$.

2. **Least squares:** solve

   $$
   \operatorname{minimize}_p \;
   \sum_{k=1}^{n}(I_k-I_{\mathrm{des}})^2,
   $$

   then clip any infeasible power to the interval $[0,p_{\max}]$. Clipping is simple but generally does not produce the constrained optimum.

3. **Weighted least squares:** solve

   $$
   \operatorname{minimize}_p \;
   \sum_{k=1}^{n}(I_k-I_{\mathrm{des}})^2
   +\sum_{j=1}^{m}w_j\left(p_j-\frac{p_{\max}}{2}\right)^2,
   $$

   and iteratively adjust the weights $w_j$ to encourage $0\le p_j\le p_{\max}$.

4. **Linear programming:** minimize the largest absolute illumination error:

   $$
   \begin{aligned}
   \operatorname{minimize}_p \quad &
   \max_{k=1,\ldots,n}|I_k-I_{\mathrm{des}}| \\
   \text{subject to} \quad & 0\le p_j\le p_{\max},
   \qquad j=1,\ldots,m.
   \end{aligned}
   $$

   Introducing an epigraph variable $t$ gives the LP

   $$
   \begin{aligned}
   \operatorname{minimize}_{p,t} \quad & t \\
   \text{subject to} \quad
   & -t\le a_k^\mathsf{T}p-I_{\mathrm{des}}\le t,
   \qquad k=1,\ldots,n,\\
   & 0\le p_j\le p_{\max},
   \qquad j=1,\ldots,m.
   \end{aligned}
   $$

5. **Convex optimization:** solve the multiplicative-error formulation in Section 5.1 directly. Unlike the heuristic approaches above, this finds the exact optimum for the chosen relative-error objective, typically at a computational cost comparable to a modest number of least-squares solves.

## Key takeaway

Least squares and linear programming are important special cases of convex optimization. Convexity is valuable because it makes global optimization tractable: once the problem is expressed in a valid convex form, efficient algorithms can reliably find a global optimum.
