# 📝 Linked List Problems - Practice Set

## Problem Categories

### 🟢 Easy Problems (5 problems)
### 🟡 Medium Problems (5 problems)
### 🔴 Hard Problems (5 problems)

---

## 🟢 Easy Problems

### Problem 1: Reverse Linked List
**Difficulty**: Easy  
**Pattern**: Reversal

**Problem**: Reverse a singly linked list.

**Example**:
```
Input: 1 -> 2 -> 3 -> 4 -> 5
Output: 5 -> 4 -> 3 -> 2 -> 1
```

<details>
<summary>💡 Hint</summary>
Iteratively change next pointers.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def reverse_list(head):
    prev = None
    curr = head
    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node
    return prev
```

**Java**
```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

**C++**
```cpp
ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;
    while (curr) {
        ListNode* next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```
</details>

---

### Problem 2: Detect Cycle in Linked List
**Difficulty**: Easy  
**Pattern**: Fast & Slow Pointers

**Problem**: Check if a linked list has a cycle.

**Example**:
```
Input: 1 -> 2 -> 3 -> 4 -> 2 (cycle)
Output: True
```

<details>
<summary>💡 Hint</summary>
Use two pointers moving at different speeds.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

**Java**
```java
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;
    }
    return false;
}
```

**C++**
```cpp
bool hasCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;
    }
    return false;
}
```
</details>

---

### Problem 3: Merge Two Sorted Lists
**Difficulty**: Easy  
**Pattern**: Merge

**Problem**: Merge two sorted linked lists into one sorted list.

**Example**:
```
Input: 1 -> 2 -> 4, 1 -> 3 -> 4
Output: 1 -> 1 -> 2 -> 3 -> 4 -> 4
```

<details>
<summary>💡 Hint</summary>
Use a dummy node and compare values.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def merge_two_lists(l1, l2):
    dummy = ListNode()
    tail = dummy
    while l1 and l2:
        if l1.val < l2.val:
            tail.next = l1
            l1 = l1.next
        else:
            tail.next = l2
            l2 = l2.next
        tail = tail.next
    tail.next = l1 or l2
    return dummy.next
```

**Java**
```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode tail = dummy;
    while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
            tail.next = l1;
            l1 = l1.next;
        } else {
            tail.next = l2;
            l2 = l2.next;
        }
        tail = tail.next;
    }
    tail.next = (l1 != null) ? l1 : l2;
    return dummy.next;
}
```

**C++**
```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode* tail = &dummy;
    while (l1 && l2) {
        if (l1->val < l2->val) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }
    tail->next = l1 ? l1 : l2;
    return dummy.next;
}
```
</details>

---

### Problem 4: Remove Nth Node From End
**Difficulty**: Easy  
**Pattern**: Two Pointers

**Problem**: Remove the nth node from the end of a linked list.

**Example**:
```
Input: 1 -> 2 -> 3 -> 4 -> 5, n = 2
Output: 1 -> 2 -> 3 -> 5
```

<details>
<summary>💡 Hint</summary>
Use two pointers with a gap of n nodes.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def remove_nth_from_end(head, n):
    dummy = ListNode(0, head)
    first = second = dummy
    for _ in range(n + 1):
        first = first.next
    while first:
        first = first.next
        second = second.next
    second.next = second.next.next
    return dummy.next
```

**Java**
```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0, head);
    ListNode first = dummy, second = dummy;
    for (int i = 0; i <= n; i++) first = first.next;
    while (first != null) {
        first = first.next;
        second = second.next;
    }
    second.next = second.next.next;
    return dummy.next;
}
```

**C++**
```cpp
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode dummy(0);
    dummy.next = head;
    ListNode* first = &dummy;
    ListNode* second = &dummy;
    for (int i = 0; i <= n; ++i) first = first->next;
    while (first) {
        first = first->next;
        second = second->next;
    }
    second->next = second->next->next;
    return dummy.next;
}
```
</details>

