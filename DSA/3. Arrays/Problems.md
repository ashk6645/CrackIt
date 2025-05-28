# 📝 Array Problems - Practice Set

## Problem Categories

### 🟢 Easy Problems (5 problems)
### 🟡 Medium Problems (5 problems)  
### 🔴 Hard Problems (5 problems)

---

## 🟢 Easy Problems

### Problem 1: Two Sum
**Difficulty**: Easy  
**Pattern**: Hash Map, Two Pointers

**Problem**: Given an array of integers `nums` and an integer `target`, return indices of two numbers that add up to `target`.

**Example**:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9
```

**Constraints**:
- 2 ≤ nums.length ≤ 10⁴
- Each input has exactly one solution
- Cannot use same element twice

<details>
<summary>💡 Hint</summary>
Use a hash map to store complements. For each number, check if its complement exists.
</details>

<details>
<summary>✅ Solution</summary>

```python
def two_sum(nums, target):
    num_to_index = {}
    
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_to_index:
            return [num_to_index[complement], i]
        num_to_index[num] = i
    
    return []

# Time: O(n), Space: O(n)
```
</details>

---

### Problem 2: Remove Duplicates from Sorted Array
**Difficulty**: Easy  
**Pattern**: Two Pointers

**Problem**: Remove duplicates from sorted array in-place and return new length.

**Example**:
```
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
```

**Constraints**:
- 1 ≤ nums.length ≤ 3 × 10⁴
- Array is sorted in non-decreasing order

<details>
<summary>💡 Hint</summary>
Use two pointers: one for iteration, one for placing unique elements.
</details>

<details>
<summary>✅ Solution</summary>

```python
def remove_duplicates(nums):
    if not nums:
        return 0
    
    write_index = 1
    
    for read_index in range(1, len(nums)):
        if nums[read_index] != nums[read_index - 1]:
            nums[write_index] = nums[read_index]
            write_index += 1
    
    return write_index

# Time: O(n), Space: O(1)
```
</details>

---

### Problem 3: Maximum Subarray (Kadane's Algorithm)
**Difficulty**: Easy  
**Pattern**: Dynamic Programming

**Problem**: Find the contiguous subarray with the largest sum.

**Example**:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6
```

**Constraints**:
- 1 ≤ nums.length ≤ 10⁵
- -10⁴ ≤ nums[i] ≤ 10⁴

<details>
<summary>💡 Hint</summary>
At each position, decide whether to extend existing subarray or start new one.
</details>

<details>
<summary>✅ Solution</summary>

```python
def max_subarray(nums):
    max_sum = float('-inf')
    current_sum = 0
    
    for num in nums:
        current_sum = max(num, current_sum + num)
        max_sum = max(max_sum, current_sum)
    
    return max_sum

# Time: O(n), Space: O(1)
```
</details>

---

### Problem 4: Rotate Array
**Difficulty**: Easy  
**Pattern**: Array Manipulation

**Problem**: Rotate array to the right by k steps.

**Example**:
```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
```

**Constraints**:
- 1 ≤ nums.length ≤ 10⁵
- k ≥ 0

<details>
<summary>💡 Hint</summary>
Reverse the entire array, then reverse first k and last n-k elements.
</details>

<details>
<summary>✅ Solution</summary>

```python
def rotate(nums, k):
    n = len(nums)
    k = k % n  # Handle k > n
    
    def reverse(start, end):
        while start < end:
            nums[start], nums[end] = nums[end], nums[start]
            start += 1
            end -= 1
    
    # Reverse entire array
    reverse(0, n - 1)
    # Reverse first k elements
    reverse(0, k - 1)
    # Reverse remaining elements
    reverse(k, n - 1)

# Time: O(n), Space: O(1)
```
</details>

---

### Problem 5: Best Time to Buy and Sell Stock
**Difficulty**: Easy  
**Pattern**: Greedy, One Pass

**Problem**: Find maximum profit from buying and selling stock once.

**Example**:
```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6)
```

**Constraints**:
- 1 ≤ prices.length ≤ 10⁵
- 0 ≤ prices[i] ≤ 10⁴

<details>
<summary>💡 Hint</summary>
Track minimum price seen so far and maximum profit at each step.
</details>

<details>
<summary>✅ Solution</summary>

```python
def max_profit(prices):
    min_price = float('inf')
    max_profit = 0
    
    for price in prices:
        if price < min_price:
            min_price = price
        elif price - min_price > max_profit:
            max_profit = price - min_price
    
    return max_profit

# Time: O(n), Space: O(1)
```
</details>

---

## 🟡 Medium Problems

### Problem 6: 3Sum
**Difficulty**: Medium  
**Pattern**: Two Pointers, Sorting

**Problem**: Find all unique triplets that sum to zero.

