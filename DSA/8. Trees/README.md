# 🌳 Trees - Hierarchical Data Structures

Welcome to the **Trees** section! Master tree data structures and algorithms that form the backbone of many computer science applications.

---

## 📚 What is a Tree?

A **Tree** is a hierarchical data structure consisting of nodes connected by edges, with the following properties:
- **Root**: The top node with no parent
- **Leaf**: Nodes with no children
- **Height**: Longest path from root to leaf
- **Depth**: Distance from root to a specific node
- **Binary Tree**: Each node has at most 2 children

---

## 🏗️ Tree Types & Applications

### 🌿 Binary Tree
- Each node has at most 2 children (left and right)
- Used in: Expression parsing, Huffman coding

### 🔍 Binary Search Tree (BST)
- Left subtree < root < right subtree
- Used in: Searching, sorting, databases

### ⚖️ Balanced Trees
- **AVL Tree**: Self-balancing BST with height difference ≤ 1
- **Red-Black Tree**: Self-balancing with color properties
- Used in: Standard library implementations (TreeMap, TreeSet)

### 🎯 Specialized Trees
- **Trie**: Prefix tree for string operations
- **Segment Tree**: Range queries and updates
- **Fenwick Tree**: Efficient prefix sum operations
- **Heap**: Priority queue implementation

---

## 🔧 Basic Tree Operations

### Core Operations
| Operation | BST | Balanced Tree | Description |
|-----------|-----|---------------|-------------|
| **Search** | O(h) | O(log n) | Find element |
| **Insert** | O(h) | O(log n) | Add element |
| **Delete** | O(h) | O(log n) | Remove element |
| **Traversal** | O(n) | O(n) | Visit all nodes |

*h = height of tree (worst case O(n) for skewed tree)*

---

## 🚶 Tree Traversal Methods

### 1. Depth-First Search (DFS)

#### **Inorder (Left → Root → Right)**
```java
void inorder(TreeNode root) {
    if (root != null) {
        inorder(root.left);
        System.out.print(root.val + " ");
        inorder(root.right);
    }
}
```
**Use Case**: BST gives sorted order

#### **Preorder (Root → Left → Right)**
```java
void preorder(TreeNode root) {
    if (root != null) {
        System.out.print(root.val + " ");
        preorder(root.left);
        preorder(root.right);
    }
}
```
**Use Case**: Tree serialization, expression prefix

#### **Postorder (Left → Right → Root)**
```java
void postorder(TreeNode root) {
    if (root != null) {
        postorder(root.left);
        postorder(root.right);
        System.out.print(root.val + " ");
    }
}
```
**Use Case**: Tree deletion, expression postfix

### 2. Breadth-First Search (BFS)

#### **Level Order**
```java
List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    
    while (!queue.isEmpty()) {
        int size = queue.size();
        List<Integer> level = new ArrayList<>();
        
        for (int i = 0; i < size; i++) {
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

---

## 🏗️ Tree Implementation

### Basic Tree Node
```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    
    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```

### Binary Search Tree Operations
```java
class BST {
    private TreeNode root;
    
    public void insert(int val) {
        root = insertRec(root, val);
    }
    
    private TreeNode insertRec(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        
        if (val < root.val) {
            root.left = insertRec(root.left, val);
        } else if (val > root.val) {
            root.right = insertRec(root.right, val);
        }
        
        return root;
    }
    
    public boolean search(int val) {
        return searchRec(root, val);
    }
    
