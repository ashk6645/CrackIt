# 📝 Queue Problems - Practice Set

## Problem Categories

### 🟢 Easy Problems (5 problems)
### 🟡 Medium Problems (5 problems)
### 🔴 Hard Problems (5 problems)

---

## 🟢 Easy Problems

### Problem 1: Implement Queue using Stacks
**LeetCode 232** | **Difficulty: Easy** | **Time: 20 mins**

Implement a first-in-first-out (FIFO) queue using only two stacks.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use two stacks: input stack for enqueue, output stack for dequeue
2. For dequeue: if output stack is empty, transfer all from input stack
3. This ensures FIFO order with amortized O(1) operations

**Time Complexity:** Amortized O(1) for all operations  
**Space Complexity:** O(n)

**Java**
```java
class MyQueue {
    private Stack<Integer> input;
    private Stack<Integer> output;
    
    public MyQueue() {
        input = new Stack<>();
        output = new Stack<>();
    }
    
    public void push(int x) {
        input.push(x);
    }
    
    public int pop() {
        peek();
        return output.pop();
    }
    
    public int peek() {
        if (output.empty()) {
            while (!input.empty()) {
                output.push(input.pop());
            }
        }
        return output.peek();
    }
    
    public boolean empty() {
        return input.empty() && output.empty();
    }
}
```

**Python**
```python
class MyQueue:
    def __init__(self):
        self.input = []
        self.output = []
    
    def push(self, x):
        self.input.append(x)
    
    def pop(self):
        self.peek()
        return self.output.pop()
    
    def peek(self):
        if not self.output:
            while self.input:
                self.output.append(self.input.pop())
        return self.output[-1]
    
    def empty(self):
        return not self.input and not self.output
```
</details>

---

### Problem 2: Design Circular Queue
**LeetCode 622** | **Difficulty: Medium** | **Time: 25 mins**

Design your implementation of the circular queue with fixed size.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use array with head and tail pointers
2. Use modulo operation for circular wrapping
3. Keep track of size to distinguish empty vs full

**Time Complexity:** O(1) for all operations  
**Space Complexity:** O(k) where k is queue size

**Java**
```java
class MyCircularQueue {
    private int[] queue;
    private int head;
    private int tail;
    private int size;
    private int capacity;
    
    public MyCircularQueue(int k) {
        this.capacity = k;
        this.queue = new int[k];
        this.head = 0;
        this.tail = -1;
        this.size = 0;
    }
    
    public boolean enQueue(int value) {
        if (isFull()) return false;
        tail = (tail + 1) % capacity;
        queue[tail] = value;
        size++;
        return true;
    }
    
    public boolean deQueue() {
        if (isEmpty()) return false;
        head = (head + 1) % capacity;
        size--;
        return true;
    }
    
    public int Front() {
        if (isEmpty()) return -1;
        return queue[head];
    }
    
    public int Rear() {
        if (isEmpty()) return -1;
        return queue[tail];
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
    
    public boolean isFull() {
        return size == capacity;
    }
}
```
</details>

---

### Problem 3: Number of Recent Calls
**LeetCode 933** | **Difficulty: Easy** | **Time: 15 mins**

Count the number of recent requests within a certain time frame.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use queue to store timestamps
2. For each new request, remove old timestamps outside the 3000ms window
3. Return current queue size

**Time Complexity:** O(1) amortized  
**Space Complexity:** O(n) where n is number of valid timestamps

**Java**
```java
class RecentCounter {
    private Queue<Integer> queue;
    
    public RecentCounter() {
        queue = new LinkedList<>();
    }
    
    public int ping(int t) {
        queue.offer(t);
        while (queue.peek() < t - 3000) {
            queue.poll();
        }
        return queue.size();
    }
}
```

**Python**
```python
from collections import deque

class RecentCounter:
    def __init__(self):
        self.queue = deque()
    
    def ping(self, t):
        self.queue.append(t)
        while self.queue[0] < t - 3000:
            self.queue.popleft()
        return len(self.queue)
```
</details>

---

