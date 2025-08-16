# 🧠 Dynamic Programming - Optimal Substructure & Memoization

Welcome to the **Dynamic Programming** section! Master the art of breaking down complex problems into simpler subproblems and avoiding redundant calculations.

---

## 📚 What is Dynamic Programming?

**Dynamic Programming (DP)** is an algorithmic paradigm that solves complex problems by:
1. **Breaking them down** into simpler subproblems
2. **Storing solutions** to subproblems (memoization)
3. **Reusing solutions** to avoid redundant calculations
4. **Building up** optimal solutions from smaller ones

**Key Insight**: If you can solve a problem optimally by solving its subproblems optimally, then it has **optimal substructure**.

---

## 🔑 Core Concepts

### 🧩 Optimal Substructure
A problem has optimal substructure if the optimal solution contains optimal solutions to subproblems.

**Example**: Shortest path - if the shortest path from A to C goes through B, then the path from A to B must also be shortest.

### 🔄 Overlapping Subproblems
The same subproblems are solved multiple times in a naive recursive approach.

**Example**: Fibonacci - `fib(n) = fib(n-1) + fib(n-2)` recalculates `fib(n-2)` in both branches.

### 💾 Memoization vs Tabulation
- **Memoization**: Top-down approach with recursive calls and caching
- **Tabulation**: Bottom-up approach building solution iteratively

---

## 🛠️ DP Implementation Patterns

### 1. Recursive with Memoization (Top-Down)
```java
public int fibMemo(int n, int[] memo) {
    if (n <= 1) return n;
    if (memo[n] != 0) return memo[n];
    
    memo[n] = fibMemo(n-1, memo) + fibMemo(n-2, memo);
    return memo[n];
}
```

### 2. Tabulation (Bottom-Up)
```java
public int fibTabulation(int n) {
    if (n <= 1) return n;
    
    int[] dp = new int[n + 1];
    dp[0] = 0;
    dp[1] = 1;
    
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    
    return dp[n];
}
```

### 3. Space-Optimized
```java
public int fibOptimized(int n) {
    if (n <= 1) return n;
    
    int prev2 = 0, prev1 = 1;
    
    for (int i = 2; i <= n; i++) {
        int current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
    }
    
    return prev1;
}
```

---

## 🎯 Common DP Patterns

### 1. Linear DP (1D Array)
**Problems**: Fibonacci, Climbing Stairs, House Robber
```java
// Template
for (int i = 1; i < n; i++) {
    dp[i] = function(dp[i-1], dp[i-2], ...);
}
```

### 2. Grid DP (2D Array)
**Problems**: Unique Paths, Minimum Path Sum, Edit Distance
```java
// Template
for (int i = 1; i < m; i++) {
    for (int j = 1; j < n; j++) {
        dp[i][j] = function(dp[i-1][j], dp[i][j-1], ...);
    }
}
```

### 3. Interval DP
**Problems**: Matrix Chain Multiplication, Burst Balloons
```java
// Template
for (int len = 2; len <= n; len++) {
    for (int i = 0; i <= n - len; i++) {
        int j = i + len - 1;
        for (int k = i; k < j; k++) {
            dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k+1][j] + cost);
        }
    }
}
```

### 4. Tree DP
**Problems**: Binary Tree Maximum Path Sum, House Robber III
```java
// Template
int[] robHelper(TreeNode root) {
    if (root == null) return new int[]{0, 0};
    
    int[] left = robHelper(root.left);
    int[] right = robHelper(root.right);
    
    int rob = root.val + left[1] + right[1];
    int notRob = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
    
    return new int[]{rob, notRob};
}
```

---

## 🔥 Classic DP Problems

### 📈 Sequence Problems
| Problem | Pattern | Key Insight |
|---------|---------|-------------|
| **Longest Increasing Subsequence** | Linear DP | dp[i] = max length ending at i |
| **Longest Common Subsequence** | 2D DP | Match characters or skip one |
| **Edit Distance** | 2D DP | Insert, delete, or replace operations |

### 💰 Knapsack Problems
| Problem | Type | Approach |
|---------|------|----------|
| **0/1 Knapsack** | Classic | Include or exclude each item |
| **Unbounded Knapsack** | Variation | Can use unlimited items |
| **Coin Change** | Application | Minimum coins for amount |