    private boolean searchRec(TreeNode root, int val) {
        if (root == null) return false;
        if (root.val == val) return true;
        
        return val < root.val ? 
            searchRec(root.left, val) : 
            searchRec(root.right, val);
    }
}
```

---

## 🧠 Common Tree Patterns

### 1. Tree Height/Depth
```java
int maxDepth(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

### 2. Path Sum Problems
```java
boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) {
        return root.val == targetSum;
    }
    
    return hasPathSum(root.left, targetSum - root.val) ||
           hasPathSum(root.right, targetSum - root.val);
}
```

### 3. Lowest Common Ancestor
```java
TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) {
        return root;
    }
    
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    
    if (left != null && right != null) return root;
    return left != null ? left : right;
}
```

### 4. Tree Serialization
```java
// Serialize tree to string
String serialize(TreeNode root) {
    StringBuilder sb = new StringBuilder();
    serializeHelper(root, sb);
    return sb.toString();
}

void serializeHelper(TreeNode root, StringBuilder sb) {
    if (root == null) {
        sb.append("null,");
        return;
    }
    
    sb.append(root.val).append(",");
    serializeHelper(root.left, sb);
    serializeHelper(root.right, sb);
}
```

---

## 🎯 Advanced Tree Concepts

### AVL Tree (Self-Balancing)
```java
class AVLNode {
    int val, height;
    AVLNode left, right;
    
    AVLNode(int val) {
        this.val = val;
        this.height = 1;
    }
}

class AVLTree {
    private int getHeight(AVLNode node) {
        return node == null ? 0 : node.height;
    }
    
    private int getBalance(AVLNode node) {
        return node == null ? 0 : getHeight(node.left) - getHeight(node.right);
    }
    
    private AVLNode rightRotate(AVLNode y) {
        AVLNode x = y.left;
        AVLNode T2 = x.right;
        
        x.right = y;
        y.left = T2;
        
        y.height = Math.max(getHeight(y.left), getHeight(y.right)) + 1;
        x.height = Math.max(getHeight(x.left), getHeight(x.right)) + 1;
        
        return x;
    }
}
```

### Trie (Prefix Tree)
```java
class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEndOfWord = false;
}

class Trie {
    private TrieNode root;
    
    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode current = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (current.children[index] == null) {
                current.children[index] = new TrieNode();
            }
            current = current.children[index];
        }
        current.isEndOfWord = true;
    }
    
    public boolean search(String word) {
        TrieNode node = searchNode(word);
        return node != null && node.isEndOfWord;
    }
    
    private TrieNode searchNode(String word) {
        TrieNode current = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (current.children[index] == null) {
                return null;
            }
            current = current.children[index];
        }
        return current;
    }
}
```

---

## 🌟 Real-World Applications

### 🗄️ Database Systems
- **B-Trees**: Database indexing
- **B+ Trees**: File systems
- **LSM Trees**: NoSQL databases

### 🌐 Web & Networking
- **DOM Tree**: HTML structure
- **Routing Tables**: Network routing
- **DNS Hierarchy**: Domain name resolution

### 🎮 Gaming & Graphics
- **Scene Graphs**: 3D rendering
- **Decision Trees**: AI game logic
- **Quad Trees**: Spatial partitioning

### 💻 System Design
- **File Systems**: Directory structure
- **Compiler Design**: Abstract syntax trees
- **Expression Evaluation**: Parse trees

---

## ⚡ Performance Analysis

### Time Complexities
| Tree Type | Search | Insert | Delete | Space |
|-----------|---------|---------|---------|-------|
| **Binary Tree** | O(n) | O(n) | O(n) | O(n) |
| **BST (Average)** | O(log n) | O(log n) | O(log n) | O(n) |
| **BST (Worst)** | O(n) | O(n) | O(n) | O(n) |
| **AVL Tree** | O(log n) | O(log n) | O(log n) | O(n) |
| **Red-Black** | O(log n) | O(log n) | O(log n) | O(n) |

### Space Complexities
- **Recursive algorithms**: O(h) stack space where h is height
- **Iterative with explicit stack**: O(h) additional space
- **Level-order traversal**: O(w) where w is maximum width

---

## 🚫 Common Mistakes & Pitfalls

### ❌ Recursion Issues
1. **Stack Overflow**: Deep recursion on skewed trees
2. **Base Case**: Forgetting null checks
3. **Return Values**: Not properly returning modified trees

### ❌ Tree Construction
1. **Memory Leaks**: Not properly deallocating nodes
2. **Dangling Pointers**: Incorrect parent-child relationships
3. **Balance Issues**: Not maintaining tree balance

### ✅ Best Practices
```java
// Always check for null
if (root == null) return someDefaultValue;

// Use iterative approach for deep trees
Stack<TreeNode> stack = new Stack<>();

// Consider using balanced trees for guaranteed performance
TreeMap<Integer, String> map = new TreeMap<>(); // Red-Black tree
```

---

## 🎯 Interview Preparation Strategy

### 🔥 Must-Know Problems
1. **Tree Traversals** (Inorder, Preorder, Postorder, Level-order)
2. **Maximum Depth** of binary tree
3. **Validate Binary Search Tree**
4. **Lowest Common Ancestor**
5. **Path Sum** problems
6. **Serialize and Deserialize** binary tree
7. **Binary Tree Maximum Path Sum**

### 💡 Key Concepts to Master
- **All traversal methods** (recursive and iterative)
- **BST properties** and validation
- **Tree construction** from traversals
- **Path and sum problems**
- **Tree modification** (invert, flatten, etc.)

### 🎤 Common Interview Questions
1. "Explain different tree traversal methods"
2. "When would you use a BST vs a hash table?"
3. "How do you detect if a binary tree is balanced?"
4. "Implement level-order traversal iteratively"
5. "Find all paths from root to leaf with given sum"

---

## 📈 Learning Path

### Week 1: Foundations
- **Day 1-2**: Tree concepts and basic operations
- **Day 3-4**: Tree traversal methods (all 4 types)
- **Day 5-7**: Practice basic tree problems

### Week 2: Binary Search Trees
- **Day 1-3**: BST operations and validation
- **Day 4-5**: BST construction and modification
- **Day 6-7**: Advanced BST problems

### Week 3: Advanced Topics
- **Day 1-3**: Balanced trees (AVL, Red-Black concepts)
- **Day 4-5**: Tries and specialized trees
- **Day 6-7**: Complex tree algorithms

---

## 🛠️ Built-in Tree Implementations

### Java
```java
// TreeMap (Red-Black Tree)
TreeMap<Integer, String> map = new TreeMap<>();
map.put(key, value);
map.get(key);
map.remove(key);

// TreeSet (Red-Black Tree)
TreeSet<Integer> set = new TreeSet<>();
set.add(value);
set.contains(value);
set.remove(value);
```

### Python
```python
# No built-in balanced tree, but can use:
import bisect

# For sorted list operations
sorted_list = []
bisect.insort(sorted_list, value)  # Insert in sorted order
index = bisect.bisect_left(sorted_list, value)  # Find position
```

### C++
```cpp
#include <set>
#include <map>

std::set<int> s;          // Red-Black Tree
std::map<int, string> m;  // Red-Black Tree

s.insert(value);
s.find(value);
s.erase(value);
```

---

## 📚 Additional Resources

### 📖 Reading Materials
- [Tree Visualization](https://visualgo.net/bst)
- [GeeksforGeeks Trees](https://www.geeksforgeeks.org/binary-tree-data-structure/)
- [Tree Algorithms MIT](https://ocw.mit.edu/courses/introduction-to-algorithms/)

### 🎥 Video Tutorials
- Tree traversal implementations
- BST operations and balancing
- Advanced tree algorithms
- Real-world tree applications

---

**Ready to solve tree problems?** Check out our comprehensive [Problems.md](./Problems.md) section! 🌳

**Next Topic**: [Graphs - Connected Data Structures](../9.%20Graphs/)