**Example**:
```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

**Constraints**:
- 3 ≤ nums.length ≤ 3000
- Solution set must not contain duplicate triplets

<details>
<summary>💡 Hint</summary>
Sort array first, then use two pointers for each fixed element.
</details>

<details>
<summary>✅ Solution</summary>

```python
def three_sum(nums):
    nums.sort()
    result = []
    n = len(nums)
    
    for i in range(n - 2):
        # Skip duplicates for first element
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        
        left, right = i + 1, n - 1
        
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            
            if total == 0:
                result.append([nums[i], nums[left], nums[right]])
                
                # Skip duplicates
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                
                left += 1
                right -= 1
            elif total < 0:
                left += 1
            else:
                right -= 1
    
    return result

# Time: O(n²), Space: O(1)
```
</details>

---

### Problem 7: Container With Most Water
**Difficulty**: Medium  
**Pattern**: Two Pointers

**Problem**: Find maximum area that can be formed by two lines and x-axis.

**Example**:
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: Lines at index 1 and 8 form container with area 49
```

**Constraints**:
- n == height.length
- 2 ≤ n ≤ 10⁵
- 0 ≤ height[i] ≤ 10⁴

<details>
<summary>💡 Hint</summary>
Use two pointers from ends. Move pointer with smaller height inward.
</details>

<details>
<summary>✅ Solution</summary>

```python
def max_area(height):
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
</details>

---

### Problem 8: Product of Array Except Self
**Difficulty**: Medium  
**Pattern**: Prefix/Suffix Arrays

**Problem**: Return array where each element is product of all elements except itself.

**Example**:
```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

**Constraints**:
- 2 ≤ nums.length ≤ 10⁵
- Cannot use division operator
- Follow-up: O(1) extra space

<details>
<summary>💡 Hint</summary>
Calculate prefix products, then multiply with suffix products in second pass.
</details>

<details>
<summary>✅ Solution</summary>

```python
def product_except_self(nums):
    n = len(nums)
    result = [1] * n
    
    # Forward pass: store prefix products
    for i in range(1, n):
        result[i] = result[i - 1] * nums[i - 1]
    
    # Backward pass: multiply with suffix products
    suffix_product = 1
    for i in range(n - 1, -1, -1):
        result[i] *= suffix_product
        suffix_product *= nums[i]
    
    return result

# Time: O(n), Space: O(1) extra
```
</details>

---

### Problem 9: Find Minimum in Rotated Sorted Array
**Difficulty**: Medium  
**Pattern**: Binary Search

**Problem**: Find minimum element in rotated sorted array.

**Example**:
```
Input: nums = [3,4,5,1,2]
Output: 1
```

**Constraints**:
- n == nums.length
- 1 ≤ n ≤ 5000
- All integers are unique

<details>
<summary>💡 Hint</summary>
Use binary search. Compare middle element with right element to determine which half to search.
</details>

<details>
<summary>✅ Solution</summary>

```python
def find_min(nums):
    left, right = 0, len(nums) - 1
    
    while left < right:
        mid = (left + right) // 2
        
        if nums[mid] > nums[right]:
            # Minimum is in right half
            left = mid + 1
        else:
            # Minimum is in left half (including mid)
            right = mid
    
    return nums[left]

# Time: O(log n), Space: O(1)
```
</details>

---

### Problem 10: Subarray Sum Equals K
**Difficulty**: Medium  
**Pattern**: Prefix Sum, Hash Map

**Problem**: Count number of subarrays with sum equal to k.

**Example**:
```
Input: nums = [1,1,1], k = 2
Output: 2
```

**Constraints**:
- 1 ≤ nums.length ≤ 2 × 10⁴
- -1000 ≤ nums[i] ≤ 1000
- -10⁷ ≤ k ≤ 10⁷

<details>
<summary>💡 Hint</summary>
Use prefix sum and hash map. For each prefix sum, check if (sum - k) exists.
</details>

<details>
<summary>✅ Solution</summary>

```python
def subarray_sum(nums, k):
    count = 0
    prefix_sum = 0
    sum_count = {0: 1}  # Handle subarrays from beginning
    
    for num in nums:
        prefix_sum += num
        
        # Check if (prefix_sum - k) exists
        if (prefix_sum - k) in sum_count:
            count += sum_count[prefix_sum - k]
        
        # Add current prefix sum
        sum_count[prefix_sum] = sum_count.get(prefix_sum, 0) + 1
    
    return count

# Time: O(n), Space: O(n)
```
</details>

---

## 🔴 Hard Problems

### Problem 11: Trapping Rain Water
**Difficulty**: Hard  
**Pattern**: Two Pointers, Stack

**Problem**: Calculate how much rain water can be trapped.

**Example**:
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

**Constraints**:
- n == height.length
- 1 ≤ n ≤ 2 × 10⁴
- 0 ≤ height[i] ≤ 10⁵

<details>
<summary>💡 Hint</summary>
Use two pointers with left_max and right_max tracking.
</details>

<details>
<summary>✅ Solution</summary>

```python
def trap(height):
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
</details>

---

### Problem 12: Median of Two Sorted Arrays
**Difficulty**: Hard  
**Pattern**: Binary Search

**Problem**: Find median of two sorted arrays in O(log(m+n)) time.

**Example**:
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.0
```

**Constraints**:
- 0 ≤ m ≤ 1000
- 0 ≤ n ≤
