# Array Manipulation Track

>Status: 🟡 Draft — core patterns and reference material added; enhance with more company-tagged problems to reach 🟢.

Arrays show up in every coding round. This guide collects the highest leverage transformation patterns, reusable code snippets, and a curated drilling list so you can ramp fast.

## 🧭 Concept Map

| Pattern | When to Reach For It | Key Idea |
|---------|----------------------|----------|
| Prefix / suffix summaries | Range queries, balance checks, cumulative costs | Pre-compute aggregated information to answer queries in O(1) |
| Difference array / lazy addition | Batch updates over ranges | Store delta at boundaries, reconstruct when needed |
| Two pointers / partition | Sorted arrays, in-place filtering, Dutch flag | Move independent cursors to shrink search or reorder |
| Sweep-line on intervals | Meeting rooms, skyline, overlapping bookings | Sort events by boundary and maintain active count |
| Sparse vs dense techniques | Large index values with few updates | Use maps / coordinate compression to avoid huge arrays |

## 🛠️ Reusable Snippets

```python
def build_prefix(nums):
	prefix = [0]
	for val in nums:
		prefix.append(prefix[-1] + val)
	return prefix

def range_sum(prefix, L, R):
	return prefix[R + 1] - prefix[L]

def apply_range_updates(n, updates):
	diff = [0] * (n + 1)
	for start, end, delta in updates:
		diff[start] += delta
		if end + 1 < len(diff):
			diff[end + 1] -= delta
	arr = [0] * n
	running = 0
	for i in range(n):
		running += diff[i]
		arr[i] = running
	return arr
```

```cpp
// Rotate array right by k in-place using reversals
void rotate(vector<int>& nums, int k) {
	int n = nums.size();
	k %= n;
	auto rev = [&](int l, int r) {
		while (l < r) swap(nums[l++], nums[r--]);
	};
	rev(0, n - 1);
	rev(0, k - 1);
	rev(k, n - 1);
}
```

## � Implementation Playbook

1. **Clarify operations** — updates vs queries, order of magnitude of array length, constraints on values.
2. **Choose representation** — static array, vector, dictionary, Fenwick/segment tree if queries abound.
3. **Understand mutation cost** — prefer difference arrays for repeated range updates; use two pointers to avoid extra space.
4. **Optimise IO** — when handling millions of operations, use fast input/output and avoid per-element prints inside loops.

## 🗂️ Curated Problem Ladder

| Problem | Pattern | Difficulty | Notes |
|---------|---------|------------|-------|
| [LeetCode 238 – Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) | Prefix & suffix | Medium | Classic no-division prefix sweep |
| [LeetCode 560 – Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) | Prefix + hashmap | Medium | Counts subarrays via prefix frequency |
| [LeetCode 53 – Maximum Subarray](https://leetcode.com/problems/maximum-subarray/) | Kadane / prefix gain | Easy/Medium | Track best running sum |
| [LeetCode 370 – Range Addition](https://leetcode.com/problems/range-addition/) | Difference array | Medium | Demonstrates lazy range updates |
| [LeetCode 128 – Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/) | Sparse handling | Medium | Set-based O(n) solution |
| [LeetCode 986 – Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/) | Two pointers | Medium | Merge style scanning |
| [LeetCode 253 – Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) | Sweep line / heap | Medium | Equivalent to counting active intervals |
| [Codeforces 474B – Worms](https://codeforces.com/problemset/problem/474/B) | Prefix + binary search | Easy/Medium | Build prefix then lower_bound |
| [GFG – Sort an array of 0s, 1s and 2s](https://practice.geeksforgeeks.org/problems/sort-an-array-of-0s-1s-and-2s/0) | Dutch national flag | Easy | Three-way partition |
| [Hackerrank – Array Manipulation](https://www.hackerrank.com/challenges/crush/problem) | Difference array | Medium | Inspires diff-array template |

## 🧪 Practice Routine

- **Warm-up (15 min)**: One prefix/suffix problem + one two-pointer problem to keep pattern sharp.
- **Drill (30 min)**: Attempt a medium problem under interview timing; articulate trade-offs aloud.
- **Review (15 min)**: Document time/space complexity, edge cases hit/missed, and alternative solutions discovered.

## ✅ Checklist Before Submitting

- [ ] Handles empty / single-element arrays gracefully.
- [ ] Avoids integer overflow (use `long long` or `int64` when summing large ranges).
- [ ] Clears auxiliary structures (maps, heaps) between test cases on competitive sites.
- [ ] Includes assertive unit tests when writing standalone scripts.

## 📚 Further Reading

- *Competitive Programmer’s Handbook* — Chapter on prefix sums & difference arrays.
- [USACO Guide: Prefix Sums](https://usaco.guide/silver/prefix-sums) for step-by-step examples.
- [Topcoder Tutorial on Sweep Line](https://www.topcoder.com/thrive/articles/line-sweep-algorithms) to extend interval reasoning.
