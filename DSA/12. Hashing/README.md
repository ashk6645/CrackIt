# 🗂️ Hashing - Fast Data Access & Retrieval

Welcome to the **Hashing** section! Master hash tables, hash functions, and collision resolution techniques for efficient data storage and retrieval.

---

## 📚 What is Hashing?

**Hashing** is a technique that transforms data into a fixed-size value (hash) using a hash function, enabling O(1) average-case access to data stored in hash tables.

**Key Components**:
- **Hash Function**: Maps keys to array indices
- **Hash Table**: Array that stores key-value pairs
- **Collision**: When different keys map to same index
- **Load Factor**: Ratio of stored elements to table size

---

## 🔧 Hash Functions

### 1. Division Method
```java
public int hash(int key, int tableSize) {
    return key % tableSize;
}
```
**Best for**: Prime table sizes, uniformly distributed keys

### 2. Multiplication Method
```java
public int hash(int key, int tableSize) {
    double A = 0.6180339887; // (√5 - 1) / 2
    return (int) (tableSize * ((key * A) % 1));
}
```
**Best for**: Any table size, good distribution

### 3. String Hashing
```java
public int hash(String key, int tableSize) {
    int hash = 0;
    int prime = 31;
    
    for (char c : key.toCharArray()) {
        hash = (hash * prime + c) % tableSize;
    }
    
    return Math.abs(hash);
}
```

### 4. Rolling Hash (Rabin-Karp)
```java
public class RollingHash {
    private static final int BASE = 256;
    private static final int MOD = 101;
    
    public int computeHash(String str, int len) {
        int hash = 0;
        for (int i = 0; i < len; i++) {
            hash = (hash * BASE + str.charAt(i)) % MOD;
        }
        return hash;
    }
    
    public int rollingHash(int oldHash, char oldChar, char newChar, int len) {
        int pow = 1;
        for (int i = 0; i < len - 1; i++) {
            pow = (pow * BASE) % MOD;
        }
        
        // Remove old character
        oldHash = (oldHash - (oldChar * pow) % MOD + MOD) % MOD;
        
        // Add new character
        return (oldHash * BASE + newChar) % MOD;
    }
}
```

---

## 🔄 Collision Resolution

### 1. Separate Chaining
```java
class HashTableChaining<K, V> {
    private class Node {
        K key;
        V value;
        Node next;
        
        Node(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }
    
    private Node[] table;
    private int size;
    private int capacity;
    
    public HashTableChaining(int capacity) {
        this.capacity = capacity;
        this.table = new Node[capacity];
        this.size = 0;
    }
    
    private int hash(K key) {
        return Math.abs(key.hashCode()) % capacity;
    }
    
    public void put(K key, V value) {
        int index = hash(key);
        Node head = table[index];
        
        // Check if key already exists
        Node current = head;
        while (current != null) {
            if (current.key.equals(key)) {
                current.value = value;
                return;
            }
            current = current.next;
        }
        
        // Add new node at beginning
        Node newNode = new Node(key, value);
        newNode.next = head;
        table[index] = newNode;
        size++;
        
        // Resize if load factor exceeds threshold
        if ((double) size / capacity > 0.75) {
            resize();
        }
    }
    
    public V get(K key) {
        int index = hash(key);
        Node current = table[index];
        
        while (current != null) {
            if (current.key.equals(key)) {
                return current.value;
            }
            current = current.next;
        }
        
        return null;
    }
    
    private void resize() {
        Node[] oldTable = table;
        capacity *= 2;
        table = new Node[capacity];
        size = 0;
        
        for (Node head : oldTable) {
            Node current = head;
            while (current != null) {
                put(current.key, current.value);
                current = current.next;
            }
        }
    }
}
```

