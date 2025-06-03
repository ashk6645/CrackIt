# 📊 Arrays - The Foundation Data Structure

## What is an Array?

An array is a collection of elements stored in contiguous memory locations. Think of it as a row of numbered boxes, where each box can hold one item, and you can access any box directly using its number (index).

```
Index:  0    1    2    3    4
Array: [10] [20] [30] [40] [50]
         ↑   ↑    ↑     ↑     ↑
      Box 0 Box 1 Box 2 Box 3 Box 4
```
````markdown
Arrays are used to store multiple values in a single variable instead of declaring separate variables.

````

## Memory Layout

Arrays store elements in consecutive memory addresses:

```
Memory Address: 1000  1004  1008  1012  1016
Array Values:   [10]  [20]  [30]  [40]  [50]
Index:           0     1     2     3     4
```

This contiguous storage enables **O(1) random access** - you can jump to any element instantly!

## ⚙️ Characteristics:

| Feature               | Description                                                                                                    |
| --------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Homogeneous**       | Stores elements of the **same data type**.                                                                     |
| **Fixed Size**        | Size is **defined at creation** and cannot be changed.                                                         |
| **Indexed Access**    | Provides **fast (O(1))** access to elements via index.                                                         |
| **Memory Efficient**  | Stored **contiguously**, helping with **CPU caching** and performance.                                         |
| **Resizing Overhead** | Cannot be resized; for dynamic sizing, use `ArrayList` which internally **doubles** when capacity is exceeded. |
| **Reusability**       | Arrays can be **passed to methods** and **returned** from methods.                                             |
| **Space Efficient**   | Efficient for storing a known number of values.                                                                |


## Array Operations and Complexities

| Operation | Time Complexity | Space Complexity | Description |
|-----------|----------------|------------------|-------------|
| Access | O(1) | O(1) | Get element by index |
| Search | O(n) | O(1) | Find element value |
| Insertion | O(n) | O(1) | Insert at specific position |
| Deletion | O(n) | O(1) | Remove from specific position |
| Append | O(1) | O(1) | Add to end (if space available) |

## Basic Array Implementation

### Python Arrays (Lists)
```python
# Creating arrays
arr = [1, 2, 3, 4, 5]           # Initialize with values
empty_arr = []                   # Empty array
sized_arr = [0] * 10            # Array of size 10 with zeros

# Basic operations
print(arr[0])                   # Access: O(1)
arr[2] = 100                    # Update: O(1)
arr.append(6)                   # Append: O(1) amortized
arr.insert(0, -1)               # Insert at beginning: O(n)
arr.remove(100)                 # Remove by value: O(n)
arr.pop()                       # Remove last: O(1)
arr.pop(0)                      # Remove first: O(n)
```

### Java Arrays
```java
// Static array
int[] arr = new int[5];         // Fixed size
int[] arr2 = {1, 2, 3, 4, 5};  // Initialize with values

// Dynamic array (ArrayList)
ArrayList<Integer> list = new ArrayList<>();
list.add(10);                   // Append
list.get(0);                    // Access
list.set(0, 20);               // Update
list.remove(0);                 // Remove by index
```

### C++ Arrays
```cpp
// Static array
int arr[5] = {1, 2, 3, 4, 5};

// Dynamic array (vector)
vector<int> vec = {1, 2, 3, 4, 5};
vec.push_back(6);               // Append
vec[0] = 10;                    // Access/Update
vec.erase(vec.begin());         // Remove first element
```

## Common Array Patterns

### 1. Two Pointers Technique

Used for: Pair problems, palindrome checking, array reversal

```python
def reverse_array(arr):
    left, right = 0, len(arr) - 1
    
    while left < right:
        # Swap elements
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    
    return arr

def two_sum_sorted(arr, target):
    """Find two numbers that sum to target in sorted array"""
    left, right = 0, len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return []
```

### 2. Sliding Window Technique

Used for: Subarray problems, string problems

```python
def max_sum_subarray(arr, k):
    """Find maximum sum of k consecutive elements"""
    if len(arr) < k:
        return -1
    
    # Calculate sum of first window
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Slide the window
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i - k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum

def longest_substring_with_k_distinct(s, k):
    """Find longest substring with at most k distinct characters"""
    if k == 0:
        return 0
    
    char_count = {}
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Expand window
        char_count[s[right]] = char_count.get(s[right], 0) + 1
        
        # Contract window if needed
        while len(char_count) > k:
            char_count[s[left]] -= 1
            if char_count[s[left]] == 0:
                del char_count[s[left]]
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

### 3. Prefix Sum Technique

Used for: Range sum queries, subarray sum problems

```python
def build_prefix_sum(arr):
    """Build prefix sum array for O(1) range queries"""
    prefix = [0] * (len(arr) + 1)
    
    for i in range(len(arr)):
        prefix[i + 1] = prefix[i] + arr[i]
    
    return prefix

