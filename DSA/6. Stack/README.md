# 6. Stacks

## What is a Stack?
A **stack** is a linear data structure that follows the Last-In-First-Out (LIFO) principle. The element added last is the first one to be removed.

## Applications
- Undo operations in editors
- Backtracking (e.g., browser history)
- Expression evaluation and syntax parsing
- Function call stack in recursion

## Stack Operations
- **Push**: Add an item to the top
- **Pop**: Remove the top item
- **Peek/Top**: View the top item
- **isEmpty**: Check if stack is empty

## Stack Implementation

### 1. Array-based Stack

#### C++
```cpp
class Stack {
    int top;
    int arr[1000];
public:
    Stack() { top = -1; }
    bool push(int x) {
        if (top >= 999) return false;
        arr[++top] = x;
        return true;
    }
    int pop() {
        if (top < 0) return -1;
        return arr[top--];
    }
    int peek() {
        if (top < 0) return -1;
        return arr[top];
    }
    bool isEmpty() { return top < 0; }
};
```

#### Python
```python
class Stack:
    def __init__(self):
        self.items = []
    def push(self, item):
        self.items.append(item)
    def pop(self):
        return self.items.pop() if not self.isEmpty() else None
    def peek(self):
        return self.items[-1] if not self.isEmpty() else None
    def isEmpty(self):
        return len(self.items) == 0
```

#### Java
```java
import java.util.*;
class StackDemo {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        stack.push(10);
        stack.push(20);
        System.out.println(stack.pop()); // 20
    }
}
```

### 2. Linked-list-based Stack

#### Python
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class StackLL:
    def __init__(self):
        self.head = None
    def push(self, data):
        node = Node(data)
        node.next = self.head
        self.head = node
    def pop(self):
        if self.head is None:
            return None
        data = self.head.data
        self.head = self.head.next
        return data
```

## Time and Space Complexity
- Push/Pop/Peek: O(1)
- Space: O(n) (where n is the number of elements)

## Further Reading
- [Stack Wikipedia](https://en.wikipedia.org/wiki/Stack_(abstract_data_type))
