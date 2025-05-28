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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}

// Time: O(n), Space: O(n)
```

#### C++
```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> num_to_index;
    for (int i = 0; i < nums.size(); ++i) {
        int complement = target - nums[i];
        if (num_to_index.count(complement)) {
            return {num_to_index[complement], i};
        }
        num_to_index[nums[i]] = i;
    }
    return {};
}

// Time: O(n), Space: O(n)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int writeIndex = 1;
    for (int readIndex = 1; readIndex < nums.length; readIndex++) {
        if (nums[readIndex] != nums[readIndex - 1]) {
            nums[writeIndex] = nums[readIndex];
            writeIndex++;
        }
    }
    return writeIndex;
}

// Time: O(n), Space: O(1)
```

#### C++
```cpp
int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;
    int writeIndex = 1;
    for (int readIndex = 1; readIndex < nums.size(); ++readIndex) {
        if (nums[readIndex] != nums[readIndex - 1]) {
            nums[writeIndex++] = nums[readIndex];
        }
    }
    return writeIndex;
}

// Time: O(n), Space: O(1)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int maxSubArray(int[] nums) {
    int maxSum = nums[0];
    int currentSum = nums[0];
    for (int i = 1; i < nums.length; i++) {
        currentSum = Math.max(nums[i], currentSum + nums[i]);
        maxSum = Math.max(maxSum, currentSum);
    }
    return maxSum;
}

// Time: O(n), Space: O(1)
```

#### C++
```cpp
int maxSubArray(vector<int>& nums) {
    int maxSum = nums[0];
    int currentSum = nums[0];
    for (int i = 1; i < nums.size(); ++i) {
        currentSum = max(nums[i], currentSum + nums[i]);
        maxSum = max(maxSum, currentSum);
    }
    return maxSum;
}

// Time: O(n), Space: O(1)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public void rotate(int[] nums, int k) {
    int n = nums.length;
    k = k % n;
    reverse(nums, 0, n - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, n - 1);
}

private void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}

// Time: O(n), Space: O(1)
```

#### C++
```cpp
void reverse(vector<int>& nums, int start, int end) {
    while (start < end) {
        swap(nums[start], nums[end]);
        start++;
        end--;
    }
}

void rotate(vector<int>& nums, int k) {
    int n = nums.size();
    k = k % n;
    reverse(nums, 0, n - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, n - 1);
}

// Time: O(n), Space: O(1)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int maxProfit(int[] prices) {
    int minPrice = Integer.MAX_VALUE;
    int maxProfit = 0;
    for (int price : prices) {
        if (price < minPrice) {
            minPrice = price;
        } else if (price - minPrice > maxProfit) {
            maxProfit = price - minPrice;
        }
    }
    return maxProfit;
}

// Time: O(n), Space: O(1)
```

#### C++
```cpp
int maxProfit(vector<int>& prices) {
    int minPrice = INT_MAX;
    int maxProfit = 0;
    for (int price : prices) {
        if (price < minPrice) {
            minPrice = price;
        } else if (price - minPrice > maxProfit) {
            maxProfit = price - minPrice;
        }
    }
    return maxProfit;
}

// Time: O(n), Space: O(1)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