### Problem 4: First Unique Character in a String
**LeetCode 387** | **Difficulty: Easy** | **Time: 20 mins**

Find the first non-repeating character in a string and return its index.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Count frequency of each character
2. Iterate again to find first character with count 1
3. Alternative: Use queue to track potential unique characters

**Time Complexity:** O(n)  
**Space Complexity:** O(1) - limited to 26 characters

**Java (HashMap approach)**
```java
public int firstUniqChar(String s) {
    Map<Character, Integer> count = new HashMap<>();
    
    // Count frequencies
    for (char c : s.toCharArray()) {
        count.put(c, count.getOrDefault(c, 0) + 1);
    }
    
    // Find first unique
    for (int i = 0; i < s.length(); i++) {
        if (count.get(s.charAt(i)) == 1) {
            return i;
        }
    }
    
    return -1;
}
```

**Java (Queue approach)**
```java
public int firstUniqChar(String s) {
    Queue<int[]> queue = new LinkedList<>();
    int[] count = new int[26];
    
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        count[c - 'a']++;
        queue.offer(new int[]{i, c - 'a'});
        
        while (!queue.isEmpty() && count[queue.peek()[1]] > 1) {
            queue.poll();
        }
    }
    
    return queue.isEmpty() ? -1 : queue.peek()[0];
}
```
</details>

---

### Problem 5: Moving Average from Data Stream
**LeetCode 346** | **Difficulty: Easy** | **Time: 15 mins**

Calculate the moving average of all integers in a sliding window.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use queue to maintain sliding window
2. Keep running sum and update when window size exceeds limit
3. Calculate average as sum / window_size

**Time Complexity:** O(1) per operation  
**Space Complexity:** O(n) where n is window size

**Java**
```java
class MovingAverage {
    private Queue<Integer> queue;
    private int size;
    private double sum;
    
    public MovingAverage(int size) {
        this.queue = new LinkedList<>();
        this.size = size;
        this.sum = 0;
    }
    
    public double next(int val) {
        queue.offer(val);
        sum += val;
        
        if (queue.size() > size) {
            sum -= queue.poll();
        }
        
        return sum / queue.size();
    }
}
```

**Python**
```python
from collections import deque

class MovingAverage:
    def __init__(self, size):
        self.queue = deque()
        self.size = size
        self.sum = 0
    
    def next(self, val):
        self.queue.append(val)
        self.sum += val
        
        if len(self.queue) > self.size:
            self.sum -= self.queue.popleft()
        
        return self.sum / len(self.queue)
```
</details>

---

## 🟡 Medium Problems

### Problem 6: Binary Tree Level Order Traversal
**LeetCode 102** | **Difficulty: Medium** | **Time: 30 mins**

Return the level order traversal of a binary tree's nodes' values.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use BFS with queue to traverse level by level
2. Process all nodes at current level before moving to next
3. Track level size to separate levels

**Time Complexity:** O(n)  
**Space Complexity:** O(w) where w is maximum width

**Java**
```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    
    while (!queue.isEmpty()) {
        int levelSize = queue.size();
        List<Integer> level = new ArrayList<>();
        
        for (int i = 0; i < levelSize; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);
            
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        
        result.add(level);
    }
    
    return result;
}
```

**Python**
```python
from collections import deque

def levelOrder(root):
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        level_size = len(queue)
        level = []
        
        for _ in range(level_size):
            node = queue.popleft()
            level.append(node.val)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        result.append(level)
    
    return result
```
</details>

---

### Problem 7: Sliding Window Maximum
**LeetCode 239** | **Difficulty: Hard** | **Time: 45 mins**

Return the maximum sliding window for each position in the array.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use deque to maintain indices of array elements
2. Keep deque in decreasing order of values
3. Front of deque always contains index of maximum element

**Time Complexity:** O(n)  
**Space Complexity:** O(k)