### 2. Open Addressing - Linear Probing
```java
class HashTableLinearProbing<K, V> {
    private K[] keys;
    private V[] values;
    private boolean[] deleted;
    private int size;
    private int capacity;
    
    @SuppressWarnings("unchecked")
    public HashTableLinearProbing(int capacity) {
        this.capacity = capacity;
        this.keys = (K[]) new Object[capacity];
        this.values = (V[]) new Object[capacity];
        this.deleted = new boolean[capacity];
        this.size = 0;
    }
    
    private int hash(K key) {
        return Math.abs(key.hashCode()) % capacity;
    }
    
    public void put(K key, V value) {
        if (size >= capacity / 2) resize();
        
        int index = hash(key);
        
        while (keys[index] != null && !deleted[index]) {
            if (keys[index].equals(key)) {
                values[index] = value;
                return;
            }
            index = (index + 1) % capacity;
        }
        
        keys[index] = key;
        values[index] = value;
        deleted[index] = false;
        size++;
    }
    
    public V get(K key) {
        int index = hash(key);
        
        while (keys[index] != null) {
            if (!deleted[index] && keys[index].equals(key)) {
                return values[index];
            }
            index = (index + 1) % capacity;
        }
        
        return null;
    }
    
    public void delete(K key) {
        int index = hash(key);
        
        while (keys[index] != null) {
            if (!deleted[index] && keys[index].equals(key)) {
                deleted[index] = true;
                size--;
                return;
            }
            index = (index + 1) % capacity;
        }
    }
}
```

### 3. Quadratic Probing
```java
private int quadraticProbe(K key, int attempt) {
    int hash = Math.abs(key.hashCode()) % capacity;
    return (hash + attempt * attempt) % capacity;
}
```

### 4. Double Hashing
```java
private int doubleHash(K key, int attempt) {
    int hash1 = Math.abs(key.hashCode()) % capacity;
    int hash2 = 7 - (Math.abs(key.hashCode()) % 7); // Secondary hash
    return (hash1 + attempt * hash2) % capacity;
}
```

---

## 🎯 Common Hashing Problems

### 1. Two Sum
```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    
    return new int[]{};
}
```

### 2. Group Anagrams
```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();
    
    for (String str : strs) {
        char[] chars = str.toCharArray();
        Arrays.sort(chars);
        String key = String.valueOf(chars);
        
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(str);
    }
    
    return new ArrayList<>(map.values());
}
```

### 3. Longest Substring Without Repeating Characters
```java
public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> map = new HashMap<>();
    int maxLength = 0;
    int left = 0;
    
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        
        if (map.containsKey(c)) {
            left = Math.max(left, map.get(c) + 1);
        }
        
        map.put(c, right);
        maxLength = Math.max(maxLength, right - left + 1);
    }
    
    return maxLength;
}
```

### 4. LRU Cache
```java
class LRUCache {
    private class Node {
        int key, value;
        Node prev, next;
        
        Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    
    private Map<Integer, Node> cache;
    private Node head, tail;
    private int capacity;
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cache = new HashMap<>();
        
        // Create dummy head and tail
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        Node node = cache.get(key);
        if (node == null) return -1;
        
        // Move to head (most recently used)
        moveToHead(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        Node node = cache.get(key);
        
        if (node != null) {
            node.value = value;
            moveToHead(node);
        } else {
            Node newNode = new Node(key, value);
            
            if (cache.size() >= capacity) {
                // Remove least recently used
                Node tail = removeTail();
                cache.remove(tail.key);
            }
            
            cache.put(key, newNode);
            addToHead(newNode);
        }
    }
    
    private void addToHead(Node node) {
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }
    
    private void removeNode(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private void moveToHead(Node node) {
        removeNode(node);
        addToHead(node);
    }
    
    private Node removeTail() {
        Node last = tail.prev;
        removeNode(last);
        return last;
    }
}
```

---

## 🔍 Hash-based Data Structures

