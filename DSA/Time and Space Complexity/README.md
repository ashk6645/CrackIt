# ⏱️ Time and Space Complexity Analysis

## What is Complexity Analysis?

Complexity analysis helps us understand how an algorithm's performance changes as the input size grows. It's like predicting how long a recipe will take based on the number of people you're cooking for.

## Why is it Important?

Imagine you have two algorithms that solve the same problem:
- **Algorithm A**: Takes 1 second for 100 items, 10 seconds for 1,000 items
- **Algorithm B**: Takes 2 seconds for 100 items, 4 seconds for 1,000 items

Which is better? Algorithm B! Even though it's slower for small inputs, it scales much better.

## Big O Notation

Big O notation describes the **worst-case** performance of an algorithm. It tells us how the algorithm behaves as input size approaches infinity.

### Common Big O Complexities (Best to Worst)

| Big O | Name | Example | Description |
|-------|------|---------|-------------|
| O(1) | Constant | Array access | Same time regardless of input size |
| O(log n) | Logarithmic | Binary search | Cuts problem in half each step |
| O(n) | Linear | Simple loop | Time grows proportionally with input |
| O(n log n) | Linearithmic | Merge sort | Efficient sorting algorithms |
| O(n²) | Quadratic | Nested loops | Time grows as square of input |
| O(n³) | Cubic | Triple nested loops | Very slow for large inputs |
| O(2ⁿ) | Exponential | Fibonacci recursion | Extremely slow, avoid if possible |
| O(n!) | Factorial | Traveling salesman | Practically unusable for n > 10 |

### Visual Representation

```
Time
 ↑
 |    
 |                                          O(n!)
 |                                    O(2ⁿ)
 |                          O(n³)
 |                   O(n²)
 |           O(n log n)
 |       O(n)
 |   O(log n)
 | O(1)
 |________________________→ Input Size (n)
```

## Time Complexity Examples

### O(1) - Constant Time
```python
def get_first_element(arr):
    return arr[0]  # Always one operation

def hash_lookup(dictionary, key):
    return dictionary[key]  # Direct access
```

### O(log n) - Logarithmic Time
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```

### O(n) - Linear Time
```python
def find_maximum(arr):
    max_val = arr[0]
    for num in arr:  # Visit each element once
        if num > max_val:
            max_val = num
    return max_val

def print_all_elements(arr):
    for element in arr:  # n operations for n elements
        print(element)
```

### O(n²) - Quadratic Time
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):           # Outer loop: n times
        for j in range(n-1):     # Inner loop: n times
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]

def print_all_pairs(arr):
    for i in arr:        # n times
        for j in arr:    # n times for each i
            print(i, j)  # Total: n × n = n² operations
```

## Space Complexity

Space complexity measures how much memory an algorithm uses relative to input size.

### Types of Space Usage