# Time: O(n^2), Space: O(1)
```

#### Java
```java
public List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    int n = nums.length;
    for (int i = 0; i < n - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        int left = i + 1, right = n - 1;
        while (left < right) {
            int total = nums[i] + nums[left] + nums[right];
            if (total == 0) {
                result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;
                left++;
                right--;
            } else if (total < 0) {
                left++;
            } else {
                right--;
            }
        }
    }
    return result;
}
// Time: O(n^2), Space: O(1)
```

#### C++
```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<vector<int>> result;
    int n = nums.size();
    for (int i = 0; i < n - 2; ++i) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        int left = i + 1, right = n - 1;
        while (left < right) {
            int total = nums[i] + nums[left] + nums[right];
            if (total == 0) {
                result.push_back({nums[i], nums[left], nums[right]});
                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;
                left++;
                right--;
            } else if (total < 0) {
                left++;
            } else {
                right--;
            }
        }
    }
    return result;
}
// Time: O(n^2), Space: O(1)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int maxArea(int[] height) {
    int left = 0, right = height.length - 1;
    int maxWater = 0;
    while (left < right) {
        int width = right - left;
        int currentHeight = Math.min(height[left], height[right]);
        maxWater = Math.max(maxWater, width * currentHeight);
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    return maxWater;
}
// Time: O(n), Space: O(1)
```

#### C++
```cpp
int maxArea(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int maxWater = 0;
    while (left < right) {
        int width = right - left;
        int currentHeight = min(height[left], height[right]);
        maxWater = max(maxWater, width * currentHeight);
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    return maxWater;
}
// Time: O(n), Space: O(1)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int[] productExceptSelf(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    result[0] = 1;
    for (int i = 1; i < n; i++) {
        result[i] = result[i - 1] * nums[i - 1];
    }
    int suffixProduct = 1;
    for (int i = n - 1; i >= 0; i--) {
        result[i] *= suffixProduct;
        suffixProduct *= nums[i];
    }
    return result;
}
// Time: O(n), Space: O(1) extra
```

#### C++
```cpp
vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n, 1);
    for (int i = 1; i < n; ++i) {
        result[i] = result[i - 1] * nums[i - 1];
    }
    int suffixProduct = 1;
    for (int i = n - 1; i >= 0; --i) {
        result[i] *= suffixProduct;
        suffixProduct *= nums[i];
    }
    return result;
}
// Time: O(n), Space: O(1) extra
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int findMin(int[] nums) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int mid = (left + right) / 2;
        if (nums[mid] > nums[right]) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
    return nums[left];
}
// Time: O(log n), Space: O(1)
```

#### C++
```cpp
int findMin(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;
    while (left < right) {
        int mid = (left + right) / 2;
        if (nums[mid] > nums[right]) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
    return nums[left];
}
// Time: O(log n), Space: O(1)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int subarraySum(int[] nums, int k) {
    int count = 0, prefixSum = 0;
    Map<Integer, Integer> sumCount = new HashMap<>();
    sumCount.put(0, 1);
    for (int num : nums) {
        prefixSum += num;
        if (sumCount.containsKey(prefixSum - k)) {
            count += sumCount.get(prefixSum - k);
        }
        sumCount.put(prefixSum, sumCount.getOrDefault(prefixSum, 0) + 1);
    }
    return count;
}
// Time: O(n), Space: O(n)
```

#### C++
```cpp
int subarraySum(vector<int>& nums, int k) {
    unordered_map<int, int> sumCount;
    sumCount[0] = 1;
    int count = 0, prefixSum = 0;
    for (int num : nums) {
        prefixSum += num;
        if (sumCount.count(prefixSum - k)) {
            count += sumCount[prefixSum - k];
        }
        sumCount[prefixSum]++;
    }
    return count;
}
// Time: O(n), Space: O(n)
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
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
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

#### Java
```java
public int trap(int[] height) {
    if (height == null || height.length == 0) return 0;
    int left = 0, right = height.length - 1;
    int leftMax = 0, rightMax = 0, water = 0;
    while (left < right) {
        if (height[left] < height[right]) {
            if (height[left] >= leftMax) {
                leftMax = height[left];
            } else {
                water += leftMax - height[left];
            }
            left++;
        } else {
            if (height[right] >= rightMax) {
                rightMax = height[right];
            } else {
                water += rightMax - height[right];
            }
            right--;
        }
    }
    return water;
}
// Time: O(n), Space: O(1)
```

#### C++
```cpp
int trap(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int leftMax = 0, rightMax = 0, water = 0;
    while (left < right) {
        if (height[left] < height[right]) {
            if (height[left] >= leftMax) {
                leftMax = height[left];
            } else {
                water += leftMax - height[left];
            }
            left++;
        } else {
            if (height[right] >= rightMax) {
                rightMax = height[right];
            } else {
                water += rightMax - height[right];
            }
            right--;
        }
    }
    return water;
}
// Time: O(n), Space: O(1)
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
- 0 ≤ n ≤ 1000
- Both nums1 and nums2 are sorted independently in non-decreasing order.
- Median is defined as the middle value or the average of the middle values.

<details>
<summary>💡 Hint</summary>
Use binary search on the shorter array. Partition both arrays into left and right halves.
</details>

<details>
<summary>✅ Solution (Python/Java/C++)</summary>

#### Python
```python
def find_median_sorted_arrays(nums1, nums2):
    # Ensure nums1 is the smaller array
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1
    
    x, y = len(nums1), len(nums2)
    low, high = 0, x
    
    while low <= high:
        partitionX = (low + high) // 2
        partitionY = (x + y + 1) // 2 - partitionX
        
        # If we are at the extreme left end or right end of the array
        maxX = float('-inf') if partitionX == 0 else nums1[partitionX - 1]
        minX = float('inf') if partitionX == x else nums1[partitionX]
        
        maxY = float('-inf') if partitionY == 0 else nums2[partitionY - 1]
        minY = float('inf') if partitionY == y else nums2[partitionY]
        
        if maxX <= minY and maxY <= minX:
            # We have partitioned array at correct places
            if (x + y) % 2 == 0:
                return (max(maxX, maxY) + min(minX, minY)) / 2
            else:
                return max(maxX, maxY)
        elif maxX > minY:
            # We are too far on right side for partitionX. Go on left side.
            high = partitionX - 1
        else:
            # We are too far on left side for partitionX. Go on right side.
            low = partitionX + 1
    
    raise ValueError("Input arrays are not sorted.")
