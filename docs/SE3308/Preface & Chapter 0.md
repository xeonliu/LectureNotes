+ Part I
	+ numbers, primality, and factoring. 
	+  RSA cryptosystem
	+ divide-and-conquer algorithms for integer multiplication
	+ sorting and median finding
	+ fast Fourier transform.
+ Part II
	+ data structures
	+ graphs
+ Part III 
	+ dynamic programming (a novel approach helps clarify this traditional stumbling block for students) 
	+ linear programming（计算机科学中的数学基础）
+ Part IV
	+ NP-completeness（离散数学）, various heuristics, as well as quantum algorithms

# Fibonacci $F_n$

## Exponential Algorithm
```
function fib1(n):
	if n=0: return 0
	if n=1: return 1
	return fib1(n-1) + fib1(n-2)
```

$$T(n) <= 2$$
for $n<=1$

+ 2 recursive invocation
+ 2 checks
+ 1 addition
$$T(n) = T(n-1) + T(n-2) + 3$$
for $n>1$
显然
$$
T(n)>=F_n
$$
## Polynomial Algorithm
```
function fib(n)
f n=0: return 0
f[0] = 0, f[1] = 1
for i = 2..n:
	f[i] = f[i-1] + f[i-2]
return f[n]
```

The inner loop consists of a single computer step and is executed n - 1 times. Therefore the number of computer steps used by fib2 is linear in n.

$\mathcal{O}(n)$？我们对基本运算定义太模糊。

> we have been too liberal with what we consider a basic step.

考虑到加法对于n位数字需要时间与n成正比，实际结果可能是$\mathcal{O}(n^2)$

> We will see in Chapter 1 that the addition of two n-bit numbers takes time roughly proportional to n;

> Thus fib1, which performs about Fn additions, actually uses a number of basic steps roughly proportional to nFn. Likewise, the number of steps taken by fib2 is proportional to n^2, **still polynomial** in n and therefore **exponentially superior** to fib1.


# Big-O Notation

+ $f = \mathcal{O}(g)$: f grows no faster than g
+ $f = \Omega(g)$ <=> $g = \mathcal{O}(f)$: f grows no slower than g
+ $f = \Theta(g)$: $f = \mathcal{O}(g)$且$f=\Omega(g)$

> Let f (n) and g(n) be functions from positive integers to positive reals. We say f = O(g) (which means that “ f grows no faster than g”) if there is a constant c > 0 such that f (n) ≤ c · g(n)

![](assets/Pasted%20image%2020240919171834.png)



![](assets/Pasted%20image%2020240919171922.png)

A
B不对，$sin(x)$ 与$cos(x)$

![](assets/Pasted%20image%2020240919172228.png)
![](assets/Pasted%20image%2020240919172732.png)

$n!$ is $2^{\Theta(nlog_n)}$
