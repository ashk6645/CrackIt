# 📝 Stack Problems - Practice Set

## Problem Categories

### 🟢 Easy Problems (5 problems)
### 🟡 Medium Problems (5 problems)
### 🔴 Hard Problems (5 problems)

---

## 🟢 Easy Problems

### Problem 1: Valid Parentheses
**LeetCode 20** | **Difficulty: Easy** | **Time: 15 mins**

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use a stack to keep track of opening brackets
2. For each closing bracket, check if it matches the most recent opening bracket
3. Stack should be empty at the end for valid string

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();
    for (char c : s.toCharArray()) {
        if (c == '(' || c == '{' || c == '[') {
            stack.push(c);
        } else {
            if (stack.isEmpty()) return false;
            char top = stack.pop();
            if ((c == ')' && top != '(') ||
                (c == '}' && top != '{') ||
                (c == ']' && top != '[')) {
                return false;
            }
        }
    }
    return stack.isEmpty();
}
```

**Python**
```python
def isValid(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    
    for char in s:
        if char in mapping:
            if not stack or stack.pop() != mapping[char]:
                return False
        else:
            stack.append(char)
    
    return not stack
```
</details>

---

### Problem 2: Implement Stack using Queues
**LeetCode 225** | **Difficulty: Easy** | **Time: 20 mins**

Implement a last-in-first-out (LIFO) stack using only two queues.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use one queue as main storage
2. For push: add to queue, then rotate all previous elements
3. For pop: simply dequeue from front

**Time Complexity:** Push O(n), Pop O(1)  
**Space Complexity:** O(n)

**Java**
```java
class MyStack {
    private Queue<Integer> queue;
    
    public MyStack() {
        queue = new LinkedList<>();
    }
    
    public void push(int x) {
        queue.offer(x);
        int size = queue.size();
        for (int i = 0; i < size - 1; i++) {
            queue.offer(queue.poll());
        }
    }
    
    public int pop() {
        return queue.poll();
    }
    
    public int top() {
        return queue.peek();
    }
    
    public boolean empty() {
        return queue.isEmpty();
    }
}
```
</details>

---

### Problem 3: Min Stack
**LeetCode 155** | **Difficulty: Easy** | **Time: 25 mins**

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use two stacks: one for values, one for minimums
2. Push to min stack only when new minimum is found
3. Pop from min stack only when current minimum is removed

**Time Complexity:** O(1) for all operations  
**Space Complexity:** O(n)

**Java**
```java
class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;
    
    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }
    
    public void push(int val) {
        stack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }
    
    public void pop() {
        if (stack.pop().equals(minStack.peek())) {
            minStack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}
```
</details>

---

### Problem 4: Baseball Game
**LeetCode 682** | **Difficulty: Easy** | **Time: 15 mins**

You are keeping score for a baseball game with strange rules. Calculate the sum of scores.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use stack to keep track of valid scores
2. Process each operation according to rules
3. Sum all remaining scores in stack

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public int calPoints(String[] ops) {
    Stack<Integer> stack = new Stack<>();
    
    for (String op : ops) {
        if (op.equals("C")) {
            stack.pop();
        } else if (op.equals("D")) {
            stack.push(2 * stack.peek());
        } else if (op.equals("+")) {
            int top = stack.pop();
            int newTop = top + stack.peek();
            stack.push(top);
            stack.push(newTop);
        } else {
            stack.push(Integer.parseInt(op));
        }
    }
    
    int sum = 0;
    while (!stack.isEmpty()) {
        sum += stack.pop();
    }
    return sum;
}
```
</details>

---

### Problem 5: Remove All Adjacent Duplicates
**LeetCode 1047** | **Difficulty: Easy** | **Time: 20 mins**

Given a string, remove all adjacent duplicate characters.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use stack to build result string
2. If top of stack equals current character, pop (remove duplicate)
3. Otherwise, push current character

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public String removeDuplicates(String s) {
    Stack<Character> stack = new Stack<>();
    
    for (char c : s.toCharArray()) {
        if (!stack.isEmpty() && stack.peek() == c) {
            stack.pop();
        } else {
            stack.push(c);
        }
    }
    
    StringBuilder result = new StringBuilder();
    while (!stack.isEmpty()) {
        result.append(stack.pop());
    }
    
    return result.reverse().toString();
}
```
</details>

---

## 🟡 Medium Problems

### Problem 6: Daily Temperatures
**LeetCode 739** | **Difficulty: Medium** | **Time: 30 mins**

Given an array of integers temperatures, return an array where answer[i] is the number of days you have to wait after the ith day to get a warmer temperature.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use monotonic decreasing stack to store indices
2. For each temperature, pop smaller temperatures and calculate days
3. Push current index to stack

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] result = new int[n];
    Stack<Integer> stack = new Stack<>();
    
    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
            int index = stack.pop();
            result[index] = i - index;
        }
        stack.push(i);
    }
    
    return result;
}
```
</details>

---

### Problem 7: Next Greater Element II
**LeetCode 503** | **Difficulty: Medium** | **Time: 35 mins**

Given a circular array, return the next greater element for every element.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use monotonic stack with circular array simulation
2. Process array twice to handle circular nature
3. Use modulo operation for circular indexing

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public int[] nextGreaterElements(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Stack<Integer> stack = new Stack<>();
    
    for (int i = 0; i < 2 * n; i++) {
        while (!stack.isEmpty() && nums[i % n] > nums[stack.peek()]) {
            result[stack.pop()] = nums[i % n];
        }
        if (i < n) {
            stack.push(i);
        }
    }
    
    return result;
}
```
</details>

---

### Problem 8: Evaluate Reverse Polish Notation
**LeetCode 150** | **Difficulty: Medium** | **Time: 25 mins**

Evaluate the value of an arithmetic expression in Reverse Polish Notation.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use stack to store operands
2. When operator is encountered, pop two operands and apply operation
3. Push result back to stack

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public int evalRPN(String[] tokens) {
    Stack<Integer> stack = new Stack<>();
    
    for (String token : tokens) {
        if ("+-*/".contains(token)) {
            int b = stack.pop();
            int a = stack.pop();
            switch (token) {
                case "+": stack.push(a + b); break;
                case "-": stack.push(a - b); break;
                case "*": stack.push(a * b); break;
                case "/": stack.push(a / b); break;
            }
        } else {
            stack.push(Integer.parseInt(token));
        }
    }
    
    return stack.pop();
}
```
</details>

---

### Problem 9: Decode String
**LeetCode 394** | **Difficulty: Medium** | **Time: 40 mins**

Given an encoded string, return its decoded string. The encoding rule is: k[encoded_string].

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use two stacks: one for numbers, one for strings
2. Build current string and number as you iterate
3. When '[' is found, push to stacks; when ']' is found, pop and build result

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public String decodeString(String s) {
    Stack<Integer> numStack = new Stack<>();
    Stack<String> strStack = new Stack<>();
    StringBuilder currentStr = new StringBuilder();
    int num = 0;
    
    for (char c : s.toCharArray()) {
        if (Character.isDigit(c)) {
            num = num * 10 + (c - '0');
        } else if (c == '[') {
            numStack.push(num);
            strStack.push(currentStr.toString());
            currentStr = new StringBuilder();
            num = 0;
        } else if (c == ']') {
            int repeatTimes = numStack.pop();
            StringBuilder temp = new StringBuilder(strStack.pop());
            for (int i = 0; i < repeatTimes; i++) {
                temp.append(currentStr);
            }
            currentStr = temp;
        } else {
            currentStr.append(c);
        }
    }
    
    return currentStr.toString();
}
```
</details>

---

### Problem 10: Asteroid Collision
**LeetCode 735** | **Difficulty: Medium** | **Time: 35 mins**

Given an array asteroids of integers representing asteroids in a row, find out the state after all collisions.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use stack to track asteroids moving right
2. For left-moving asteroids, simulate collisions with right-moving ones
3. Handle different collision scenarios (destruction, survival)

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public int[] asteroidCollision(int[] asteroids) {
    Stack<Integer> stack = new Stack<>();
    
    for (int asteroid : asteroids) {
        boolean destroyed = false;
        
        while (!stack.isEmpty() && asteroid < 0 && stack.peek() > 0) {
            if (stack.peek() < -asteroid) {
                stack.pop();
            } else if (stack.peek() == -asteroid) {
                stack.pop();
                destroyed = true;
                break;
            } else {
                destroyed = true;
                break;
            }
        }
        
        if (!destroyed) {
            stack.push(asteroid);
        }
    }
    
    return stack.stream().mapToInt(i -> i).toArray();
}
```
</details>

---

## 🔴 Hard Problems

### Problem 11: Largest Rectangle in Histogram
**LeetCode 84** | **Difficulty: Hard** | **Time: 45 mins**

Given an array of integers heights representing the histogram's bar height, return the area of the largest rectangle.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use monotonic increasing stack to store indices
2. When a smaller height is found, calculate area for each popped height
3. The width is determined by the span between stack elements

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public int largestRectangleArea(int[] heights) {
    Stack<Integer> stack = new Stack<>();
    int maxArea = 0;
    int index = 0;
    
    while (index < heights.length) {
        if (stack.isEmpty() || heights[index] >= heights[stack.peek()]) {
            stack.push(index++);
        } else {
            int top = stack.pop();
            int area = heights[top] * (stack.isEmpty() ? index : index - stack.peek() - 1);
            maxArea = Math.max(maxArea, area);
        }
    }
    
    while (!stack.isEmpty()) {
        int top = stack.pop();
        int area = heights[top] * (stack.isEmpty() ? index : index - stack.peek() - 1);
        maxArea = Math.max(maxArea, area);
    }
    
    return maxArea;
}
```
</details>

---

### Problem 12: Maximal Rectangle
**LeetCode 85** | **Difficulty: Hard** | **Time: 50 mins**

Given a binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Convert to histogram problem for each row
2. Use largest rectangle in histogram algorithm
3. Update heights array for consecutive 1's

**Time Complexity:** O(m * n)  
**Space Complexity:** O(n)

**Java**
```java
public int maximalRectangle(char[][] matrix) {
    if (matrix.length == 0) return 0;
    
    int[] heights = new int[matrix[0].length];
    int maxArea = 0;
    
    for (char[] row : matrix) {
        for (int i = 0; i < row.length; i++) {
            heights[i] = row[i] == '1' ? heights[i] + 1 : 0;
        }
        maxArea = Math.max(maxArea, largestRectangleArea(heights));
    }
    
    return maxArea;
}

// Use the largestRectangleArea method from Problem 11
```
</details>

---

### Problem 13: Basic Calculator
**LeetCode 224** | **Difficulty: Hard** | **Time: 45 mins**

Given a string s representing a valid expression, implement a basic calculator to evaluate it.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use stack to handle parentheses and maintain state
2. Keep track of current number, result, and sign
3. Handle parentheses by saving current state to stack

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public int calculate(String s) {
    Stack<Integer> stack = new Stack<>();
    int result = 0;
    int number = 0;
    int sign = 1;
    
    for (char c : s.toCharArray()) {
        if (Character.isDigit(c)) {
            number = number * 10 + (c - '0');
        } else if (c == '+') {
            result += sign * number;
            number = 0;
            sign = 1;
        } else if (c == '-') {
            result += sign * number;
            number = 0;
            sign = -1;
        } else if (c == '(') {
            stack.push(result);
            stack.push(sign);
            sign = 1;
            result = 0;
        } else if (c == ')') {
            result += sign * number;
            number = 0;
            result *= stack.pop();    // sign
            result += stack.pop();    // result
        }
    }
    
    if (number != 0) result += sign * number;
    return result;
}
```
</details>

---

### Problem 14: Remove K Digits
**LeetCode 402** | **Difficulty: Medium-Hard** | **Time: 40 mins**

Given string num representing a non-negative integer and an integer k, remove k digits to make the smallest possible number.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use monotonic increasing stack
2. Remove larger digits when possible to minimize result
3. Handle edge cases (leading zeros, removing more digits)

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public String removeKdigits(String num, int k) {
    Stack<Character> stack = new Stack<>();
    
    for (char digit : num.toCharArray()) {
        while (!stack.isEmpty() && k > 0 && stack.peek() > digit) {
            stack.pop();
            k--;
        }
        stack.push(digit);
    }
    
    // Remove remaining k digits from the end
    while (k > 0) {
        stack.pop();
        k--;
    }
    
    // Build result
    StringBuilder result = new StringBuilder();
    while (!stack.isEmpty()) {
        result.append(stack.pop());
    }
    
    result.reverse();
    
    // Remove leading zeros
    while (result.length() > 1 && result.charAt(0) == '0') {
        result.deleteCharAt(0);
    }
    
    return result.length() == 0 ? "0" : result.toString();
}
```
</details>

---

### Problem 15: Trapping Rain Water (Stack Solution)
**LeetCode 42** | **Difficulty: Hard** | **Time: 40 mins**

Given n non-negative integers representing an elevation map, compute how much water can be trapped.

<details>
<summary><strong>Solution Approach</strong></summary>

**Algorithm:**
1. Use monotonic decreasing stack to store indices
2. When current height is greater than stack top, calculate trapped water
3. Water level is determined by minimum of left and right boundaries

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

**Java**
```java
public int trap(int[] height) {
    if (height.length == 0) return 0;
    
    Stack<Integer> stack = new Stack<>();
    int water = 0;
    
    for (int i = 0; i < height.length; i++) {
        while (!stack.isEmpty() && height[i] > height[stack.peek()]) {
            int top = stack.pop();
            if (stack.isEmpty()) break;
            
            int distance = i - stack.peek() - 1;
            int boundedHeight = Math.min(height[i], height[stack.peek()]) - height[top];
            water += distance * boundedHeight;
        }
        stack.push(i);
    }
    
    return water;
}
```
</details>

---

## Common Interview Patterns

- **Monotonic Stack**: For next greater/smaller element problems
- **Expression Evaluation**: Using stack for operators and operands
- **Parentheses Matching**: Stack for bracket validation
- **Undo Operations**: Stack for maintaining state history

## Common Mistakes

- Not checking if stack is empty before popping
- Forgetting to handle edge cases (empty stack, single element)
- Not considering the order of operations in calculations
- Missing the reverse operation when building result from stack

## Interview Tips

- Always check for empty stack before peek() or pop()
- Consider using monotonic stack for optimization problems
- Think about what information needs to be stored in the stack
- Practice implementing stack using arrays and linked lists

## Further Practice

- [LeetCode Stack Problems](https://leetcode.com/tag/stack/)
- [GeeksforGeeks Stack Practice](https://www.geeksforgeeks.org/stack-data-structure/)
- [InterviewBit Stack](https://www.interviewbit.com/courses/programming/topics/stacks-and-queues/)
