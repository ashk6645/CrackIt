# 🚀 Queues - First In First Out (FIFO) Data Structure

Welcome to the **Queues** section! Master the Queue data structure and its applications in solving real-world problems efficiently.

---

## 📚 What is a Queue?

A **Queue** is a linear data structure that follows the **First In First Out (FIFO)** principle. Think of it like a line of people waiting:
- The first person to join the line is the first to be served
- New people join at the **rear (back)** of the line
- People are served from the **front** of the line

---

## 🔧 Basic Queue Operations

### Core Operations
| Operation | Description | Time Complexity |
|-----------|-------------|-----------------|
| **enqueue(item)** | Add item to rear of queue | O(1) |
| **dequeue()** | Remove item from front of queue | O(1) |
| **front()** | Get front item without removing | O(1) |
| **isEmpty()** | Check if queue is empty | O(1) |
| **size()** | Get number of elements | O(1) |

### Additional Operations
| Operation | Description | Time Complexity |
|-----------|-------------|-----------------|
| **rear()** | Get rear item without removing | O(1) |
| **isFull()** | Check if queue is full (for bounded queues) | O(1) |

---

## 🏗️ Queue Implementation Methods

### 1. Array-Based Implementation
```java
class ArrayQueue {
    private int[] queue;
    private int front, rear, size, capacity;
    
    public ArrayQueue(int capacity) {
        this.capacity = capacity;
        this.queue = new int[capacity];
        this.front = 0;
        this.rear = -1;
        this.size = 0;
    }
    
    public void enqueue(int item) {
        if (size == capacity) throw new RuntimeException("Queue is full");
        rear = (rear + 1) % capacity;
        queue[rear] = item;
        size++;
    }
    
    public int dequeue() {
        if (isEmpty()) throw new RuntimeException("Queue is empty");
        int item = queue[front];
        front = (front + 1) % capacity;
        size--;
        return item;
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
}
```

### 2. Linked List Implementation
```java
class ListQueue {
    private Node front, rear;
    private int size;
    
    private class Node {
        int data;
        Node next;
        Node(int data) { this.data = data; }
    }
    
    public void enqueue(int item) {
        Node newNode = new Node(item);
        if (rear == null) {
            front = rear = newNode;
        } else {
            rear.next = newNode;
            rear = newNode;
        }
        size++;
    }
    
    public int dequeue() {
        if (isEmpty()) throw new RuntimeException("Queue is empty");
        int item = front.data;
        front = front.next;
        if (front == null) rear = null;
        size--;
        return item;
    }
    
    public boolean isEmpty() {
        return front == null;
    }
}
```

---

## 🌟 Types of Queues

### 1. Simple Queue (Linear Queue)
- Basic FIFO queue
- Fixed size with front and rear pointers

### 2. Circular Queue
- Rear wraps around to front when end is reached
- Better space utilization than linear queue

### 3. Priority Queue
- Elements have priorities
- Higher priority elements dequeued first
- Implemented using heaps

### 4. Double-ended Queue (Deque)
- Insertion and deletion at both ends
- Combines stack and queue operations

### 5. Blocking Queue
- Thread-safe queue for concurrent programming
- Blocks when full (enqueue) or empty (dequeue)

---

## 🎯 Real-World Applications

### 🖥️ Operating Systems
- **Process Scheduling**: Ready queue for CPU scheduling
- **Buffer Management**: I/O buffering
- **Print Spooling**: Managing print jobs

### 🌐 Networking
- **Packet Routing**: Network packet queues
- **Load Balancing**: Request distribution
- **Bandwidth Management**: Traffic shaping

### 🎮 Gaming & Simulation
- **Event Handling**: Game event queues
- **Animation**: Frame buffers
- **AI Pathfinding**: BFS traversal

### 💻 Software Development
- **Asynchronous Processing**: Task queues
- **Caching**: LRU cache implementation
- **Web Servers**: Request handling

---

## 🧠 Problem-Solving Patterns

### 1. Level-order Traversal
**Use Case**: Tree/Graph BFS traversal
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

### 2. Sliding Window Maximum
**Use Case**: Finding maximum in sliding windows
```java
public int[] maxSlidingWindow(int[] nums, int k) {
    Deque<Integer> deque = new ArrayDeque<>();
    int[] result = new int[nums.length - k + 1];
    
    for (int i = 0; i < nums.length; i++) {
        // Remove elements outside window
        while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
            deque.pollFirst();
        }
        
        // Remove smaller elements
        while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
            deque.pollLast();
        }
        
        deque.offerLast(i);
        
        if (i >= k - 1) {
            result[i - k + 1] = nums[deque.peekFirst()];
        }
    }
    
    return result;
}
```

### 3. First Non-repeating Character in Stream
**Use Case**: Processing data streams
```java
class FirstUnique {
    private Queue<Integer> queue;
    private Map<Integer, Integer> count;
    
    public FirstUnique(int[] nums) {
        queue = new LinkedList<>();
        count = new HashMap<>();
        for (int num : nums) {
            add(num);
        }
    }
    
    public int showFirstUnique() {
        while (!queue.isEmpty() && count.get(queue.peek()) > 1) {
            queue.poll();
        }
        return queue.isEmpty() ? -1 : queue.peek();
    }
    
    public void add(int value) {
        count.put(value, count.getOrDefault(value, 0) + 1);
        if (count.get(value) == 1) {
            queue.offer(value);
        }
    }
}
```

---

## ⚡ Performance Comparison