---

### Problem 5: Find Middle of Linked List
**Difficulty**: Easy  
**Pattern**: Fast & Slow Pointers

**Problem**: Find the middle node of a linked list.

**Example**:
```
Input: 1 -> 2 -> 3 -> 4 -> 5
Output: 3
```

<details>
<summary>💡 Hint</summary>
Use fast and slow pointers.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def middle_node(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```

**Java**
```java
public ListNode middleNode(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```

**C++**
```cpp
ListNode* middleNode(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}
```
</details>

---

## 🟡 Medium Problems

### Problem 6: Add Two Numbers
**Difficulty**: Medium  
**Pattern**: Linked List Math

**Problem**: Add two numbers represented by linked lists.

**Example**:
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
```

<details>
<summary>💡 Hint</summary>
Simulate addition with carry.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def add_two_numbers(l1, l2):
    dummy = ListNode()
    curr = dummy
    carry = 0
    while l1 or l2 or carry:
        val1 = l1.val if l1 else 0
        val2 = l2.val if l2 else 0
        total = val1 + val2 + carry
        carry = total // 10
        curr.next = ListNode(total % 10)
        curr = curr.next
        l1 = l1.next if l1 else None
        l2 = l2.next if l2 else None
    return dummy.next
```

**Java**
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    int carry = 0;
    while (l1 != null || l2 != null || carry != 0) {
        int val1 = (l1 != null) ? l1.val : 0;
        int val2 = (l2 != null) ? l2.val : 0;
        int sum = val1 + val2 + carry;
        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
        if (l1 != null) l1 = l1.next;
        if (l2 != null) l2 = l2.next;
    }
    return dummy.next;
}
```

**C++**
```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode* curr = &dummy;
    int carry = 0;
    while (l1 || l2 || carry) {
        int val1 = (l1) ? l1->val : 0;
        int val2 = (l2) ? l2->val : 0;
        int sum = val1 + val2 + carry;
        carry = sum / 10;
        curr->next = new ListNode(sum % 10);
        curr = curr->next;
        if (l1) l1 = l1->next;
        if (l2) l2 = l2->next;
    }
    return dummy.next;
}
```
</details>

---

### Problem 7: Intersection of Two Linked Lists
**Difficulty**: Medium  
**Pattern**: Two Pointers

**Problem**: Find the node where two linked lists intersect.

**Example**:
```
Input: A = 4 -> 1 -> 8 -> 4 -> 5, B = 5 -> 6 -> 1 -> 8 -> 4 -> 5
Output: 8
```

<details>
<summary>💡 Hint</summary>
Traverse both lists, switch heads when reaching end.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def get_intersection_node(headA, headB):
    a, b = headA, headB
    while a != b:
        a = a.next if a else headB
        b = b.next if b else headA
    return a
```

**Java**
```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    ListNode a = headA, b = headB;
    while (a != b) {
        a = (a != null) ? a.next : headB;
        b = (b != null) ? b.next : headA;
    }
    return a;
}
```

**C++**
```cpp
ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) {
    ListNode* a = headA;
    ListNode* b = headB;
    while (a != b) {
        a = (a != nullptr) ? a->next : headB;
        b = (b != nullptr) ? b->next : headA;
    }
    return a;
}
```
</details>

---

### Problem 8: Remove Duplicates from Sorted List
**Difficulty**: Medium  
**Pattern**: Pointer Manipulation

**Problem**: Remove duplicates from a sorted linked list.

**Example**:
```
Input: 1 -> 1 -> 2 -> 3 -> 3
Output: 1 -> 2 -> 3
```

<details>
<summary>💡 Hint</summary>
Iterate and skip duplicate nodes.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def delete_duplicates(head):
    curr = head
    while curr and curr.next:
        if curr.val == curr.next.val:
            curr.next = curr.next.next
        else:
            curr = curr.next
    return head
```

