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

## ==Definition($\beta$-reducing)==
Any term of form  $(\lambda x.M)N$ is called a *$\beta$-redex* and the corresponding term  $[N/x]M$ is called its *contractum*. We call the act that replace the $\beta$-redex by its contractum  in $P$ a $\beta$-contract, noted as 
$$P \triangleright_{1\beta} Q$$
If $P$ can $\beta$-contract to $Q$ within finite steps, we say $P$ can $\beta$-reduce to $Q$ and noted:
$$P \triangleright_{\beta} Q$$

---

## Examples of $\beta$-reducing

- $(\lambda x.x(xy))N \quad \triangleright_{\beta} \quad N(Ny)$
- $(\lambda x.y)N \quad \triangleright_{\beta} \quad y$
- $(\lambda x.(\lambda y.yx)z)v \quad \triangleright_{\beta} \quad (\lambda y.yv)z \quad \triangleright_{\beta} \quad zv$
- $(\lambda x.xx)(\lambda x.xx) \quad \triangleright_{\beta} \quad (\lambda x.xx)(\lambda x.xx)$
- $(\lambda x.xxy)$

---


# Introducing ==Gaia== theme

#### Marp's new slide theme

###### Created by [Yuki Hattori (@yhatt)](https://github.com/yhatt)

---
<!-- *template: invert -->

> In Greek mythology, **Gaia** also spelled **Gaea**, was the personification of the Earth and one of the Greek primordial deities.
>
> <small>-- *[Gaia (mythology) - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Gaia_%28mythology%29)*</small>

---
<!-- page_number: true -->

# Overview

**Gaia** is the beautiful presentation theme on Marp!

- ==**New features**==
	1. Title Slides
	2. Highlight
	3. Color scheme

---

# How to use

#### From menu

Select menu: *View :arrow_right: Theme :arrow_right: Gaia*

#### Use directive

Set `gaia` theme by `$theme` Global Directive.

```
<!-- $theme: gaia -->
```

---

# Basic example 1

**Lorem ipsum** dolor *sit* amet, ***consectetur*** adipiscing elit, sed do `eiusmod` tempor ==incididunt== ut labore et dolore ~~magna aliqua~~. :smile:

> Stay Hungry. Stay Foolish. <small>_--Steve Jobs (2005)_</small>

- List A
	1. [Sub list](https://yhatt.github.io/marp/)
	1. Sub list
		- _More Sub list_

---

# Basic example 2

```javascript
document.write('Hello, world!');
```

|table|layout|example|
|:--|:-:|--:|
|align to left|align to center|align to right|
|:arrow_left: left|:arrow_left: center :arrow_right:|right :arrow_right:|

![70% center](../images/marp.png)

---
<!-- *template: gaia -->

## Introduce new features!!

# ==1.== Title Slides

---

# ==e.g.== This page :yum:

---

## ==Apply centering== to the page<br />that has only headings!

##### Useful to title slide. :laughing:

---

> **==Tips:==**
> Apply vertical centering to quote only page too.

---
<!-- *template: gaia -->

# ==2.== Highlight

---
## Highlight Markup

You can use `==` for ==highlighting blue==.

```markdown
==This is highlight markup.==
```

#### Notice

*Marp would show <span style="background-color:yellow;">yellow marker highlight</span> in Markdown view or default slide theme.*

---
<!-- *template: gaia -->

# ==3.== Color scheme templates
---
# ==Color== scheme templates

Change color scheme *by `template` page directive.*

```
<!-- template: default -->
```

- **Default** :arrow_left: This page
- Invert
- Gaia (Theme color)

---

# Hello,world

this is bria

$$ \sum_{i=1}^{n}i$$

---

<!-- *template: invert -->
# ==Color== scheme templates

Change color scheme *by `template` page directive.*

```
<!-- template: invert -->
```

- Default
- **Invert** :arrow_left: This page
- Gaia (Theme color)

---
<!-- *template: gaia -->
# ==Color== scheme templates

Change color scheme *by `template` page directive.*

```
<!-- template: gaia -->
```

- Default
- Invert
- **Gaia** (Theme color) :arrow_left: This page

---
<!-- *template: invert -->

# Templates can use<br />to ==per pages==!

##### with using temporally page directive `<!-- *template: invert -->`

---
<!-- template: gaia -->

# ==That's all!==

## Let's create beautiful slides<br />with ==Marp== + ==Gaia== theme!

---

#### `<!-- $theme: gaia -->` of Marp

###### [![](../images/marp.png)](https://yhatt.github.io/marp)

#### https://yhatt.github.io/marp
