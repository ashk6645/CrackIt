
# Bit Manipulation: Tricks, Patterns & Problem Solving

> Status: 🟢 Comprehensive — covers bitwise tricks, code, and classic problems.

---

## ⚡ Why Bit Manipulation?
Bit manipulation is a powerful technique for optimizing code, solving tricky problems, and working with sets, masks, and low-level data efficiently.

---

## 🧩 Core Patterns

- **Bitmasking**: Representing sets, toggling, and checking membership.
- **Bit Tricks**: LSB/MSB, counting set bits, isolating bits, swapping, etc.
- **XOR Properties**: Finding unique elements, toggling, parity checks.
- **Bit DP**: Dynamic programming with state compression (e.g., TSP, subset DP).
- **Gray Codes**: Generating sequences with single-bit changes.

---

## �️ Bit Manipulation Cheat Sheet

| Operation | Code (Python) | Description |
|-----------|--------------|-------------|
| Set $i$-th bit | `x |= (1 << i)` | Turns on bit $i$ |
| Clear $i$-th bit | `x &= ~(1 << i)` | Turns off bit $i$ |
| Toggle $i$-th bit | `x ^= (1 << i)` | Flips bit $i$ |
| Test $i$-th bit | `(x >> i) & 1` | Checks if bit $i$ is set |
| Count set bits | `bin(x).count('1')` or `ctz(x)` | Number of 1s |
| Isolate LSB | `x & -x` | Gets least significant 1 bit |
| Remove LSB | `x & (x-1)` | Clears least significant 1 bit |
| Power of 2? | `x > 0 and (x & (x-1)) == 0` | Checks if $x$ is power of 2 |
| XOR swap | `a ^= b; b ^= a; a ^= b` | Swaps $a$ and $b$ |

---

## 🔥 Classic Bit Manipulation Problems & Patterns

| Problem | Pattern | Key Trick | Tip |
|---------|---------|----------|-----|
| Subsets of Set | Bitmasking | Loop $0$ to $2^n-1$ | Each bit = include/exclude |
| Single Number | XOR | $a \oplus a = 0$ | XOR all elements |
| Counting Bits | Popcount | `x & (x-1)` | Remove LSB repeatedly |
| Reverse Bits | Bitwise | Shift & mask | Build from LSB to MSB |
| Power of Two | Bitwise | `x & (x-1)` | Only one bit set |
| Bitwise AND of Range | Bitwise | Common prefix | Shift until equal |

---

## 🧑‍� Code Templates

### 1. Generate All Subsets (Bitmask)
```python
def subsets(nums):
	n = len(nums)
	res = []
	for mask in range(1 << n):
		subset = [nums[i] for i in range(n) if (mask >> i) & 1]
		res.append(subset)
	return res
```

### 2. Count Set Bits (Brian Kernighan’s Algorithm)
```python
def count_bits(x):
	count = 0
	while x:
		x &= x - 1
		count += 1
	return count
```

### 3. Find Single Number (XOR)
```python
def single_number(nums):
	res = 0
	for num in nums:
		res ^= num
	return res
```

### 4. Check Power of Two
```python
def is_power_of_two(x):
	return x > 0 and (x & (x-1)) == 0
```

---

## 🏆 Problem Ladder (Practice Order)

1. Subsets (LeetCode 78)
2. Single Number (LeetCode 136)
3. Counting Bits (LeetCode 338)
4. Reverse Bits (LeetCode 190)
5. Bitwise AND of Numbers Range (LeetCode 201)
6. Power of Two (LeetCode 231)
7. Maximum Product of Word Lengths (LeetCode 318)
8. Total Hamming Distance (LeetCode 477)
9. Bitwise ORs of Subarrays (LeetCode 898)
10. Minimum Flips to Make OR Equal to 1 (LeetCode 1318)

---

## 📚 Further Resources

- [Bit Manipulation Patterns (NeetCode)](https://neetcode.io/roadmap)
- [Bitwise Operations (GeeksforGeeks)](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)
- [LeetCode Explore: Bit Manipulation](https://leetcode.com/explore/learn/card/bit-manipulation/)

---

> **Contributed by CrackIt Team — Last updated: September 2025**
