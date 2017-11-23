<!-- $theme: gaia -->

# A Brief Introduction to 
# $\lambda$-calculas 
#### by 丁尧尧

---

## How to express a function ?

---

Usually we define a function like this:
$$f(x,y) = x - y$$
$$g(x) = e^x$$
Then use it like this:
$$f(5,1) = 5 - 1 = 4$$
$$g(0) = e^0 = 1 $$

---

## Is the name of a function so important ?

---

We can define the two functions:$f(x,y) = x-y$ and $g(x)=e^x$ like this:
$$(x,y\rightarrow x-y)$$
$$(x\rightarrow e^x) $$
and use them like this:
$$(x,y\rightarrow x-y)(5,1) = 5 - 1 = 4$$
$$(x\rightarrow e^x)(1) = e$$

---

## Is the ability to define functions with more than one parament necessary?

---
For function:
$$ f(x,y) = x - y$$
We can also define a function like this:
$$
	(x\rightarrow (y\rightarrow x-y))
$$
The function map x to another function ,which maps  y to x - y.
(Now we can see the power to write the function itself as the name of it)

---

We call $(x\rightarrow x-1)$ an **anonymous function**.

And the method that using 
$$ (x\rightarrow (y \rightarrow x - y))$$
to replace the function
$$f(x,y) = x - y$$
is called **Currying**

---

## Let's see the formal definition of 
## $\lambda$-calculus

---

## ==Definition($\lambda$-terms)==

Assume there is a sequence of expressions $v_0,v_{00},v_{000},...$ called **variables**. The set of expression called **$\lambda$-terms** is defined as follows:

- all variables are $\lambda$-terms (called **atoms**);
- if $M$ and $N$ are any $\lambda$-terms, then $(MN)$ is a $\lambda$-term (called  an **Application**);
- if $M$ is any $\lambda$-term and $x$ is any variable, then $(\lambda x.M)$ is a $\lambda$-term (called an **Abstraction**).

---

## Examples of $\lambda$-term
If $x,y,z$ are any distinc variables, the following are $\lambda$-terms:
1. $(\lambda v_0.(v_0v_{00}))$
2. $(\lambda x.(xy))$
3. $(x(\lambda x.(\lambda x.x)))$
4. $((\lambda y.y)(\lambda x.(xy)))$
5. $(\lambda x.(yz))$

---

### For simplicity, we omit some unnecessary parentheses.
|Original expressions|Shorter expressions|
|:------------------:|:-----------------:|
| $(\lambda x.(\lambda y.(((yx)a)b)))$ | $\lambda x.\lambda y. y x a b$|
| $(((\lambda x.(\lambda y.(yx)))a)b)$ | $(\lambda x.\lambda y. yx) a b$|
|$(\lambda x.(\lambda y.((ab)(\lambda z.z))))$|$\lambda x.\lambda y.ab \lambda z.z$|

---

## ==Definition(Free variable, FV)==

For any $\lambda$-term $P$, we can define its free variables $FV(P)$ such as:

- $FV(x) = \{x\}$
- $FV(MN) = FV(M) \cup FV(N)$
- $FV(\lambda x.M) = FV(M) - \{ x \}$

---

## Examples of free variables
- $FV(\lambda x. \lambda y. xyab) = \{ a,b\}$
- $FV(abcd) = \{a,b,c,d \}$
- $FV(xy\lambda y. \lambda x.x) = \{x, y\}$

---

## ==Definition(Substitution)==
For any $M, N, x$, define $[N/x]M$ as follows:
1. $[N/x]x \equiv N$
2. $[N/x]y \equiv y$
3. $[N/x](PQ) \equiv ([N/x]P [N/x]Q)$
4. $[N/x](\lambda x.P) \equiv \lambda x.P$
5. $[N/x](\lambda y.P) \equiv \lambda y.P \quad (x \notin FV(P))$
6. $[N/x](\lambda y.P) \equiv \lambda y.[N/x]P$
	$(x \in FV(P)$ and $y \notin FV(N))$

---
7. $[N/x](\lambda y.P) \equiv \lambda [N/x][z/y]P$
   $(x \in FV(P)$ and $y \in FV(N))$

## Examples of substitution
- $[(uv)/x](\lambda y.x(\lambda w.vwx))$ 
 $\equiv \lambda y.(uv)(\lambda w. vw(uv))$
- $[(\lambda y.vy)/x](y(\lambda v. xv))$
 $\equiv y(\lambda w.(\lambda y.vy)w)$

---

## ==Definition($\alpha$-conversion)==
Let a $\lambda$-term $P$ contain an occurrence of $\lambda x.M$ and let $y \notin FV(M)$. The act of replacing 
$$\lambda x. M$$
by
$$\lambda y.[y/x]M$$ 
is called an **$\alpha$-conversion.** If $P$ can convert to $Q$ within finite $\alpha$-conversion, we say $P$ $\alpha$-convert to $Q$, noted as $P \equiv_{\alpha} Q$.

---

## Examples of $\alpha$-conversion

- $\lambda x.x \equiv \lambda y.y$
- $\lambda x.\lambda y.x(xy) \equiv_{\alpha} \lambda u.\lambda v. u(uv)$

---

## ==Definition($\beta$-reducing)==
Any term of form  $(\lambda x.M)N$ is called a *$\beta$-redex* and the corresponding term  $[N/x]M$ is called its *contractum*. We call the act that replace the $\beta$-redex by its contractum  in $P$ a $\beta$-contract, noted as 
$$P \triangleright_{1\beta} Q$$
If $P$ can $\beta$-contracts or $\alpha$-converses to $Q$ within finite steps, we say $P$ can $\beta$-reduce to $Q$ and noted:
$$P \triangleright_{\beta} Q$$