**Java**
```java
public int[] maxSlidingWindow(int[] nums, int k) {
    Deque<Integer> deque = new ArrayDeque<>();
    int[] result = new int[nums.length - k + 1];
    
    for (int i = 0; i < nums.length; i++) {
        // Remove indices outside current window
        while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
            deque.pollFirst();
        }
        
        // Remove indices of smaller elements
        while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
            deque.pollLast();
        }
        
        deque.offerLast(i);
        
        // Add to result when window is complete
        if (i >= k - 1) {
            result[i - k + 1] = nums[deque.peekFirst()];
        }
    }
    
    return result;
}
```
</details>

---

### Problem 8: Rotting Oranges
**LeetCode 994** | **Difficulty: Medium** | **Time: 35 mins**

Determine the minimum time for all oranges to rot, or -1 if impossible.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use BFS to simulate rotting process
2. Start with all initially rotten oranges in queue
3. Process level by level, each level represents one minute

**Time Complexity:** O(m * n)  
**Space Complexity:** O(m * n)

**Java**
```java
public int orangesRotting(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    Queue<int[]> queue = new LinkedList<>();
    int fresh = 0;
    
    // Count fresh oranges and add rotten ones to queue
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == 1) fresh++;
            else if (grid[i][j] == 2) queue.offer(new int[]{i, j});
        }
    }
    
    if (fresh == 0) return 0;
    
    int[][] directions = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    int minutes = 0;
    
    while (!queue.isEmpty()) {
        int size = queue.size();
        boolean rotted = false;
        
        for (int i = 0; i < size; i++) {
            int[] pos = queue.poll();
            
            for (int[] dir : directions) {
                int newRow = pos[0] + dir[0];
                int newCol = pos[1] + dir[1];
                
                if (newRow >= 0 && newRow < m && newCol >= 0 && newCol < n 
                    && grid[newRow][newCol] == 1) {
                    grid[newRow][newCol] = 2;
                    queue.offer(new int[]{newRow, newCol});
                    fresh--;
                    rotted = true;
                }
            }
        }
        
        if (rotted) minutes++;
    }
    
    return fresh == 0 ? minutes : -1;
}
```
</details>

---

### Problem 9: Open the Lock
**LeetCode 752** | **Difficulty: Medium** | **Time: 40 mins**

Find minimum steps to open a 4-digit lock, avoiding deadends.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use BFS to find shortest path from "0000" to target
2. Generate all possible next states (8 possibilities per state)
3. Use visited set to avoid cycles and deadends

**Time Complexity:** O(10^4) = O(1) - constant search space  
**Space Complexity:** O(10^4) = O(1) - constant space

**Java**
```java
public int openLock(String[] deadends, String target) {
    Set<String> deadSet = new HashSet<>(Arrays.asList(deadends));
    if (deadSet.contains("0000")) return -1;
    if (target.equals("0000")) return 0;
    
    Queue<String> queue = new LinkedList<>();
    Set<String> visited = new HashSet<>();
    
    queue.offer("0000");
    visited.add("0000");
    int steps = 0;
    
    while (!queue.isEmpty()) {
        int size = queue.size();
        steps++;
        
        for (int i = 0; i < size; i++) {
            String current = queue.poll();
            
            for (String next : getNextStates(current)) {
                if (visited.contains(next) || deadSet.contains(next)) {
                    continue;
                }
                
                if (next.equals(target)) {
                    return steps;
                }
                
                queue.offer(next);
                visited.add(next);
            }
        }
    }
    
    return -1;
}

private List<String> getNextStates(String lock) {
    List<String> states = new ArrayList<>();
    char[] chars = lock.toCharArray();
    
    for (int i = 0; i < 4; i++) {
        char original = chars[i];
        
        // Turn up
        chars[i] = original == '9' ? '0' : (char)(original + 1);
        states.add(new String(chars));
        
        // Turn down
        chars[i] = original == '0' ? '9' : (char)(original - 1);
        states.add(new String(chars));
        
        chars[i] = original; // restore
    }
    
    return states;
}
```
</details>

---

### Problem 10: Perfect Squares
**LeetCode 279** | **Difficulty: Medium** | **Time: 35 mins**

Find the minimum number of perfect squares that sum to given number n.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use BFS where each level represents number of squares used
2. From each number, try subtracting all possible perfect squares
3. First time we reach 0, return the level

