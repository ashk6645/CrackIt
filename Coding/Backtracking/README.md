
# Backtracking: Mastering Recursive Search & Pruning

> Status: 🟢 Comprehensive — covers recursion, pruning, and classic backtracking problems.

---

## 🚩 What is Backtracking?
Backtracking is a general algorithmic technique for solving problems recursively by building a solution incrementally, one piece at a time, and removing those solutions that fail to satisfy the constraints of the problem at any point (pruning).

---

## 🧩 Core Patterns

- **Subsets/Combinations**: Explore all possible selections (e.g., Subsets, Combination Sum).
- **Permutations**: Explore all possible orderings (e.g., Permute, N-Queens).
- **Constraint Satisfaction**: Fill a structure under rules (e.g., Sudoku, N-Queens).
- **Decision Trees**: Try all choices at each step, backtrack on failure.

---

## 🛠️ Backtracking Template

```python
def backtrack(path, options):
	if is_solution(path):
		results.append(path[:])
		return
	for option in options:
		if is_valid(option, path):  # Prune invalid choices
			path.append(option)
			backtrack(path, next_options(option, path))
			path.pop()  # Undo choice
```

---

## ✂️ Pruning Techniques

- **Early Termination**: Stop exploring a path as soon as constraints are violated.
- **Sorting/Input Preprocessing**: Enables skipping duplicates or early stopping.
- **State Memoization**: Cache visited states to avoid recomputation (hybrid with DP).
- **Bounding**: Use problem-specific bounds to cut off branches (e.g., sum > target).

---

## 🔥 Classic Backtracking Problems & Patterns

| Problem | Pattern | Pruning | Key Insight |
|---------|---------|---------|-------------|
| Subsets | Subset | None | Explore include/exclude |
| Permutations | Permutation | Used set/visited | Track used elements |
| N-Queens | Constraint | Row/col/diag sets | Place queen row by row |
| Sudoku Solver | Constraint | Validity check | Fill empty cells recursively |
| Combination Sum | Combination | Early stop if sum > target | Sort input |
| Word Search | Path Search | Mark visited | Backtrack on dead end |

---

## 🧑‍� Code Templates

### 1. Subsets (All Possible Subsets)
```python
def subsets(nums):
	res = []
	def dfs(i, path):
		res.append(path[:])
		for j in range(i, len(nums)):
			dfs(j+1, path + [nums[j]])
	dfs(0, [])
	return res
```

### 2. Permutations
```python
def permute(nums):
	res = []
	def dfs(path, used):
		if len(path) == len(nums):
			res.append(path[:])
			return
		for i in range(len(nums)):
			if not used[i]:
				used[i] = True
				dfs(path + [nums[i]], used)
				used[i] = False
	dfs([], [False]*len(nums))
	return res
```

### 3. N-Queens
```python
def solveNQueens(n):
	res = []
	board = [['.']*n for _ in range(n)]
	cols = set(); diag1 = set(); diag2 = set()
	def dfs(r):
		if r == n:
			res.append([''.join(row) for row in board])
			return
		for c in range(n):
			if c in cols or (r+c) in diag1 or (r-c) in diag2:
				continue
			board[r][c] = 'Q'
			cols.add(c); diag1.add(r+c); diag2.add(r-c)
			dfs(r+1)
			board[r][c] = '.'
			cols.remove(c); diag1.remove(r+c); diag2.remove(r-c)
	dfs(0)
	return res
```

---

## 🧠 Tips & Best Practices

- Always undo your choice (backtrack) after the recursive call.
- Use sets/arrays to track used elements or constraints.
- Prune as early as possible for efficiency.
- For combinations, avoid revisiting previous elements by passing an index.
- For permutations, use a visited array or swap in-place.

---

## 🏆 Problem Ladder (Practice Order)

1. Subsets (LeetCode 78)
2. Permutations (LeetCode 46)
3. Combination Sum (LeetCode 39)
4. N-Queens (LeetCode 51)
5. Sudoku Solver (LeetCode 37)
6. Word Search (LeetCode 79)
7. Palindrome Partitioning (LeetCode 131)
8. Restore IP Addresses (LeetCode 93)
9. Letter Combinations of a Phone Number (LeetCode 17)
10. Generate Parentheses (LeetCode 22)

---

## 📚 Further Resources

- [Backtracking Patterns (NeetCode)](https://neetcode.io/roadmap)
- [Backtracking Visualizations (VisuAlgo)](https://visualgo.net/en/recursion)
- [LeetCode Explore: Backtracking](https://leetcode.com/explore/learn/card/recursion-ii/)

---

> **Contributed by CrackIt Team — Last updated: September 2025**