**Java**
```java
public ListNode deleteDuplicates(ListNode head) {
    ListNode curr = head;
    while (curr != null && curr.next != null) {
        if (curr.val == curr.next.val) {
            curr.next = curr.next.next;
        } else {
            curr = curr.next;
        }
    }
    return head;
}
```

**C++**
```cpp
ListNode* deleteDuplicates(ListNode* head) {
    ListNode* curr = head;
    while (curr && curr->next) {
        if (curr->val == curr->next->val) {
            curr->next = curr->next->next;
        } else {
            curr = curr->next;
        }
    }
    return head;
}
```
</details>

---

### Problem 9: Odd Even Linked List
**Difficulty**: Medium  
**Pattern**: Pointer Manipulation

**Problem**: Group all odd nodes together followed by even nodes.

**Example**:
```
Input: 1 -> 2 -> 3 -> 4 -> 5
Output: 1 -> 3 -> 5 -> 2 -> 4
```

<details>
<summary>💡 Hint</summary>
Use two pointers for odd and even positions.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def odd_even_list(head):
    if not head:
        return None
    odd, even = head, head.next
    even_head = even
    while even and even.next:
        odd.next = even.next
        odd = odd.next
        even.next = odd.next
        even = even.next
    odd.next = even_head
    return head
```

**Java**
```java
public ListNode oddEvenList(ListNode head) {
    if (head == null) return null;
    ListNode odd = head, even = head.next, evenHead = even;
    while (even != null && even.next != null) {
        odd.next = even.next;
        odd = odd.next;
        even.next = odd.next;
        even = even.next;
    }
    odd.next = evenHead;
    return head;
}
```

**C++**
```cpp
ListNode* oddEvenList(ListNode* head) {
    if (!head) return nullptr;
    ListNode* odd = head;
    ListNode* even = head->next;
    ListNode* evenHead = even;
    while (even && even->next) {
        odd->next = even->next;
        odd = odd->next;
        even->next = odd->next;
        even = even->next;
    }
    odd->next = evenHead;
    return head;
}
```
</details>

---

### Problem 10: Rotate List
**Difficulty**: Medium  
**Pattern**: Pointer Manipulation

**Problem**: Rotate the list to the right by k places.

**Example**:
```
Input: 1 -> 2 -> 3 -> 4 -> 5, k = 2
Output: 4 -> 5 -> 1 -> 2 -> 3
```

<details>
<summary>💡 Hint</summary>
Connect the list into a ring, then break at the right place.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def rotate_right(head, k):
    if not head or not head.next or k == 0:
        return head
    # Compute length and connect tail to head
    old_tail = head
    length = 1
    while old_tail.next:
        old_tail = old_tail.next
        length += 1
    old_tail.next = head
    # Find new tail and new head
    k = k % length
    new_tail = head
    for _ in range(length - k - 1):
        new_tail = new_tail.next
    new_head = new_tail.next
    new_tail.next = None
    return new_head
```

**Java**
```java
public ListNode rotateRight(ListNode head, int k) {
    if (head == null || head.next == null || k == 0) return head;
    // Compute the length of the list
    ListNode oldTail = head;
    int length = 1;
    while (oldTail.next != null) {
        oldTail = oldTail.next;
        length++;
    }
    oldTail.next = head; // Connect tail to head to make it circular
    // Find the new tail: (length - k % length - 1)th node
    int newTailIndex = length - k % length - 1;
    ListNode newTail = head;
    for (int i = 0; i < newTailIndex; i++) {
        newTail = newTail.next;
    }
    ListNode newHead = newTail.next;
    newTail.next = null; // Break the cycle
    return newHead;
}
```