**Time Complexity:** O(n * √n)  
**Space Complexity:** O(n)

**Java**
```java
public int numSquares(int n) {
    Queue<Integer> queue = new LinkedList<>();
    Set<Integer> visited = new HashSet<>();
    
    queue.offer(n);
    visited.add(n);
    int level = 0;
    
    while (!queue.isEmpty()) {
        int size = queue.size();
        level++;
        
        for (int i = 0; i < size; i++) {
            int current = queue.poll();
            
            for (int j = 1; j * j <= current; j++) {
                int next = current - j * j;
                
                if (next == 0) {
                    return level;
                }
                
                if (!visited.contains(next)) {
                    queue.offer(next);
                    visited.add(next);
                }
            }
        }
    }
    
    return level;
}
```

**Dynamic Programming Alternative:**
```java
public int numSquares(int n) {
    int[] dp = new int[n + 1];
    Arrays.fill(dp, Integer.MAX_VALUE);
    dp[0] = 0;
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j * j <= i; j++) {
            dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
        }
    }
    
    return dp[n];
}
```
</details>

---

## 🔴 Hard Problems

### Problem 11: Shortest Path in Binary Matrix
**LeetCode 1091** | **Difficulty: Medium-Hard** | **Time: 40 mins**

Find shortest path from top-left to bottom-right in binary matrix.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use BFS to find shortest path (guarantees minimum steps)
2. Explore all 8 directions from each cell
3. Mark visited cells to avoid revisiting

**Time Complexity:** O(n^2)  
**Space Complexity:** O(n^2)

**Java**
```java
public int shortestPathBinaryMatrix(int[][] grid) {
    int n = grid.length;
    if (grid[0][0] != 0 || grid[n-1][n-1] != 0) return -1;
    
    Queue<int[]> queue = new LinkedList<>();
    boolean[][] visited = new boolean[n][n];
    int[][] directions = {{-1,-1},{-1,0},{-1,1},{0,-1},{0,1},{1,-1},{1,0},{1,1}};
    
    queue.offer(new int[]{0, 0, 1}); // row, col, path length
    visited[0][0] = true;
    
    while (!queue.isEmpty()) {
        int[] current = queue.poll();
        int row = current[0], col = current[1], pathLen = current[2];
        
        if (row == n-1 && col == n-1) {
            return pathLen;
        }
        
        for (int[] dir : directions) {
            int newRow = row + dir[0];
            int newCol = col + dir[1];
            
            if (newRow >= 0 && newRow < n && newCol >= 0 && newCol < n 
                && grid[newRow][newCol] == 0 && !visited[newRow][newCol]) {
                queue.offer(new int[]{newRow, newCol, pathLen + 1});
                visited[newRow][newCol] = true;
            }
        }
    }
    
    return -1;
}
```
</details>

---

### Problem 12: Minimum Genetic Mutation
**LeetCode 433** | **Difficulty: Medium-Hard** | **Time: 45 mins**

Find minimum mutations needed to transform start gene to end gene.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use BFS to find minimum transformations
2. Generate all possible single-character mutations
3. Only consider mutations that are in the gene bank

**Time Complexity:** O(n * m) where n is bank size, m is gene length  
**Space Complexity:** O(n * m)

**Java**
```java
public int minMutation(String start, String end, String[] bank) {
    Set<String> bankSet = new HashSet<>(Arrays.asList(bank));
    if (!bankSet.contains(end)) return -1;
    
    Queue<String> queue = new LinkedList<>();
    Set<String> visited = new HashSet<>();
    char[] genes = {'A', 'C', 'G', 'T'};
    
    queue.offer(start);
    visited.add(start);
    int mutations = 0;
    
    while (!queue.isEmpty()) {
        int size = queue.size();
        
        for (int i = 0; i < size; i++) {
            String current = queue.poll();
            
            if (current.equals(end)) {
                return mutations;
            }
            
            char[] currentArray = current.toCharArray();
            for (int j = 0; j < currentArray.length; j++) {
                char originalChar = currentArray[j];
                
                for (char gene : genes) {
                    if (gene == originalChar) continue;
                    
                    currentArray[j] = gene;
                    String mutated = new String(currentArray);
                    
                    if (bankSet.contains(mutated) && !visited.contains(mutated)) {
                        queue.offer(mutated);
                        visited.add(mutated);
                    }
                }
                
                currentArray[j] = originalChar; // restore
            }
        }
        
        mutations++;
    }
    
    return -1;
}
```
</details>

