# Addition
### Algo 1: repeated increments
Start with x, and increment y times
say x, y each have n digits

+ increments <= n steps（进位）
+ y increments

total steps: y * n <= 10^n * n 约等于 10^n

（y  at most 10^n）

### Algo 2 竖式相加
```
456
141 +
-----
```
大约n次（进位算是附加在两位运算之间的，对同一位置的两个数字，最后成为n的常数项）

$f = \mathcal{O}(n)$

最优：
+ 答案就有n位，至少n步
+ 输入就有2n位，肯定要读
反正，假设<=2n步，有的输入没有读。
那么对不同的两个输入可能输出相同答案，不对。

# Multiplication
given x, y in base 10.return digits of `x*y` in base 10

### Algo 1: Reapted addition
add x over and over, y times

Steps of add * y = n 10^n

### Algo 2：竖式

n^2

`x*y` <= 2n digits？

### Algo 3: Divide and Conqure (Recursion)

分而治之：例子Merge sort

```
x = 5 1 4 2
y = 2 0 4 8 

y_high = 2 0 y_low = 4 8
```

Recurrence Relation
$T(n)$ are steps to mult two n-digit nums using Alg 3.

$$T(n)<=  $$

![](assets/Pasted%20image%2020240918232107.png)

 