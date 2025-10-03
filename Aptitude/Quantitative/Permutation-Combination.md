# Permutation & Combination

>Status: 🟢 Complete — comprehensive guide with counting principles, circular arrangements, derangements, and drills.

## 🚀 Quick Overview

Permutation & Combination (P&C) provides systematic tools to count arrangements and selections without exhaustive listing. These problems often feed directly into probability and data interpretation sets.

---

## � Core Concepts

| Concept | Meaning |
|---------|---------|
| Fundamental Principle | If a task can be done in m ways and another in n ways → total m·n ways |
| Permutation | Ordered arrangement |
| Combination | Unordered selection |
| Circular Permutation | Arrangement around a circle (rotations same) |
| Derangement | Permutation with no element in original position |

---

## 🧮 Formula Sheet

| Scenario | Formula | Notes |
|----------|---------|-------|
| Permutations (n distinct, r taken) | $^{n}P_r = \frac{n!}{(n-r)!}$ | Order matters |
| Combinations (n distinct, r chosen) | $^{n}C_r = \frac{n!}{r!(n-r)!}$ | Order not matter |
| Relation | $^{n}P_r = ^{n}C_r \cdot r!$ | Convert between forms |
| Circular permutation (distinct) | $(n-1)!$ | Rotation equivalence |
| Circular with reflection same (necklace) | $(n-1)!/2$ | Flip symmetry |
| Identical object distribution (stars & bars) | $^{n+k-1}C_{k-1}$ | Distribute n identical into k boxes (allow 0) |
| Non‑empty distribution | $^{n-1}C_{k-1}$ | Each box ≥1 |
| Derangements $!n$ | $!n = n! \sum_{k=0}^{n} \frac{(-1)^k}{k!}$ | Approx: $!n \approx \frac{n!}{e}$ |
| Repetition combinations | $^{n+r-1}C_r$ | Multiset selection |

---

## 🧠 Patterns & Techniques

- Break constraints early (e.g., seat fixed person → reduce circular freedom)
- Use complement counting for “at least one” restrictions
- For identical items: convert to partition / stars & bars
- For adjacency restrictions: place mandatory separators first
- For derangements: apply inclusion–exclusion

---

## 🧑‍💻 Solved Examples

### 1. Basic Permutation
How many 4-letter words (no meaning needed) from A,B,C,D,E without repetition?
Answer: $^{5}P_4 = 5·4·3·2 = 120$

### 2. Combination Selection
From 10 candidates choose a 4-member committee.
Answer: $^{10}C_4 = 210$

### 3. Circular Arrangement
Number of ways to seat 6 distinct people around a round table.
Answer: $(6-1)! = 120$

### 4. Circular with Restriction
Seat 5 people (A must sit to left of B) around circular table.
- Total circular = $(5-1)! = 24$
- A relative to B: exactly half satisfy “A left of B” ⇒ 24/2 = 12

### 5. Distribution (Stars & Bars)
Distribute 7 identical balls into 3 boxes (allow empty).
Ways = $^{7+3-1}C_{3-1} = ^{9}C_2 = 36$

### 6. Non-empty Distribution
Distribute 7 identical balls into 3 non‑empty boxes.
Transform: give each box 1 → remaining 4 free ⇒ $^{4+3-1}C_{2} = ^{6}C_2 = 15$

### 7. Derangement
Number of ways to permute 4 letters so none in original place.
Exact: $!4 = 4!(1 - 1/1! + 1/2! - 1/3! + 1/4!) = 24(1 -1 +1/2 -1/6 +1/24)=24(0 +0.5 -0.1667 +0.0417)=24×0.375=9$

### 8. At Least One Condition
Number of 4-digit numbers formed from digits 1–7 (no repetition) that contain digit 5.
- Total 4-digit (no leading 0 issue): $^{7}P_4 = 840$
- Exclude without 5: choose 4 from remaining 6 and permute: $^{6}P_4 = 360$
- Required = 840 - 360 = 480

### 9. Repetition Allowed
Number of 3-letter strings over {A,B,C} with repetition.
Answer: $3^3 = 27$

### 10. Arrangement With Identical Letters
Number of distinct permutations of “BALLOON”.
Count letters: B(1) A(1) L(2) O(2) N(1) ⇒ $\frac{7!}{2!2!} = 1260$

---

## 📝 Practice Drill (15 Questions)

1. Evaluate $^{8}P_3$.
2. Compute $^{9}C_5$.
3. Ways to arrange 8 people in a row if two specific people must be together.
4. Ways to arrange letters of “MISSISSIPPI”.
5. Seat 7 people around circular table if two must not sit together.
6. Distribute 10 identical chocolates among 4 kids (allow empty).
7. Distribute 10 identical chocolates so each gets at least 1.
8. Number of 5-digit numbers from digits 1–9 without repetition.
9. Count derangements of 5 objects (exact value).
10. Form 4-digit even numbers from digits {1,2,3,4,5,6} without repetition.
11. Choose a team of 3 boys and 2 girls from 5 boys & 4 girls.
12. Number of solutions to x1 + x2 + x3 = 12 (xi ≥ 0, integer).
13. Number of solutions to x1 + x2 + x3 = 12 (xi ≥ 1, integer).
14. Arrange letters of “ACCOUNT” so vowels together.
15. From 6 men & 4 women choose a committee of 4 with ≥1 woman.

---

## 📚 Additional Resources

- [Permutation & Combination (Khan Academy)](https://www.khanacademy.org/math/statistics-probability/probability-library)
- [Derangements Explanation (Brilliant)](https://brilliant.org/wiki/derangements/)
- [Stars & Bars Method](https://brilliant.org/wiki/combinations-with-repetition/)

---

## 🎯 Answer Key

1. 336  2. 126  3. Treat block: 7!×2 = 10080  4. 34650  5. Total (6! = 720) - together (5!×2 = 240) = 480  6. ^{13}C_3 = 286  7. ^{9}C_3 = 84  8. ^{9}P_5 = 15120  9. !5 = 44  10. Choose last even {2,4,6}: 3 choices; arrange remaining 3 from other 5: ^5P3 = 60 ⇒ 180  11. ^5C3 × ^4C2 = 10×6=60  12. ^{12+3-1}C_{3-1} = ^{14}C_2 = 91  13. After 1 each: ^{9}C_2 = 36  14. Word: A,O,U vowels together block + consonants C,C,C,N,T (treat C’s identical): arrange block + 5 = 6!/3! = 120  15. Total ^{10}C_4 = 210 minus all-men ^6C4 = 15 ⇒ 195

---

>**Last Updated**: October 2025 | **Contributor**: CrackIt Team