# Time: O(log(min(m, n))), Space: O(1)
```

#### Java
```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    if (nums1.length > nums2.length) return findMedianSortedArrays(nums2, nums1);
    int x = nums1.length, y = nums2.length;
    int low = 0, high = x;
    while (low <= high) {
        int partitionX = (low + high) / 2;
        int partitionY = (x + y + 1) / 2 - partitionX;
        int maxX = (partitionX == 0) ? Integer.MIN_VALUE : nums1[partitionX - 1];
        int minX = (partitionX == x) ? Integer.MAX_VALUE : nums1[partitionX];
        int maxY = (partitionY == 0) ? Integer.MIN_VALUE : nums2[partitionY - 1];
        int minY = (partitionY == y) ? Integer.MAX_VALUE : nums2[partitionY];
        if (maxX <= minY && maxY <= minX) {
            if ((x + y) % 2 == 0) {
                return ((double)Math.max(maxX, maxY) + Math.min(minX, minY)) / 2;
            } else {
                return (double)Math.max(maxX, maxY);
            }
        } else if (maxX > minY) {
            high = partitionX - 1;
        } else {
            low = partitionX + 1;
        }
    }
    throw new IllegalArgumentException();
}
// Time: O(log(min(m, n))), Space: O(1)
```

#### C++
```cpp
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    if (nums1.size() > nums2.size()) return findMedianSortedArrays(nums2, nums1);
    int x = nums1.size(), y = nums2.size();
    int low = 0, high = x;
    while (low <= high) {
        int partitionX = (low + high) / 2;
        int partitionY = (x + y + 1) / 2 - partitionX;
        int maxX = (partitionX == 0) ? INT_MIN : nums1[partitionX - 1];
        int minX = (partitionX == x) ? INT_MAX : nums1[partitionX];
        int maxY = (partitionY == 0) ? INT_MIN : nums2[partitionY - 1];
        int minY = (partitionY == y) ? INT_MAX : nums2[partitionY];
        if (maxX <= minY && maxY <= minX) {
            if ((x + y) % 2 == 0) {
                return (max(maxX, maxY) + min(minX, minY)) / 2.0;
            } else {
                return max(maxX, maxY);
            }
        } else if (maxX > minY) {
            high = partitionX - 1;
        } else {
            low = partitionX + 1;
        }
    }
    throw invalid_argument("Input arrays are not sorted.");
}
// Time: O(log(min(m, n))), Space: O(1)
```
</details>

---

## Common Interview Patterns
- **Two Pointers:** For pair, triplet, and partition problems.
- **Sliding Window:** For subarray/substring problems.
- **Prefix Sum:** For range queries and subarray sums.
- **Sorting & Binary Search:** For searching and order-based problems.

## Common Mistakes
- Not handling edge cases (empty, single element, all duplicates).
- Modifying the array when not allowed.
- Using extra space when in-place is required.

## Interview Tips
- Clarify if the array is sorted or unsorted.
- Ask about constraints and expected input size.
- State your approach and optimize if possible.

## Further Practice
- [LeetCode Array Problems](https://leetcode.com/tag/array/)
- [GeeksforGeeks Array Practice](https://www.geeksforgeeks.org/array-data-structure/)
- [InterviewBit Arrays](https://www.interviewbit.com/courses/programming/topics/arrays/)