---

### Problem 13: Cut Off Trees for Golf Event
**LeetCode 675** | **Difficulty: Hard** | **Time: 60 mins**

Find minimum steps to cut all trees in order of height.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Sort all trees by height
2. Use BFS to find shortest path between consecutive trees
3. Sum up all the shortest paths

**Time Complexity:** O(m^2 * n^2) worst case  
**Space Complexity:** O(m * n)

**Java**
```java
public int cutOffTree(List<List<Integer>> forest) {
    List<int[]> trees = new ArrayList<>();
    
    // Collect all trees with their positions
    for (int i = 0; i < forest.size(); i++) {
        for (int j = 0; j < forest.get(i).size(); j++) {
            int height = forest.get(i).get(j);
            if (height > 1) {
                trees.add(new int[]{height, i, j});
            }
        }
    }
    
    // Sort trees by height
    trees.sort((a, b) -> a[0] - b[0]);
    
    int totalSteps = 0;
    int startRow = 0, startCol = 0;
    
    for (int[] tree : trees) {
        int steps = bfs(forest, startRow, startCol, tree[1], tree[2]);
        if (steps == -1) return -1;
        
        totalSteps += steps;
        startRow = tree[1];
        startCol = tree[2];
    }
    
    return totalSteps;
}

private int bfs(List<List<Integer>> forest, int startRow, int startCol, 
                int endRow, int endCol) {
    if (startRow == endRow && startCol == endCol) return 0;
    
    int m = forest.size(), n = forest.get(0).size();
    Queue<int[]> queue = new LinkedList<>();
    boolean[][] visited = new boolean[m][n];
    int[][] directions = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    
    queue.offer(new int[]{startRow, startCol, 0});
    visited[startRow][startCol] = true;
    
    while (!queue.isEmpty()) {
        int[] current = queue.poll();
        
        for (int[] dir : directions) {
            int newRow = current[0] + dir[0];
            int newCol = current[1] + dir[1];
            int steps = current[2] + 1;
            
            if (newRow == endRow && newCol == endCol) {
                return steps;
            }
            
            if (newRow >= 0 && newRow < m && newCol >= 0 && newCol < n 
                && !visited[newRow][newCol] && forest.get(newRow).get(newCol) != 0) {
                queue.offer(new int[]{newRow, newCol, steps});
                visited[newRow][newCol] = true;
            }
        }
    }
    
    return -1;
}
```
</details>

---

### Problem 14: Bus Routes
**LeetCode 815** | **Difficulty: Hard** | **Time: 50 mins**

Find minimum number of buses to reach target from source.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Build graph where each bus route is a node
2. Use BFS to find minimum transfers between routes
3. Handle stops that belong to multiple routes

**Time Complexity:** O(N^2 + M) where N is routes, M is total stops  
**Space Complexity:** O(N^2 + M)

**Java**
```java
public int numBusesToDestination(int[][] routes, int source, int target) {
    if (source == target) return 0;
    
    Map<Integer, List<Integer>> stopToRoutes = new HashMap<>();
    
    // Build mapping from stop to routes
    for (int i = 0; i < routes.length; i++) {
        for (int stop : routes[i]) {
            stopToRoutes.computeIfAbsent(stop, k -> new ArrayList<>()).add(i);
        }
    }
    
    Queue<Integer> queue = new LinkedList<>();
    Set<Integer> visitedRoutes = new HashSet<>();
    
    // Start with all routes containing source
    for (int route : stopToRoutes.getOrDefault(source, new ArrayList<>())) {
        queue.offer(route);
        visitedRoutes.add(route);
    }
    
    int buses = 1;
    
    while (!queue.isEmpty()) {
        int size = queue.size();
        
        for (int i = 0; i < size; i++) {
            int currentRoute = queue.poll();
            
            // Check all stops in current route
            for (int stop : routes[currentRoute]) {
                if (stop == target) {
                    return buses;
                }
                
                // Add all unvisited routes containing this stop
                for (int nextRoute : stopToRoutes.getOrDefault(stop, new ArrayList<>())) {
                    if (!visitedRoutes.contains(nextRoute)) {
                        queue.offer(nextRoute);
                        visitedRoutes.add(nextRoute);
                    }
                }
            }
        }
        
        buses++;
    }
    
    return -1;
}
```
</details>