1. **Input Space**: Memory for storing input (doesn't count in space complexity)
2. **Auxiliary Space**: Extra memory used by algorithm (this is what we measure)
3. **Total Space**: Input space + Auxiliary space

### Space Complexity Examples

#### O(1) - Constant Space
```python
def find_sum(arr):
    total = 0           # One variable
    for num in arr:
        total += num    # No additional space used
    return total
```

#### O(n) - Linear Space
```python
def create_copy(arr):
    new_arr = []
    for num in arr:
        new_arr.append(num)  # Creating array of size n
    return new_arr

def fibonacci_dp(n):
    dp = [0] * (n + 1)  # Array of size n+1
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]
```

#### O(log n) - Logarithmic Space
```python
def binary_search_recursive(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)
    
    # Each recursive call uses stack space
    # Maximum depth is log n, so space is O(log n)
```

## How to Analyze Complexity

### Step-by-Step Process

1. **Identify the basic operations** (comparisons, arithmetic, assignments)
2. **Count how many times each operation executes**
3. **Express the count as a function of input size n**
4. **Find the dominant term** (highest order term)
5. **Drop constants and lower-order terms**

### Example Analysis

```python
def example_function(arr):
    n = len(arr)
    
    # Step 1: O(1) - constant time
    max_val = arr[0]
    
    # Step 2: O(n) - linear time
    for i in range(n):
        if arr[i] > max_val:
            max_val = arr[i]
    
    # Step 3: O(n²) - quadratic time
    for i in range(n):
        for j in range(n):
            print(arr[i] + arr[j])
    
    return max_val

# Total: O(1) + O(n) + O(n²) = O(n²)
# We keep the dominant term O(n²)
```

## Best, Average, and Worst Case

### Quick Sort Example

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    return quicksort(left) + middle + quicksort(right)
```

- **Best Case**: O(n log n) - Pivot divides array evenly
- **Average Case**: O(n log n) - Random pivot selection
- **Worst Case**: O(n²) - Pivot is always smallest/largest element

## Common Pitfalls and Tips

### ❌ Common Mistakes

1. **Counting inner operations separately**
   ```python
   # Wrong analysis: O(n) + O(n) = O(2n) = O(n)
   for i in range(n):
       for j in range(n):  # This is actually O(n²)
           print(i, j)
   ```

2. **Ignoring hidden complexities**
   ```python
   def process_strings(strings):
       for s in strings:           # O(n)
           s = s.upper()          # O(m) where m is string length
       # Total: O(n × m), not just O(n)
   ```

3. **Confusing space and time complexity**
   - Recursive algorithms often have different time and space complexities

### ✅ Best Practices

1. **Always consider the worst case** for Big O
2. **Look for nested loops** - usually indicates higher complexity
3. **Consider the input size** - what grows with the problem?
4. **Analyze recursive calls** - use recursion trees
5. **Account for library function complexities**

## Practical Examples

### Example 1: Two Sum Problem

```python
# Approach 1: Brute Force - O(n²) time, O(1) space
def two_sum_brute(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
    return []

# Approach 2: Hash Map - O(n) time, O(n) space
def two_sum_hash(nums, target):
    num_to_index = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_to_index:
            return [num_to_index[complement], i]
        num_to_index[num] = i
    return []
```

### Example 2: Finding Duplicates

```python
# Approach 1: Nested loops - O(n²) time, O(1) space
def has_duplicates_nested(arr):
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] == arr[j]:
                return True
    return False

# Approach 2: Sorting - O(n log n) time, O(1) space
def has_duplicates_sort(arr):
    arr.sort()
    for i in range(len(arr) - 1):
        if arr[i] == arr[i + 1]:
            return True
    return False

# Approach 3: Hash Set - O(n) time, O(n) space
def has_duplicates_set(arr):
    seen = set()
    for num in arr:
        if num in seen:
            return True
        seen.add(num)
    return False
```

## Practice Problems

### Problem 1: Array Sum
What's the time and space complexity?
```python
def array_sum(arr):
    total = 0
    for num in arr:
        total += num
    return total
```

<details>
<summary>Answer</summary>
Time: O(n) - we visit each element once
Space: O(1) - only using one variable
</details>

### Problem 2: Matrix Multiplication
```python
def matrix_multiply(A, B):
    n = len(A)
    C = [[0] * n for _ in range(n)]
    
    for i in range(n):
        for j in range(n):
            for k in range(n):
                C[i][j] += A[i][k] * B[k][j]
    
    return C
```

<details>
<summary>Answer</summary>
Time: O(n³) - three nested loops
Space: O(n²) - creating n×n result matrix
</details>

### Problem 3: Fibonacci Sequence
Compare these approaches:

```python
# Recursive
def fib_recursive(n):
    if n <= 1:
        return n
    return fib_recursive(n-1) + fib_recursive(n-2)

# Dynamic Programming
def fib_dp(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

# Optimized DP
def fib_optimized(n):
    if n <= 1:
        return n
    prev, curr = 0, 1
    for i in range(2, n + 1):
        prev, curr = curr, prev + curr
    return curr
```

<details>
<summary>Answer</summary>
1. Recursive: Time O(2ⁿ), Space O(n)
2. DP: Time O(n), Space O(n)
3. Optimized: Time O(n), Space O(1)
</details>

## Summary

### Key Takeaways

1. **Big O describes worst-case performance** as input size grows
2. **Focus on dominant terms** - drop constants and lower-order terms
3. **Consider both time and space** complexity
4. **Trade-offs exist** - sometimes better time complexity requires more space
5. **Context matters** - O(n²) might be fine for small, fixed inputs

### Common Complexities to Remember

- **O(1)**: Array access, hash table operations
- **O(log n)**: Binary search, balanced tree operations
- **O(n)**: Linear search, single pass through array
- **O(n log n)**: Efficient sorting (merge sort, heap sort)
- **O(n²)**: Nested loops, bubble sort
- **O(2ⁿ)**: Recursive solutions with overlapping subproblems

### Next Steps

Now that you understand how to analyze algorithms, you're ready to learn about specific data structures! Each data structure has different complexity characteristics for different operations.

**Next Topic**: [Arrays - The Foundation Data Structure](../03-Arrays/)

---

**Practice Tip**: Whenever you write code, ask yourself: "What's the time and space complexity?" This habit will make you a better programmer! 🚀