---

## Examples of $\beta$-reducing

- $(\lambda x.x(xy))N \quad \triangleright_{\beta} \quad N(Ny)$
- $(\lambda x.y)N \quad \triangleright_{\beta} \quad y$
- $(\lambda x.(\lambda y.yx)z)v \quad \triangleright_{\beta} \quad (\lambda y.yv)z \quad \triangleright_{\beta} \quad zv$
- $(\lambda x.xx)(\lambda x.xx) \quad \triangleright_{\beta} \quad (\lambda x.xx)(\lambda x.xx)$
- $(\lambda x.xxy)(\lambda x.xxy) \quad \triangleright_{\beta} \quad (\lambda x.xxy)(\lambda x.xxy)y$

---

## ==Definition($\beta$-normal form)==

A $\lambda$-term $Q$ which contains no $\beta$-redexes is called a **$\beta$-normal form**. If $P$ can $\beta$-reduces to a $\beta$-normal form $Q$, we say $Q$ is a $\beta$-normal form of $P$. 

---

## Examples of $\beta$-normal form
- $zv$ is a $\beta$-normal form of $(\lambda x.(\lambda y.yx)z)v$
- Let $L \equiv (\lambda x.xxy)(\lambda x.xxy)$ and we have
  $L \quad \triangleright \quad Ly \quad \triangleright \quad Lyy \quad \triangleright \quad ...$
  So $L$ has no $\beta$-normal form.
- Let $P \equiv (\lambda u.v)L$.
  1. $P \quad \triangleright_{\beta} \quad v$
  2. $P \quad \triangleright_{\beta} \quad (\lambda u.v)Ly \quad \triangleright_{\beta} \quad (\lambda u.v)Lyy\quad \triangleright_{\beta} \quad \cdots$ 

---

## There are some great results

---

### ==Fact 1==

The relation $\equiv_{\alpha}$ is an equivalence relation.

### ==Fact 2(Church-Rosser Theorem)==

If $P \triangleright_{\beta} M$ and $Q \triangleright_{\beta} N$, then exist a $\lambda$-term $T$ such:
$$
	M \triangleright_{\beta} T \quad and \quad N \triangleright_{\beta} T
$$

### ==Fact 3==

If we always $\beta$-reduce the leftest-outest $\beta$-redex and this process can't stop, any order of reduction will not stop.

---

## Why can we say the "computing ability" of $\beta$-calculus is equal to the turing machine ?

---

## Code number and basic arithmetic

|Name|$\beta$-terms|
|:-:|:-:|
|ZERO|$\lambda f.\lambda x.x$|
|SUCC|$\lambda n.\lambda f.\lambda x.f\,(n\,f\,x)$|
|PLUS|$\lambda m.\lambda n.m\,\text{SUCC}\,n$|
|MULT|$\lambda m.\lambda n.\lambda f.m\,(n\,f)$|
|POW |$\lambda b.\lambda e.e\,b$|
|PRED|$\lambda n.\lambda f.\lambda x.n\,(\lambda g.\lambda h.h\,(g\,f))\,(\lambda u.x)\,(\lambda u.u)$|
|SUB |$\lambda m.\lambda n.n\,\text{PRED}\,m$|

---

## Code boolean and basic logic

|Name|$\beta$-terms|
|:-:|:-:|
|TRUE  | $\lambda x.\lambda y.x$|
|FALSE | $\lambda x.\lambda y.y$|
|AND   | $\lambda p.\lambda q.p q p$|
|OR    | $\lambda p.\lambda q.p p q$|
|NOT   | $\lambda p.\lambda a.\lambda b.p b a$|
|IF    | $\lambda p.\lambda a.\lambda b.p a b$|


---

## Combination of number and boolean

|Name|$\beta$-terms|
|:-:|:-:|
|ISZERO |$\lambda n.n (\lambda x.\text{FALSE}) \text{TRUE}$|
|LEQ    |$\lambda m.\lambda n. \text{ISZERO} (\text{SUB} m n)$|
|EQ     |$\lambda m.\lambda n. \text{AND} (\text{LEQ} m n) (\text{LEQ} n m)$|

---

## Code repetition (recursion)

The fixed points:
$$
Y \equiv (\lambda g.(\lambda x.g (x x)) \lambda x.g (x x))
$$
$Y$ follows:
$$
	Y F =_{\beta} F(Y F)
$$

---

## Example 

Now we are going to create the factorial function as example:
$$
f(n) = n(n-1)(n-2)\cdots
$$
An intuitive idea is:
```text
FACT = \n. If (ISZERO n) ONE (MULT n (FACT (PRED n)))
```
But we can't define such term beacuse it's self-recurisive.

---

## Example

The right answer is:
```text
FACT2 = \f. \n. IF (ISZERO n) ONE (MULT n (f (PRED n)))
FACT = Y FACT2
```
---

## Example

Let's see what happend when we call "FACT THREE":
```text
FACT THREE
= Y FACT2 THREE
= FACT2(Y FACT2) THREE
= IF(ISZERO THREE) ONE (MULT THREE(Y FACT2 TWO))
= MULT THREE(Y FACT2 TWO)
= ...
= MULT THREE (MULT TWO (MULT ONE ONE))
```
---

## Reference
- Lambda-Calculus and Combinators,an Introduction, 
  by J. ROGER HINDLEY and JONATHAN P. SELDIN
- 让我们谈谈 λ 演算
  by 王盛颐
- Lambda calculus - Wikipedia

Slide is made by Marp(a markdown editor)
## Any question ?
