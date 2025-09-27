# Number Systems

>Status: 🟡 Draft – foundational summary added, expand with more solved examples and drill sets.

## 🚀 Quick Overview

Number systems govern how values are represented, decomposed, and manipulated. Mastering them unlocks speed in divisibility, remainders, factorisation, and conversions across bases.

- **Place value** defines contribution of each digit based on position.
- **Base conversions** bridge questions that move between binary, octal, decimal, or hexadecimal systems.
- **Divisibility tests & digital sums** allow lightning-fast validation.
- **Remainder theorems** (Euler/Fermat/Chinese remainder) supercharge modular arithmetic questions.

## 📚 Core Concepts Checklist

- [ ] Classification: natural, whole, integers, rationals, irrationals, real, complex.
- [ ] Representation of integers and fractions in different bases.
- [ ] Recurring decimals ↔ fractions conversion.
- [ ] Highest Common Factor (HCF) / Least Common Multiple (LCM) of integers.
- [ ] Prime factorisation, trailing zeros, power of a prime in n!.
- [ ] Remainder calculations using Euler's totient / Fermat's little theorem.
- [ ] Properties of digital roots, casting out nines, alternating sum tests.

## 🧮 Formula & Trick Sheet

| Concept | Shortcut |
|---------|----------|
| Sum of first n natural numbers | $S = \frac{n(n+1)}{2}$ |
| Sum of first n odd numbers | $S = n^2$ |
| Highest power of prime $p$ in $n!$ | $\sum\limits_{k=1}^{\infty} \left\lfloor \frac{n}{p^k} \right\rfloor$ |
| Trailing zeros in $n!$ | Count of 5s in prime factorisation of $n!$ |
| Fermat's little theorem | $a^{p-1} \equiv 1 \pmod p$ (p prime, gcd(a,p)=1) |
| Euler's totient | $a^{\phi(n)} \equiv 1 \pmod n$ (gcd(a,n)=1) |
| Digit root (decimal) | $\text{dr}(n) = 1 + ((n-1) \bmod 9)$ |

## 🧠 Sample Problems

### 1. Highest Power of 12 in 50!
Find the largest exponent $k$ such that $12^k$ divides $50!$.

**Solution Sketch:** Factor 12 as $2^2 \times 3$. Compute powers of 2 and 3 in $50!$.

- Power of 2: $\lfloor \frac{50}{2} \rfloor + \lfloor \frac{50}{4} \rfloor + \lfloor \frac{50}{8} \rfloor + \lfloor \frac{50}{16} \rfloor + \lfloor \frac{50}{32} \rfloor = 25 + 12 + 6 + 3 + 1 = 47$
- Power of 3: $\lfloor \frac{50}{3} \rfloor + \lfloor \frac{50}{9} \rfloor + \lfloor \frac{50}{27} \rfloor = 16 + 5 + 1 = 22$

Divide by respective exponents in 12: $\lfloor 47/2 \rfloor = 23$, $\lfloor 22/1 \rfloor = 22$. Smallest value = **22**.

### 2. Remainder When $7^{222}$ is Divided by 240

**Solution Sketch:** Prime-factorise $240 = 2^4 \cdot 3 \cdot 5$ and use the Chinese Remainder Theorem.
- Mod $16$: $7^2 \equiv 1 \pmod{16} \Rightarrow 7^{222} \equiv 1^{111} \equiv 1$.
- Mod $3$: $7 \equiv 1 \pmod 3 \Rightarrow 7^{222} \equiv 1$.
- Mod $5$: $7 \equiv 2 \pmod 5$, Euler: $2^4 \equiv 1 \Rightarrow 7^{222} \equiv 2^{222} \equiv (2^4)^{55}\cdot 2^2 \equiv 4$.

Solve system: $x \equiv 1 \pmod{16}$, $x \equiv 1 \pmod 3$, $x \equiv 4 \pmod 5$.
- Combine mod 16 and 3 ⇒ lcm 48: solutions are $1, 49, 97, \dots$.
- Find $x \equiv 4 \pmod 5$: $49 \equiv 4$ works.

Therefore, remainder = **49**.

## 🎯 Practice Ladder

| Level | Problems | Source |
|-------|----------|--------|
| Warm-up | 10 question drill on classification & divisibility | IndiaBix → Quantitative → Number System |
| Core | "Power of prime & trailing zeros" set | PrepInsta Premium – Number System |
| Challenge | Modulo arithmetic mixed bag (CRT/Euler) | LeetCode Discuss, search "number theory tricks" |

## 🔗 Further Reading

- [Art of Problem Solving – Number Theory Basics](https://artofproblemsolving.com/wiki/index.php/Number_theory)  
- [Brilliant.org – Number Theory (free preview lessons)](https://brilliant.org/courses/number-theory/)  
- Quantitative Aptitude by R.S. Aggarwal – Chapter 2

## 📌 Contributor To-Do List

- [ ] Add additional solved examples for base conversions.
- [ ] Compile shortcut sheet for divisibility up to 25.
- [ ] Curate 20-question timed drill with answer key.
- [ ] Link 2 high-quality video explainers.