### 🎯 Optimization Problems
| Problem | Focus | Technique |
|---------|-------|-----------|
| **Maximum Subarray** | Array | Kadane's algorithm |
| **Best Time to Buy/Sell Stock** | Sequence | State machine DP |
| **Palindrome Partitioning** | String | Interval DP |

---

## 🧠 Problem-Solving Strategy

### 🔍 Step 1: Identify DP Problem
**Signs that suggest DP**:
- Optimization problems (min/max)
- Counting problems (number of ways)
- Decision problems (can/cannot)
- Overlapping subproblems in recursive solution

### 📝 Step 2: Define the State
**Questions to ask**:
- What parameters change between subproblems?
- What information do I need to compute the answer?
- How can I represent the state with minimum parameters?

### 🔄 Step 3: Find the Recurrence
**Common patterns**:
- **Choice**: `dp[i] = max(include, exclude)`
- **Sequence**: `dp[i] = dp[i-1] + dp[i-2] + ...`
- **Grid**: `dp[i][j] = f(dp[i-1][j], dp[i][j-1])`

### 🏁 Step 4: Handle Base Cases
**Important considerations**:
- What are the smallest subproblems?
- What happens when parameters are 0 or negative?
- Initialize appropriately (0, infinity, etc.)

### ⚡ Step 5: Optimize Space
**Techniques**:
- Rolling arrays for 2D problems
- Space compression when only previous states needed
- In-place computation when possible

---

## 💡 Advanced DP Techniques

### 🎭 State Machine DP
Used when the state depends on previous actions or modes.

**Example: Best Time to Buy and Sell Stock**
```java
public int maxProfit(int[] prices) {
    int held = -prices[0];  // Holding a stock
    int sold = 0;           // Not holding a stock
    
    for (int i = 1; i < prices.length; i++) {
        int newHeld = Math.max(held, sold - prices[i]);
        int newSold = Math.max(sold, held + prices[i]);
        held = newHeld;
        sold = newSold;
    }
    
    return sold;
}
```

### 🎯 Bitmask DP
Used when state involves subsets or combinations.

**Example: Traveling Salesman Problem**
```java
// dp[mask][i] = minimum cost to visit all cities in mask and end at city i
for (int mask = 0; mask < (1 << n); mask++) {
    for (int i = 0; i < n; i++) {
        if ((mask & (1 << i)) == 0) continue;
        
        for (int j = 0; j < n; j++) {
            if (i == j || (mask & (1 << j)) == 0) continue;
            
            dp[mask][i] = Math.min(dp[mask][i], 
                                   dp[mask ^ (1 << i)][j] + dist[j][i]);
        }
    }
}
```

### 🌊 Digit DP
Used for problems involving number constraints.

**Example: Count numbers with specific digit properties**
```java
int digitDP(String num, int pos, int tight, int started, boolean[] used) {
    if (pos == num.length()) return started ? 1 : 0;
    
    if (memo[pos][tight][started] != -1) {
        return memo[pos][tight][started];
    }
    
    int limit = tight == 1 ? (num.charAt(pos) - '0') : 9;
    int result = 0;
    
    for (int digit = 0; digit <= limit; digit++) {
        // Process each digit choice
        int newTight = tight == 1 && digit == limit ? 1 : 0;
        int newStarted = started || (digit > 0) ? 1 : 0;
        
        result += digitDP(num, pos + 1, newTight, newStarted, used);
    }
    
    return memo[pos][tight][started] = result;
}
```

---

## ⚡ Performance Optimization

### 🚀 Time Complexity Analysis
| Problem Type | Naive Recursive | DP Solution | Optimization |
|-------------|-----------------|-------------|--------------|
| **Fibonacci** | O(2^n) | O(n) | Matrix exponentiation O(log n) |
| **LCS** | O(2^(m+n)) | O(m*n) | Space compression O(min(m,n)) |
| **Knapsack** | O(2^n) | O(n*W) | Space compression O(W) |

### 💾 Space Optimization Techniques
```java
// 2D to 1D optimization example (Knapsack)
// Instead of dp[i][w], use dp[w] and iterate backwards
for (int i = 0; i < n; i++) {
    for (int w = capacity; w >= weight[i]; w--) {
        dp[w] = Math.max(dp[w], dp[w - weight[i]] + value[i]);
    }
}
```

---

## 🚫 Common Mistakes & Pitfalls

### ❌ State Definition Errors
1. **Too many parameters** - makes solution complex
2. **Missing parameters** - cannot solve subproblems correctly
3. **Wrong state representation** - doesn't capture problem essence