### 1. HashSet Implementation
```java
class SimpleHashSet<T> {
    private static final int DEFAULT_CAPACITY = 16;
    private static final double LOAD_FACTOR = 0.75;
    
    private Object[] buckets;
    private int size;
    private int capacity;
    
    @SuppressWarnings("unchecked")
    public SimpleHashSet() {
        capacity = DEFAULT_CAPACITY;
        buckets = new Object[capacity];
        size = 0;
    }
    
    public boolean add(T element) {
        if (contains(element)) return false;
        
        if (size >= capacity * LOAD_FACTOR) {
            resize();
        }
        
        int index = getIndex(element);
        @SuppressWarnings("unchecked")
        Set<T> bucket = (Set<T>) buckets[index];
        
        if (bucket == null) {
            bucket = new HashSet<>();
            buckets[index] = bucket;
        }
        
        bucket.add(element);
        size++;
        return true;
    }
    
    public boolean contains(T element) {
        int index = getIndex(element);
        @SuppressWarnings("unchecked")
        Set<T> bucket = (Set<T>) buckets[index];
        return bucket != null && bucket.contains(element);
    }
    
    private int getIndex(T element) {
        return Math.abs(element.hashCode()) % capacity;
    }
    
    private void resize() {
        Object[] oldBuckets = buckets;
        capacity *= 2;
        buckets = new Object[capacity];
        size = 0;
        
        for (Object bucket : oldBuckets) {
            if (bucket != null) {
                @SuppressWarnings("unchecked")
                Set<T> set = (Set<T>) bucket;
                for (T element : set) {
                    add(element);
                }
            }
        }
    }
}
```

### 2. Bloom Filter
```java
class BloomFilter {
    private BitSet bitSet;
    private int size;
    private int hashFunctions;
    
    public BloomFilter(int size, int hashFunctions) {
        this.size = size;
        this.hashFunctions = hashFunctions;
        this.bitSet = new BitSet(size);
    }
    
    public void add(String element) {
        for (int i = 0; i < hashFunctions; i++) {
            int hash = hash(element, i) % size;
            bitSet.set(Math.abs(hash));
        }
    }
    
    public boolean mightContain(String element) {
        for (int i = 0; i < hashFunctions; i++) {
            int hash = hash(element, i) % size;
            if (!bitSet.get(Math.abs(hash))) {
                return false;
            }
        }
        return true;
    }
    
    private int hash(String element, int seed) {
        int hash = 0;
        for (char c : element.toCharArray()) {
            hash = hash * 31 + c + seed;
        }
        return hash;
    }
}
```

---

## 📊 Performance Analysis

### Time Complexities
| Operation | Average Case | Worst Case | Best Case |
|-----------|--------------|------------|-----------|
| **Search** | O(1) | O(n) | O(1) |
| **Insert** | O(1) | O(n) | O(1) |
| **Delete** | O(1) | O(n) | O(1) |

### Space Complexity
- **Hash Table**: O(n) where n is number of elements
- **Load Factor**: Affects performance (typically 0.75)
- **Collision Resolution**: Additional space for chaining

### Collision Resolution Comparison
| Method | Space | Search | Insert | Delete |
|--------|-------|--------|--------|--------|
| **Chaining** | O(n) | O(1 + α) | O(1 + α) | O(1 + α) |
| **Linear Probing** | O(m) | O(1 + α²) | O(1 + α²) | O(1 + α²) |
| **Quadratic Probing** | O(m) | O(1 + α²) | O(1 + α²) | O(1 + α²) |

*α = load factor, m = table size*

---

## 🎯 Advanced Hashing Techniques

### 1. Consistent Hashing
```java
class ConsistentHashRing {
    private TreeMap<Integer, String> ring = new TreeMap<>();
    private int virtualNodes;
    
    public ConsistentHashRing(int virtualNodes) {
        this.virtualNodes = virtualNodes;
    }
    
    public void addServer(String server) {
        for (int i = 0; i < virtualNodes; i++) {
            int hash = hash(server + ":" + i);
            ring.put(hash, server);
        }
    }
    
    public void removeServer(String server) {
        for (int i = 0; i < virtualNodes; i++) {
            int hash = hash(server + ":" + i);
            ring.remove(hash);
        }
    }
    
    public String getServer(String key) {
        if (ring.isEmpty()) return null;
        
        int hash = hash(key);
        Map.Entry<Integer, String> entry = ring.ceilingEntry(hash);
        
        if (entry == null) {
            entry = ring.firstEntry();
        }
        
        return entry.getValue();
    }
    
    private int hash(String key) {
        return key.hashCode();
    }
}
```