**C++**
```cpp
ListNode* rotateRight(ListNode* head, int k) {
    if (!head || !head->next || k == 0) return head;
    // Compute the length and connect tail to head
    ListNode* oldTail = head;
    int length = 1;
    while (oldTail->next) {
        oldTail = oldTail->next;
        length++;
    }
    oldTail->next = head;
    // Find new tail and new head
    k = k % length;
    ListNode* newTail = head;
    for (int i = 0; i < length - k - 1; i++) {
        newTail = newTail->next;
    }
    ListNode* newHead = newTail->next;
    newTail->next = nullptr;
    return newHead;
}
```
</details>

---

## 🔴 Hard Problems

### Problem 11: Reverse Nodes in k-Group
**Difficulty**: Hard  
**Pattern**: Reversal

**Problem**: Reverse nodes of a linked list k at a time.

**Example**:
```
Input: 1 -> 2 -> 3 -> 4 -> 5, k = 2
Output: 2 -> 1 -> 4 -> 3 -> 5
```

<details>
<summary>💡 Hint</summary>
Reverse k nodes at a time recursively or iteratively.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def reverse_k_group(head, k):
    count = 0
    node = head
    while node and count < k:
        node = node.next
        count += 1
    if count == k:
        prev = self.reverse_k_group(node, k)
        while count > 0:
            temp = head.next
            head.next = prev
            prev = head
            head = temp
            count -= 1
        head = prev
    return head
```

**Java**
```java
public ListNode reverseKGroup(ListNode head, int k) {
    ListNode curr = head;
    int count = 0;
    // Count the number of nodes in the list
    while (curr != null && count < k) {
        curr = curr.next;
        count++;
    }
    // If we have k nodes, then we reverse them
    if (count == k) {
        curr = reverseKGroup(curr, k); // Reverse the rest of the list
        while (count-- > 0) {
            ListNode temp = head.next;
            head.next = curr;
            curr = head;
            head = temp;
        }
        head = curr;
    }
    return head;
}
```

**C++**
```cpp
ListNode* reverseKGroup(ListNode* head, int k) {
    ListNode* curr = head;
    int count = 0;
    // Count the number of nodes in the list
    while (curr && count < k) {
        curr = curr->next;
        count++;
    }
    // If we have k nodes, then we reverse them
    if (count == k) {
        curr = reverseKGroup(curr, k); // Reverse the rest of the list
        while (count-- > 0) {
            ListNode* temp = head->next;
            head->next = curr;
            curr = head;
            head = temp;
        }
        head = curr;
    }
    return head;
}
```
</details>

---

### Problem 12: Copy List with Random Pointer
**Difficulty**: Hard  
**Pattern**: Hash Map

**Problem**: Copy a linked list with next and random pointers.

**Example**:
```
Input: Node with random pointers
Output: Deep copy of the list
```

<details>
<summary>💡 Hint</summary>
Use a hash map to map original to copied nodes.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def copy_random_list(head):
    if not head:
        return None
    old_to_new = {}
    curr = head
    while curr:
        old_to_new[curr] = ListNode(curr.val)
        curr = curr.next
    curr = head
    while curr:
        old_to_new[curr].next = old_to_new.get(curr.next)
        old_to_new[curr].random = old_to_new.get(curr.random)
        curr = curr.next
    return old_to_new[head]
```

**Java**
```java
public Node copyRandomList(Node head) {
    if (head == null) return null;
    Map<Node, Node> oldToNew = new HashMap<>();
    Node curr = head;
    // First pass: create all nodes
    while (curr != null) {
        oldToNew.put(curr, new Node(curr.val));
        curr = curr.next;
    }
    curr = head;
    // Second pass: assign next and random pointers
    while (curr != null) {
        Node newCurr = oldToNew.get(curr);
        newCurr.next = oldToNew.get(curr.next);
        newCurr.random = oldToNew.get(curr.random);
        curr = curr.next;
    }
    return oldToNew.get(head);
}
```

