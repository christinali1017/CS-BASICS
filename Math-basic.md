###GCD && LCM
---
Greatest common divisor and Lowest common multiple

```java
public static long gcd(long a, long b) {
    while (b > 0) {
        long temp = b;
        b = a % b; 
        a = temp;
    }
    return a;
}

public static long lcm(long a, long b) {
    return a * (b / gcd(a, b));
}

```


###Arithmetic progression(等差数列)

- A sequence of numbers such that the difference between the consecutive terms is constant.

- Example: 5, 7, 9, 11, 13, 15 … 

- Induction: Suppose d is the difference. **An = A1 + (n - 1) * d** Or **An = Am + (n - m) * d**

- **Sum**

    * To derive the above formula, begin by expressing the arithmetic series in two different ways:

    * Sn=a1+(a1+d)+(a1+2d)+....+(a1+(n-2)d)+(a1+(n-1)d)
    * Sn=(an-(n-1)d)+(an-(n-2)d)+...+(an - 2d)+(an-d)+an.
    
    * Adding both sides of the two equations, all terms involving d cancel:**2Sn=n(a1 + an)**, which is **Sn = n * (A1 + An) / 2**


###Geometric progression(等比数列）
---

- A sequence of numbers where each term after the first is found by multiplying the previous one by a fixed, non-zero number called the common ratio.

- Example: 2, 6, 18, 54, ...

- Induction: Suppose R is the ratio. An = A1 * R ^ (n - 1)

- Sum: S = A1 * (1 - R^n) / (1 - R)

- Derivation:
https://en.wikipedia.org/wiki/Geometric_progression




###Sum of square numbers
---

```
1 ^ 2 + 2 ^ 2 + ... + n ^ 2 = n (n + 1) (2n + 1) / 6
```








 