### Time Complexities
| Implementation | Enqueue | Dequeue | Front | Space |
|----------------|---------|---------|-------|-------|
| Array (Circular) | O(1) | O(1) | O(1) | O(n) |
| Linked List | O(1) | O(1) | O(1) | O(n) |
| Priority Queue | O(log n) | O(log n) | O(1) | O(n) |

### Space Complexities
- **Array Implementation**: O(n) fixed space
- **Linked List**: O(n) dynamic space
- **Priority Queue**: O(n) heap space

---

## 🚫 Common Mistakes & Pitfalls

### ❌ Array Implementation Issues
1. **Not using circular indexing** - leads to false "queue full" condition
2. **Incorrect front/rear pointer updates** - causes memory leaks or corruption
3. **Not checking bounds** - array overflow/underflow

### ❌ General Queue Mistakes
1. **Dequeue from empty queue** - always check isEmpty() first
2. **Mixing up front/rear operations** - remember FIFO principle
3. **Memory leaks in linked implementation** - properly manage node references

### ✅ Best Practices
```java
// Always check before dequeue
if (!queue.isEmpty()) {
    int item = queue.dequeue();
}

// Use exception handling
try {
    int item = queue.dequeue();
} catch (QueueEmptyException e) {
    // Handle empty queue
}

// Prefer built-in implementations
Queue<Integer> queue = new LinkedList<>();
Queue<Integer> queue = new ArrayDeque<>();
```

---

## 🛠️ Built-in Queue Implementations

### Java
```java
// Interface
Queue<Integer> queue = new LinkedList<>();
Queue<Integer> queue = new ArrayDeque<>();
Queue<Integer> queue = new PriorityQueue<>();

// Methods
queue.offer(item);    // enqueue
queue.poll();         // dequeue
queue.peek();         // front
queue.isEmpty();      // check empty
```

### Python
```python
from collections import deque
from queue import Queue, PriorityQueue

# Built-in implementations
queue = deque()           # Double-ended queue
queue = Queue()           # Thread-safe queue
queue = PriorityQueue()   # Priority queue

# Methods
queue.append(item)        # enqueue
queue.popleft()          # dequeue
queue[0]                 # front (for deque)
```

### C++
```cpp
#include <queue>

std::queue<int> q;
std::priority_queue<int> pq;
std::deque<int> dq;

// Methods
q.push(item);    // enqueue
q.pop();         // dequeue
q.front();       // front
q.empty();       // check empty
```

---

## 🎯 Interview Preparation Tips

### 🔥 Must-Know Problems
1. **Implement Queue using Stacks** (LeetCode 232)
2. **Implement Stack using Queues** (LeetCode 225)
3. **Sliding Window Maximum** (LeetCode 239)
4. **Design Circular Queue** (LeetCode 622)
5. **Number of Recent Calls** (LeetCode 933)

### 💡 Key Concepts to Master
- **FIFO principle** and when to use queues
- **Different queue implementations** and their trade-offs
- **Queue vs Stack** - when to use which
- **BFS traversal** using queues
- **Priority queues** and heap operations

### 🎤 Common Interview Questions
1. "Explain the difference between stack and queue"
2. "When would you use a queue over other data structures?"
3. "How do you implement a queue using arrays efficiently?"
4. "What are the applications of queues in real systems?"
5. "How do you detect if a queue is empty or full?"

---

## 🧪 Practice Problems Overview

### 🟢 Easy Level
- Queue implementation basics
- Simple BFS problems
- Basic queue operations

### 🟡 Medium Level
- Sliding window problems
- Multi-level BFS
- Queue with additional constraints

### 🔴 Hard Level
- Complex queue-based algorithms
- Multiple queue coordination
- Optimization problems

---

## 📈 Learning Path

### Week 1: Fundamentals
- **Day 1-2**: Queue concepts and basic operations
- **Day 3-4**: Array and linked list implementations
- **Day 5-7**: Practice basic queue problems

### Week 2: Applications
- **Day 1-3**: BFS traversal and level-order problems
- **Day 4-5**: Priority queues and heaps
- **Day 6-7**: Double-ended queues (deque)

### Week 3: Advanced Topics
- **Day 1-3**: Sliding window problems with queues
- **Day 4-5**: Queue-based system design
- **Day 6-7**: Interview problem practice

---

## 🔗 Additional Resources

### 📚 Reading Materials
- [GeeksforGeeks Queue Tutorial](https://www.geeksforgeeks.org/queue-data-structure/)
- [Visualgo Queue Visualization](https://visualgo.net/queue)
- [Khan Academy Queues](https://www.khanacademy.org/computing/computer-science/algorithms/intro-to-algorithms/a/intro-to-queues)

### 🎥 Video Tutorials
- Queue implementation walkthroughs
- BFS traversal tutorials
- Priority queue explanations
- Real-world queue applications

### 💻 Practice Platforms
- [LeetCode Queue Problems](https://leetcode.com/tag/queue/)
- [HackerRank Queue Challenges](https://www.hackerrank.com/domains/data-structures/queues)
- [InterviewBit Queue Section](https://www.interviewbit.com/courses/programming/topics/queues/)

---

## 🎉 Fun Facts About Queues

🎭 **Etymology**: "Queue" comes from French, meaning "tail"

🏪 **Everyday Queues**: Supermarket checkout, traffic lights, printer queues

⚡ **Performance**: Modern CPUs use instruction queues for optimization

🌐 **Internet**: Web servers use request queues to handle traffic

🎮 **Gaming**: Message queues handle multiplayer game events

---

**Ready to dive deep into queue problems?** Check out our comprehensive [Problems.md](./Problems.md) section! 🚀

**Next Topic**: [Trees - Hierarchical Data Structures](../8.%20Trees/)