**C++**
```cpp
Node* copyRandomList(Node* head) {
    if (!head) return nullptr;
    unordered_map<Node*, Node*> oldToNew;
    Node* curr = head;
    // First pass: create all nodes
    while (curr) {
        oldToNew[curr] = new Node(curr->val);
        curr = curr->next;
    }
    curr = head;
    // Second pass: assign next and random pointers
    while (curr) {
        Node* newCurr = oldToNew[curr];
        newCurr->next = oldToNew[curr->next];
        newCurr->random = oldToNew[curr->random];
        curr = curr->next;
    }
    return oldToNew[head];
}
```
</details>

---

### Problem 13: LRU Cache
**Difficulty**: Hard  
**Pattern**: Doubly Linked List, Hash Map

**Problem**: Design a data structure for LRU cache.

**Example**:
```
Input: put(1,1), put(2,2), get(1), put(3,3), get(2)
Output: 1, -1
```

<details>
<summary>💡 Hint</summary>
Use doubly linked list and hash map for O(1) operations.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
class LRUCache:
    def __init__(self, capacity: int):
        self.cache = {}
        self.capacity = capacity
        self.order = DoublyLinkedList()
    def get(self, key: int) -> int:
        # Implementation omitted for brevity
        pass
    def put(self, key: int, value: int) -> None:
        # Implementation omitted for brevity
        pass
```
</details>

---

### Problem 14: Merge k Sorted Lists
**Difficulty**: Hard  
**Pattern**: Heap, Linked List

**Problem**: Merge k sorted linked lists into one sorted list.

**Example**:
```
Input: [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
```

<details>
<summary>💡 Hint</summary>
Use a min-heap to efficiently get the smallest node.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def merge_k_lists(lists):
    import heapq
    heap = []
    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))
    dummy = ListNode()
    curr = dummy
    while heap:
        val, i, node = heapq.heappop(heap)
        curr.next = node
        curr = curr.next
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))
    return dummy.next
```

**Java**
```java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> minHeap = new PriorityQueue<>(Comparator.comparingInt(node -> node.val));
    for (ListNode node : lists) {
        if (node != null) minHeap.offer(node);
    }
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    while (!minHeap.isEmpty()) {
        curr.next = minHeap.poll();
        curr = curr.next;
        if (curr.next != null) {
            minHeap.offer(curr.next);
        }
    }
    return dummy.next;
}
```

**C++**
```cpp
ListNode* mergeKLists(vector<ListNode*>& lists) {
    auto cmp = [](ListNode* a, ListNode* b) { return a->val > b->val; };
    priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> minHeap(cmp);
    for (auto node : lists) {
        if (node) minHeap.push(node);
    }
    ListNode dummy(0);
    ListNode* curr = &dummy;
    while (!minHeap.empty()) {
        curr->next = minHeap.top();
        curr = curr->next;
        minHeap.pop();
        if (curr->next) {
            minHeap.push(curr->next);
        }
    }
    return dummy.next;
}
```
</details>

---

### Problem 15: Linked List Cycle II
**Difficulty**: Hard  
**Pattern**: Fast & Slow Pointers

**Problem**: Find the node where the cycle begins in a linked list.

**Example**:
```
Input: 3 -> 2 -> 0 -> -4 (cycle at 2)
Output: Node with value 2
```

<details>
<summary>💡 Hint</summary>
Use fast and slow pointers, then reset one pointer to head.
</details>

<details>
<summary>✅ Solution (Toggle for Python/Java/C++)</summary>

**Python**
```python
def detect_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break
    else:
        return None
    slow = head
    while slow != fast:
        slow = slow.next
        fast = fast.next
    return slow
```

**Java**
```java
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) {
            ListNode ptr = head;
            while (ptr != slow) {
                ptr = ptr.next;
                slow = slow.next;
            }
            return ptr;
        }
    }
    return null;
}
```

**C++**
```cpp
ListNode* detectCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) {
            ListNode* ptr = head;
            while (ptr != slow) {
                ptr = ptr->next;
                slow = slow->next;
            }
            return ptr;
        }
    }
    return nullptr;
}
```
</details>