def range_sum(prefix, left, right):
    """Get sum of elements from index left to right (inclusive)"""
    return prefix[right + 1] - prefix[left]

def subarray_sum_equals_k(arr, k):
    """Count subarrays with sum equal to k"""
    count = 0
    prefix_sum = 0
    sum_count = {0: 1}  # Handle subarrays starting from index 0
    
    for num in arr:
        prefix_sum += num
        
        # Check if (prefix_sum - k) exists
        if (prefix_sum - k) in sum_count:
            count += sum_count[prefix_sum - k]
        
        # Add current prefix sum to map
        sum_count[prefix_sum] = sum_count.get(prefix_sum, 0) + 1
    
    return count
```

### 4. Kadane's Algorithm (Maximum Subarray Sum)

```python
def max_subarray_sum(arr):
    """Find maximum sum of contiguous subarray"""
    max_sum = float('-inf')
    current_sum = 0
    
    for num in arr:
        current_sum = max(num, current_sum + num)
        max_sum = max(max_sum, current_sum)
    
    return max_sum

def max_subarray_with_indices(arr):
    """Return max sum and the subarray indices"""
    max_sum = float('-inf')
    current_sum = 0
    start = 0
    end = 0
    temp_start = 0
    
    for i, num in enumerate(arr):
        current_sum += num
        
        if current_sum > max_sum:
            max_sum = current_sum
            start = temp_start
            end = i
        
        if current_sum < 0:
            current_sum = 0
            temp_start = i + 1
    
    return max_sum, start, end
```

## Advanced Array Techniques

### 1. Dutch National Flag Algorithm (3-Way Partitioning)

```python
def sort_colors(nums):
    """Sort array of 0s, 1s, and 2s in-place"""
    low = mid = 0
    high = len(nums) - 1
    
    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:  # nums[mid] == 2
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1
            # Don't increment mid here!
    
    return nums
```

### 2. Cycle Detection (Floyd's Algorithm)

```python
def find_duplicate(nums):
    """Find duplicate in array where numbers are 1 to n"""
    # Phase 1: Find intersection point
    slow = fast = nums[0]
    
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break
    
    # Phase 2: Find entrance to cycle
    slow = nums[0]
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]
    
    return slow
```

### 3. Next Greater Element

```python
def next_greater_elements(nums):
    """Find next greater element for each element"""
    n = len(nums)
    result = [-1] * n
    stack = []
    
    # Process array twice to handle circular nature
    for i in range(2 * n):
        while stack and nums[stack[-1]] < nums[i % n]:
            result[stack.pop()] = nums[i % n]
        
        if i < n:  # Only push indices in first pass
            stack.append(i)
    
    return result
```

## Array Sorting Algorithms

### 1. Bubble Sort - O(n²)
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        if not swapped:  # Optimization: already sorted
            break
    
    return arr
```

### 2. Selection Sort - O(n²)
```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    
    return arr
```

### 3. Insertion Sort - O(n²)
```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        
        arr[j + 1] = key
    
    return arr
```

### 4. Quick Sort - O(n log n) average, O(n²) worst
```python
def quick_sort(arr, low=0, high=None):
    if high is None:
        high = len(arr) - 1
    
    if low < high:
        pivot_idx = partition(arr, low, high)
        quick_sort(arr, low, pivot_idx - 1)
        quick_sort(arr, pivot_idx + 1, high)
    
    return arr

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

### 5. Merge Sort - O(n log n)
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

## Array Searching Algorithms

### 1. Linear Search - O(n)
```python
def linear_search(arr, target):
    for i, value in enumerate(arr):
        if value == target:
            return i
    return -1
```

### 2. Binary Search - O(log n)
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
```

### 3. Binary Search Variants

```python
def find_first_occurrence(arr, target):
    """Find first occurrence of target in sorted array"""
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            result = mid
            right = mid - 1  # Continue searching left
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

def find_last_occurrence(arr, target):
    """Find last occurrence of target in sorted array"""
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            result = mid
            left = mid + 1  # Continue searching right
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

def search_in_rotated_array(arr, target):
    """Search in rotated sorted array"""
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        
        # Check which half is sorted
        if arr[left] <= arr[mid]:  # Left half is sorted
            if arr[left] <= target < arr[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:  # Right half is sorted
            if arr[mid] < target <= arr[right]:
                left = mid + 1
            else:
                right = mid - 1
    
    return -1
```

