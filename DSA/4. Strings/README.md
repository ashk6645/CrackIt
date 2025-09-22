# 🔤 Strings - Text Processing and Manipulation

## What is a String?

A string is a sequence of characters stored in contiguous memory locations. Think of it as a special type of array that specifically stores characters.

```
Index:   0    1    2    3    4
String: [H]  [E]  [L]  [L]  [O]
         ↑    ↑    ↑    ↑    ↑
        'H'  'E'  'L'  'L'  'O'
```

## Memory Layout

Strings store characters in consecutive memory addresses:

```
Memory Address: 1000  1001  1002  1003  1004
String Values:   [H]   [E]   [L]   [L]   [O]
Index:            0     1     2     3     4
```

Most programming languages implement strings as immutable sequences, meaning once created, they cannot be modified.

## ⚙️ Characteristics:

| Feature               | Description                                                                                              |
| --------------------- | -------------------------------------------------------------------------------------------------------- |
| **Immutability**      | Once created, strings **cannot be modified** in most languages                                           |
| **Sequential Access** | Characters stored in **contiguous memory locations**                                                     |
| **Length Property**   | Provides **constant time** access to string length                                                       |
| **Unicode Support**   | Can store **international characters** and symbols                                                       |
| **String Methods**    | Rich set of built-in **operations and manipulations**                                                   |
| **Memory Efficient**  | Most implementations use **shared memory** for identical strings                                         |
| **Null Termination** | In some languages (C/C++), strings are **terminated with null character** '\0'                          |

## String Operations and Complexities

| Operation | Time Complexity | Space Complexity | Description |
|-----------|----------------|------------------|-------------|
| Access | O(1) | O(1) | Get character at index |
| Search | O(n) | O(1) | Find substring/character |
| Concatenation | O(n+m) | O(n+m) | Join two strings |
| Substring | O(k) | O(k) | Extract k characters |
| Compare | O(min(n,m)) | O(1) | Compare two strings |
| Split | O(n) | O(n) | Split into array |

## Basic String Implementation

### Python Strings
```python
# Creating strings
str1 = "Hello"                  # String literal
str2 = str(123)                 # Convert to string
empty_str = ""                  # Empty string

# Basic operations
print(str1[0])                  # Access: O(1)
length = len(str1)              # Length: O(1)
substring = str1[1:4]           # Substring: O(k)
combined = str1 + " World"      # Concatenation: O(n+m)
found = "el" in str1            # Search: O(n)
```

### Java Strings
```java
// String creation
String str1 = "Hello";          // String literal
String str2 = new String("Hello"); // String object
StringBuilder sb = new StringBuilder(); // Mutable string

// Common operations
char first = str1.charAt(0);    // Access character
int length = str1.length();     // Get length
String sub = str1.substring(1,4); // Get substring
boolean contains = str1.contains("el"); // Search
String upper = str1.toUpperCase(); // Convert case
```

### C++ Strings
```cpp
// String creation
string str1 = "Hello";          // Standard string
char str2[] = "Hello";          // C-style string

// Basic operations
char first = str1[0];           // Access character
size_t len = str1.length();     // Get length
string sub = str1.substr(1,3);  // Get substring
str1.append(" World");          // Append
str1.find("el");               // Search
```

## Common String Patterns

### 1. String Reversal
```java
// Using StringBuilder
String reverse(String s) {
    return new StringBuilder(s).reverse().toString();
}

// Manual reversal
String reverse(String s) {
    char[] chars = s.toCharArray();
    int left = 0, right = chars.length - 1;
    while (left < right) {
        char temp = chars[left];
        chars[left++] = chars[right];
        chars[right--] = temp;
    }
    return new String(chars);
}
```

### 2. String Rotation
```java
boolean isRotation(String s1, String s2) {
    return s1.length() == s2.length() && 
           (s1 + s1).contains(s2);
}
```

### 3. Palindrome Check
```java
boolean isPalindrome(String s) {
    s = s.toLowerCase().replaceAll("[^a-z0-9]", "");
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left++) != s.charAt(right--)) 
            return false;
    }
    return true;
}
```

## Advanced String Techniques

### 1. KMP (Knuth-Morris-Pratt) Algorithm
Used for pattern matching with O(n+m) complexity

### 2. Rabin-Karp Algorithm
Hash-based pattern searching

### 3. Z Algorithm
Linear time pattern matching

### 4. Manacher's Algorithm
Finding longest palindromic substring in O(n)

## Tips and Best Practices

### ✅ Do's

1. **Use StringBuilder** for multiple concatenations
2. **Check for null/empty** strings
3. **Consider case sensitivity**
4. **Use appropriate methods** for comparison
5. **Handle special characters** properly

### ❌ Don'ts

1. **Don't use == for comparison** in Java
2. **Don't ignore character encoding**
3. **Don't concatenate in loops** without StringBuilder
4. **Don't assume ASCII only**
5. **Don't forget about immutability**

### Common Optimizations

1. **Use string interning** for frequent comparisons
2. **StringBuilder** for multiple modifications
3. **Character array** for in-place modifications
4. **Hash tables** for pattern matching
5. **Prefix/suffix arrays** for repeated searches

## String vs Other Data Structures

| Feature | String | Character Array | StringBuilder |
|---------|--------|-----------------|---------------|
| Mutability | Immutable | Mutable | Mutable |
| Memory | Shared Pool | Unique | Unique |
| Performance | Good for reading | Good for modification | Best for building |
| Methods | Many built-in | Basic array ops | Building focused |
| Memory Usage | Optimized | Fixed | Dynamic |

## Summary

### Key Points

1. **Strings are immutable** in most languages
2. **Use appropriate tools** for string manipulation
3. **Consider performance** implications
4. **Handle edge cases** properly
5. **Know your language's** string implementation

### When to Use Strings

- **Text processing**
- **Pattern matching**
- **Data representation**
- **File operations**
- **User input handling**

### When to Avoid Strings

- **Frequent character modifications**
- **Memory-critical operations**
- **High-performance number processing**
- **Binary data handling**

**Next Topic**: [LinkedLists - Dynamic Data Storage](../05-LinkedLists/)

---

**Practice Recommendation**: Complete at least 5 easy and 3 medium string manipulation problems before moving to the next topic. String manipulation is crucial for many programming tasks! 🚀
