# 🔗 Linked Lists – Dynamic Data Storage
## What is a Linked List?
A linked list is a linear data structure where elements (nodes) are stored non-contiguously in memory. Each node contains two parts: data and a reference (or link) to the next node in the sequence.

```
Index:  0    1    2    3    4
Node:  [A] -> [B] -> [C] -> [D] -> [E]
         ↑     ↑     ↑     ↑     ↑
       'A'   'B'   'C'   'D'   'E'
```
In this representation, each node points to the next, forming a chain-like structure.

## Memory Layout
Unlike arrays, linked lists do not require contiguous memory locations. Each node is dynamically allocated and connected via pointers.
```
Memory Address: 1000  1001  1002  1003  1004
Node Values:    [A]   [B]   [C]   [D]   [E]
Next Pointer:   1001  1002  1003  1004  NULL
```
Here, each node contains data and a pointer to the next node's memory address. The last node points to NULL, indicating the end of the list.


## ⚙️ Characteristics
|Feature	|     Description     |    
|-----------------------|-------------|
|Dynamic Size           |	Size can grow or shrink at runtime without pre-allocation |
|Efficient Insert/Delete |	Insertion and deletion operations are efficient, especially at the beginning of the list (O(1)) |
|Sequential Access |	Nodes are accessed sequentially; direct access by index is not possible |
|Memory Usage |	Each node requires extra memory for storing the reference to the next node |
|Implementation |	Used to implement other data structures like stacks, queues, and deques |

## 📊 Common Operations and Time Complexities

| Operation                        | SLL       | DLL (w/ tail) | Space | Notes |
|----------------------------------|-----------|---------------|--------|-------|
| **Access (by index)**            | O(n)      | O(n)/O(n/2)   | O(1)   | Traversal required |
| **Search (by value)**            | O(n)      | O(n)          | O(1)   | Sequential search |
| **Insert at Head**               | O(1)      | O(1)          | O(1)   | Efficient insertion |
| **Insert at Tail**               | O(n) / O(1) | O(1)        | O(1)   | Efficient with tail pointer |
| **Insert After Known Node**      | O(1)      | O(1)          | O(1)   | Requires pointer to node |
| **Delete at Head**               | O(1)      | O(1)          | O(1)   | Simple pointer update |
| **Delete at Tail**               | O(n)      | O(1)          | O(1)   | DLL more efficient |
| **Delete by Value / Index**      | O(n)      | O(n)          | O(1)   | Need to locate node first |

---

## 💻 Basic Linked List Implementations

<details>
<summary>🐍 Python</summary>

```python
class ListNode:
    def __init__(self, val=0, next_node=None):
        self.val = val
        self.next = next_node

# 1 → 2 → 3
node3 = ListNode(3)
node2 = ListNode(2, node3)
head = ListNode(1, node2)

# Traversal:
# current = head
# while current:
#     print(current.val, end=" → ")
#     current = current.next
# print("None")
````

</details>

<details>
<summary>☕ Java</summary>

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
        this.next = null;
    }

    ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}
```

</details>

<details>
<summary>⚙️ C++</summary>

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode* nxt) : val(x), next(nxt) {}
};
```

</details>

---

## ✨ Popular Patterns & Algorithms

### 1. Cycle Detection – Fast & Slow Pointers 🐢🐇

<details>
<summary>🐍 Python</summary>

```python
def has_cycle(head):
    slow, fast = head, head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next
        if slow == fast:
            return True
    return False
```

</details>

---

### 2. Reverse a Linked List 🔄

<details>
<summary>🐍 Python (Iterative)</summary>

```python
def reverse_list(head):
    prev = None
    while head:
        next_node = head.next
        head.next = prev
        prev = head
        head = next_node
    return prev
```

</details>

---

### 3. Merge Two Sorted Lists 🤝

<details>
<summary>🐍 Python</summary>

```python
def merge_two_lists(l1, l2):
    dummy = ListNode(-1)
    current = dummy
    while l1 and l2:
        if l1.val < l2.val:
            current.next, l1 = l1, l1.next
        else:
            current.next, l2 = l2, l2.next
        current = current.next
    current.next = l1 or l2
    return dummy.next
```

</details>

---

## 🚀 Advanced Linked List Variants

* **Skip List**: Multi-level linked list for faster search (O(log n) avg).
* **Self-Organizing List**: Reorders nodes based on access frequency.
* **Unrolled List**: Stores multiple items per node to improve cache usage.
* **XOR Linked List**: Reduces memory by using XOR of prev and next addresses.

---

## ✅ Best Practices

### ✅ Do:

* Use **dummy nodes** to simplify head/tail insertions.
* **Visualize** pointer movements.
* Check for `null` before dereferencing.
* Cover edge cases: empty list, single node, cycle, head/tail deletion.
* Deallocate memory properly in C++.

### ❌ Don’t:

* Assume O(1) index access.
* Forget to update head/tail during modifications.
* Lose references during pointer updates.
* Skip `null` checks (risk of segmentation faults or exceptions).
* Ignore memory management in low-level languages.

---

## ⚡ Optimizations & Tips

* **Tail Pointer** for O(1) insertions at end.
* **Circular Lists** for round-robin structures.
* **Doubly Linked Lists** when backward traversal is needed.
* **Sentinel Nodes** reduce edge case complexity.

---

## 🆚 Linked List vs Array/Data Structures

| Feature                     | Linked List    | Array      | Dynamic Array (List/ArrayList) |
| --------------------------- | -------------- | ---------- | ------------------------------ |
| **Size**                    | Dynamic        | Fixed      | Dynamic (resizable)            |
| **Memory**                  | Non-contiguous | Contiguous | Contiguous                     |
| **Random Access**           | ❌ O(n)         | ✅ O(1)     | ✅ O(1) (avg)                   |
| **Insert/Delete at Middle** | O(n)           | O(n)       | O(n)                           |
| **Insert/Delete at Ends**   | ✅ O(1) head    | ❌ N/A      | ✅ O(1) (append only)           |
| **Cache Locality**          | Poor           | Excellent  | Good (unless resized)          |

---

## 📝 Summary

**When to Use Linked Lists:**

* When frequent insertions/deletions at unknown positions.
* When list size is unpredictable.
* To build queues, stacks, or adjacency lists.

**When Not to Use:**

* When frequent index-based access is needed.
* When memory overhead or poor locality matters.

---

## 📚 Next Topic

> **Stacks & Queues – Linear Data Structures** 📥📤

---

## 🧠 Practice Suggestions

Solve problems involving:

* Reverse a Linked List
* Cycle Detection
* Merge Sorted Lists
* Remove N-th Node from End
* Detect and Remove Loop
* Intersection of Two Linked Lists

👉 Platforms: **LeetCode**, **GeeksforGeeks**, **HackerRank**

---
