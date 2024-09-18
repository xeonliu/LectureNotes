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

# Fibonacci

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

# Big-O Notation

+ $f = \mathcal{O}(g)$: f grows no faster than g
+ $f = \Omega(g)$ <=> $g = \mathcal{O}(f)$: f grows no slower than g
+ $f = \Theta(g)$: $f = \mathcal{O}(g)$且$f=\Omega(g)$

> Let f (n) and g(n) be functions from positive integers to positive reals. We say f = O(g) (which means that “ f grows no faster than g”) if there is a constant c > 0 such that f (n) ≤ c · g(n)