### 2. Cuckoo Hashing
```java
class CuckooHashTable {
    private int[] table1, table2;
    private int size, capacity;
    private static final int MAX_ITERATIONS = 10;
    
    public CuckooHashTable(int capacity) {
        this.capacity = capacity;
        this.table1 = new int[capacity];
        this.table2 = new int[capacity];
        Arrays.fill(table1, -1);
        Arrays.fill(table2, -1);
    }
    
    public boolean insert(int key) {
        if (lookup(key)) return false;
        
        return insertHelper(key, 0);
    }
    
    private boolean insertHelper(int key, int iteration) {
        if (iteration >= MAX_ITERATIONS) {
            rehash();
            return insertHelper(key, 0);
        }
        
        int pos1 = hash1(key);
        if (table1[pos1] == -1) {
            table1[pos1] = key;
            size++;
            return true;
        }
        
        int displaced = table1[pos1];
        table1[pos1] = key;
        
        int pos2 = hash2(displaced);
        if (table2[pos2] == -1) {
            table2[pos2] = displaced;
            size++;
            return true;
        }
        
        displaced = table2[pos2];
        table2[pos2] = table1[pos1];
        
        return insertHelper(displaced, iteration + 1);
    }
    
    private int hash1(int key) {
        return Math.abs(key) % capacity;
    }
    
    private int hash2(int key) {
        return Math.abs(key / capacity) % capacity;
    }
}
```

---

## 🌟 Real-World Applications

### 💾 Database Systems
- **Indexing**: B+ trees with hash indexes
- **Query Optimization**: Hash joins
- **Distributed Databases**: Consistent hashing for sharding

### 🌐 Web Applications
- **Caching**: Redis, Memcached
- **Session Management**: Hash-based session stores
- **URL Shortening**: Hash-based ID generation

### 🔐 Security
- **Password Storage**: bcrypt, scrypt
- **Digital Signatures**: SHA family
- **Blockchain**: Proof of work hashing

---

## 🚫 Common Pitfalls & Best Practices

### ❌ Common Mistakes
1. **Poor hash function choice** - leads to clustering
2. **Ignoring load factor** - degrades performance
3. **Not handling collisions properly** - data loss
4. **Using mutable objects as keys** - breaks hash table

### ✅ Best Practices
```java
// Good hash function for strings
@Override
public int hashCode() {
    int result = 17;
    result = 31 * result + field1.hashCode();
    result = 31 * result + field2.hashCode();
    return result;
}

// Proper equals implementation
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (obj == null || getClass() != obj.getClass()) return false;
    
    MyClass other = (MyClass) obj;
    return Objects.equals(field1, other.field1) &&
           Objects.equals(field2, other.field2);
}
```

---

## 🎯 Interview Preparation

### 🔥 Must-Know Problems
1. **Two Sum** - Basic hash table usage
2. **Group Anagrams** - String hashing and grouping
3. **LRU Cache** - Hash table + doubly linked list
4. **Design HashMap** - Collision resolution implementation
5. **Valid Anagram** - Character frequency counting
6. **Intersection of Two Arrays** - Set operations
7. **First Missing Positive** - Array as hash table

### 💡 Key Concepts
- **Hash function design** and collision handling
- **Load factor** impact on performance
- **Hash table vs other data structures** trade-offs
- **Custom hashCode and equals** implementation
- **Distributed hashing** concepts

---

**Ready to hash your way to success?** Explore [Problems.md](./Problems.md) for comprehensive practice! 🗂️