---

### Problem 15: Alien Dictionary
**LeetCode 269** | **Difficulty: Hard** | **Time: 55 mins**

Derive the order of letters in alien language from sorted dictionary.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Build directed graph from character ordering constraints
2. Use topological sort (BFS with indegree) to find valid ordering
3. Detect cycles which indicate invalid input

**Time Complexity:** O(C) where C is total content length  
**Space Complexity:** O(1) - at most 26 characters

**Java**
```java
public String alienOrder(String[] words) {
    Map<Character, Set<Character>> graph = new HashMap<>();
    Map<Character, Integer> indegree = new HashMap<>();
    
    // Initialize all characters
    for (String word : words) {
        for (char c : word.toCharArray()) {
            graph.put(c, new HashSet<>());
            indegree.put(c, 0);
        }
    }
    
    // Build graph
    for (int i = 0; i < words.length - 1; i++) {
        String word1 = words[i];
        String word2 = words[i + 1];
        
        // Check for invalid case: prefix is longer
        if (word1.length() > word2.length() && word1.startsWith(word2)) {
            return "";
        }
        
        for (int j = 0; j < Math.min(word1.length(), word2.length()); j++) {
            char c1 = word1.charAt(j);
            char c2 = word2.charAt(j);
            
            if (c1 != c2) {
                if (!graph.get(c1).contains(c2)) {
                    graph.get(c1).add(c2);
                    indegree.put(c2, indegree.get(c2) + 1);
                }
                break;
            }
        }
    }
    
    // Topological sort using BFS
    Queue<Character> queue = new LinkedList<>();
    for (char c : indegree.keySet()) {
        if (indegree.get(c) == 0) {
            queue.offer(c);
        }
    }
    
    StringBuilder result = new StringBuilder();
    
    while (!queue.isEmpty()) {
        char current = queue.poll();
        result.append(current);
        
        for (char neighbor : graph.get(current)) {
            indegree.put(neighbor, indegree.get(neighbor) - 1);
            if (indegree.get(neighbor) == 0) {
                queue.offer(neighbor);
            }
        }
    }
    
    return result.length() == indegree.size() ? result.toString() : "";
}
```
</details>

---

## Common Interview Patterns

- **BFS Level-order Traversal**: Process nodes level by level
- **Shortest Path**: BFS guarantees minimum steps in unweighted graphs
- **Multi-source BFS**: Start BFS from multiple sources simultaneously
- **State Space Search**: Model problems as graph traversal
- **Deque for Optimization**: Sliding window maximum, monotonic queue

## Common Mistakes

- Forgetting to mark nodes as visited in BFS
- Not handling the case when queue becomes empty
- Mixing up BFS (level-order) with DFS (depth-first)
- Not considering all possible directions/states in state space problems
- Incorrect level counting in BFS

## Interview Tips

- Always ask about constraints and edge cases
- Consider if BFS is more appropriate than DFS for the problem
- Use appropriate data structures (deque for optimization, priority queue for weighted graphs)
- Think about state representation for complex problems
- Practice drawing out BFS execution for sample inputs

## Further Practice

- [LeetCode Queue Problems](https://leetcode.com/tag/queue/)
- [GeeksforGeeks Queue Practice](https://www.geeksforgeeks.org/queue-data-structure/)
- [InterviewBit Queue](https://www.interviewbit.com/courses/programming/topics/queues/)