## Practice Problems

### 🟢 Easy Problems

1. **Two Sum**: Find two numbers that add up to target
2. **Remove Duplicates**: Remove duplicates from sorted array
3. **Maximum Element**: Find the largest element
4. **Reverse Array**: Reverse array in-place
5. **Rotate Array**: Rotate array by k positions

### 🟡 Medium Problems

6. **3Sum**: Find all triplets that sum to zero
7. **Container With Most Water**: Find max water area
8. **Product of Array Except Self**: Calculate products
9. **Spiral Matrix**: Traverse matrix in spiral order
10. **Merge Intervals**: Merge overlapping intervals

### 🔴 Hard Problems

11. **Median of Two Sorted Arrays**: Find median efficiently
12. **Trapping Rain Water**: Calculate trapped water
13. **Sliding Window Maximum**: Maximum in each window
14. **Minimum Window Substring**: Smallest window containing all chars
15. **Array Median**: Find median without sorting

## Problem Solutions

### Two Sum (Easy)
```python
def two_sum(nums, target):
    """Find indices of two numbers that add up to target"""
    num_to_index = {}
    
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_to_index:
            return [num_to_index[complement], i]
        num_to_index[num] = i
    
    return []

# Time: O(n), Space: O(n)
```

### Container With Most Water (Medium)
```python
def max_area(height):
    """Find maximum water area between two lines"""
    left, right = 0, len(height) - 1
    max_water = 0
    
    while left < right:
        width = right - left
        current_height = min(height[left], height[right])
        max_water = max(max_water, width * current_height)
        
        # Move pointer with smaller height
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    
    return max_water

# Time: O(n), Space: O(1)
```

### Trapping Rain Water (Hard)
```python
def trap(height):
    """Calculate total trapped rainwater"""
    if not height:
        return 0
    
    left, right = 0, len(height) - 1
    left_max = right_max = 0
    water = 0
    
    while left < right:
        if height[left] < height[right]:
            if height[left] >= left_max:
                left_max = height[left]
            else:
                water += left_max - height[left]
            left += 1
        else:
            if height[right] >= right_max:
                right_max = height[right]
            else:
                water += right_max - height[right]
            right -= 1
    
    return water

# Time: O(n), Space: O(1)
```

## Tips and Best Practices

### ✅ Do's

1. **Check array bounds** before accessing elements
2. **Handle edge cases**: empty arrays, single elements
3. **Use appropriate data structures** for the problem
4. **Consider time-space tradeoffs**
5. **Write clean, readable code** with meaningful variable names

### ❌ Don'ts

1. **Don't assume array is sorted** unless specified
2. **Don't modify input** unless allowed
3. **Don't use extra space** if in-place solution exists
4. **Don't forget integer overflow** in languages like Java/C++
5. **Don't use nested loops** if linear solution exists

### Common Optimizations

1. **Early termination**: Break loops when answer is found
2. **Two pointers**: Reduce O(n²) to O(n) for sorted arrays
3. **Hash maps**: Trade space for time in lookup operations
4. **Prefix/suffix arrays**: Precompute for range queries
5. **Sorting**: Sometimes O(n log n) sort + O(n) is better than O(n²)

## Array vs Other Data Structures

| Feature | Array | Linked List | Hash Table |
|---------|-------|-------------|------------|
| Access | O(1) | O(n) | O(1) average |
| Search | O(n) | O(n) | O(1) average |
| Insertion | O(n) | O(1) | O(1) average |
| Deletion | O(n) | O(1) | O(1) average |
| Memory | Contiguous | Scattered | Scattered |
| Cache | Excellent | Poor | Good |

## Summary

### Key Points

1. **Arrays provide O(1) random access** due to contiguous memory
2. **Insertion/deletion is expensive** except at the end
3. **Many problems have O(n) solutions** using clever techniques
4. **Two pointers and sliding window** are powerful patterns
5. **Binary search works on sorted arrays** in O(log n) time

### When to Use Arrays

- **Need random access** to elements
- **Memory efficiency** is important
- **Cache performance** matters
- **Simple iteration** patterns
- **Mathematical operations** on sequences

### When to Avoid Arrays

- **Frequent insertions/deletions** in middle
- **Unknown/highly variable size**
- **Need efficient search** without sorting
- **Complex relationships** between elements

**Next Topic**: [Strings - Text Processing and Manipulation](https://github.com/ashk6645/CrackIt/tree/main/DSA/4.%20Strings)

---

**Practice Recommendation**: Solve at least 5 easy and 3 medium array problems before moving to the next topic. Arrays are fundamental to understanding more complex data structures! 🚀