### ❌ Implementation Issues
1. **Wrong iteration order** - dependencies not satisfied
2. **Incorrect base cases** - leads to wrong answers
3. **Space optimization errors** - overwriting needed values

### ❌ Logical Errors
1. **Missing state transitions** - not considering all choices
2. **Wrong recurrence relation** - incorrect problem breakdown
3. **Boundary condition errors** - array out of bounds

### ✅ Best Practices
```java
// Always validate inputs
if (n <= 0) return 0;

// Initialize DP table properly
int[][] dp = new int[m][n];
Arrays.fill(dp[0], baseValue);

// Clear variable names for states
int withItem = dp[i-1][w-weight] + value;
int withoutItem = dp[i-1][w];
dp[i][w] = Math.max(withItem, withoutItem);

// Consider edge cases
if (w < weight[i]) dp[i][w] = dp[i-1][w];
```

---

## 🎯 Interview Preparation Strategy

### 🔥 Must-Master Problems
1. **Fibonacci Sequence** - Basic DP understanding
2. **Climbing Stairs** - Simple state transition
3. **Coin Change** - Unbounded knapsack
4. **Longest Increasing Subsequence** - O(n log n) optimization
5. **Edit Distance** - 2D DP classic
6. **House Robber** - Linear DP with constraints
7. **Unique Paths** - Grid DP fundamentals

### 💡 Problem Categories by Difficulty

#### 🟢 Beginner Level
- Simple recurrence relations
- 1D DP arrays
- Clear state definitions

#### 🟡 Intermediate Level
- 2D DP problems
- Multiple choice at each step
- Space optimization techniques

#### 🔴 Advanced Level
- Complex state definitions
- Multiple DP dimensions
- Advanced optimization techniques

### 🎤 Common Interview Questions
1. "Explain the difference between memoization and tabulation"
2. "How do you identify when to use dynamic programming?"
3. "Walk me through optimizing the space complexity of this DP solution"
4. "What's the time complexity and why?"
5. "Can you solve this problem without DP?"

---

## 📈 Learning Progression

### Week 1: Foundations
- **Day 1-2**: DP concepts and Fibonacci variations
- **Day 3-4**: Linear DP problems (Climbing Stairs, House Robber)
- **Day 5-7**: Practice basic 1D DP problems

### Week 2: 2D DP
- **Day 1-3**: Grid problems (Unique Paths, Minimum Path Sum)
- **Day 4-5**: String DP (LCS, Edit Distance)
- **Day 6-7**: Knapsack problems (0/1, Unbounded)

### Week 3: Advanced Patterns
- **Day 1-3**: Interval DP and state machines
- **Day 4-5**: Tree DP and complex states
- **Day 6-7**: Optimization techniques and edge cases

---

## 🛠️ DP Problem Templates

### Linear DP Template
```java
public int solve(int[] arr) {
    int n = arr.length;
    int[] dp = new int[n];
    
    // Base case
    dp[0] = arr[0];
    
    // Fill DP table
    for (int i = 1; i < n; i++) {
        dp[i] = Math.max(dp[i-1], arr[i]); // Example recurrence
    }
    
    return dp[n-1];
}
```

### 2D DP Template
```java
public int solve(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];
    
    // Base cases
    dp[0][0] = grid[0][0];
    
    // Fill first row and column
    for (int i = 1; i < m; i++) dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; j++) dp[0][j] = dp[0][j-1] + grid[0][j];
    
    // Fill rest of the table
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + grid[i][j];
        }
    }
    
    return dp[m-1][n-1];
}
```

---

## 📚 Additional Resources

### 📖 Study Materials
- [DP Patterns for Coding Interviews](https://leetcode.com/discuss/general-discussion/458695/dynamic-programming-patterns)
- [MIT DP Lectures](https://ocw.mit.edu/courses/introduction-to-algorithms/)
- [Competitive Programming DP](https://cp-algorithms.com/dynamic_programming/)

### 🎥 Video Resources
- Dynamic programming fundamentals
- Problem-solving walkthroughs
- Optimization techniques
- Interview question discussions

---

**Ready to master dynamic programming?** Check out our [Problems.md](./Problems.md) for comprehensive practice! 🧠

**Next Topic**: [Sorting & Searching - Fundamental Algorithms](../11.%20Sorting%20&%20Searching/)