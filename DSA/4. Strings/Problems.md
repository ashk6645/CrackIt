# 📝 String Problems - Practice Set

## Problem Categories

### 🟢 Easy Problems (5 problems)
### 🟡 Medium Problems (5 problems)
### 🔴 Hard Problems (5 problems)

---

## 🟢 Easy Problems

### Problem 1: Reverse String
**Difficulty**: Easy  
**Pattern**: Two Pointers

**Problem**: Reverse the characters of a string.

**Example**:
```
Input: s = "hello"
Output: "olleh"
```

<details>
<summary>💡 Hint</summary>
Use two pointers from both ends and swap characters.
</details>

<details>
<summary>✅ Solution</summary>

```python
def reverse_string(s):
    return s[::-1]
```
</details>

---

### Problem 2: Valid Palindrome
**Difficulty**: Easy  
**Pattern**: Two Pointers

**Problem**: Check if a string is a palindrome (reads the same backward).

**Example**:
```
Input: s = "racecar"
Output: True
```

<details>
<summary>💡 Hint</summary>
Compare characters from both ends moving towards the center.
</details>

<details>
<summary>✅ Solution</summary>

```python
def is_palindrome(s):
    return s == s[::-1]
```
</details>

---

### Problem 3: First Unique Character in a String
**Difficulty**: Easy  
**Pattern**: Hash Map

**Problem**: Find the first non-repeating character in a string.

**Example**:
```
Input: s = "leetcode"
Output: 0
```

<details>
<summary>💡 Hint</summary>
Use a hash map to count character frequencies.
</details>

<details>
<summary>✅ Solution</summary>

```python
def first_uniq_char(s):
    from collections import Counter
    count = Counter(s)
    for i, ch in enumerate(s):
        if count[ch] == 1:
            return i
    return -1
```
</details>

---

### Problem 4: Implement strStr()
**Difficulty**: Easy  
**Pattern**: Substring Search

**Problem**: Return the index of the first occurrence of needle in haystack, or -1 if not found.

**Example**:
```
Input: haystack = "hello", needle = "ll"
Output: 2
```

<details>
<summary>💡 Hint</summary>
Use built-in find or loop through substrings.
</details>

<details>
<summary>✅ Solution</summary>

```python
def str_str(haystack, needle):
    return haystack.find(needle)
```
</details>

---

### Problem 5: Anagram Check
**Difficulty**: Easy  
**Pattern**: Hash Map

**Problem**: Check if two strings are anagrams of each other.

**Example**:
```
Input: s = "anagram", t = "nagaram"
Output: True
```

<details>
<summary>💡 Hint</summary>
Sort both strings or use a hash map to count characters.
</details>

<details>
<summary>✅ Solution</summary>

```python
def is_anagram(s, t):
    return sorted(s) == sorted(t)
```
</details>

---

## 🟡 Medium Problems

### Problem 6: Longest Substring Without Repeating Characters
**Difficulty**: Medium  
**Pattern**: Sliding Window

**Problem**: Find the length of the longest substring without repeating characters.

**Example**:
```
Input: s = "abcabcbb"
Output: 3
```

<details>
<summary>💡 Hint</summary>
Use a sliding window and a set to track unique characters.
</details>

<details>
<summary>✅ Solution</summary>

```python
def length_of_longest_substring(s):
    char_set = set()
    left = max_len = 0
    for right in range(len(s)):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])
        max_len = max(max_len, right - left + 1)
    return max_len
```
</details>

---

### Problem 7: Group Anagrams
**Difficulty**: Medium  
**Pattern**: Hash Map

**Problem**: Group strings that are anagrams of each other.

**Example**:
```
Input: ["eat","tea","tan","ate","nat","bat"]
Output: [["eat","tea","ate"],["tan","nat"],["bat"]]
```

<details>
<summary>💡 Hint</summary>
Use a hash map with sorted string as key.
</details>

<details>
<summary>✅ Solution</summary>

```python
def group_anagrams(strs):
    from collections import defaultdict
    anagrams = defaultdict(list)
    for s in strs:
        key = tuple(sorted(s))
        anagrams[key].append(s)
    return list(anagrams.values())
```
</details>

---

### Problem 8: Longest Palindromic Substring
**Difficulty**: Medium  
**Pattern**: Expand Around Center

**Problem**: Find the longest palindromic substring in a string.

**Example**:
```
Input: s = "babad"
Output: "bab" or "aba"
```

<details>
<summary>💡 Hint</summary>
Expand around each character as center.
</details>

<details>
<summary>✅ Solution</summary>

```python
def longest_palindrome(s):
    res = ""
    for i in range(len(s)):
        # Odd length
        l, r = i, i
        while l >= 0 and r < len(s) and s[l] == s[r]:
            if (r - l + 1) > len(res):
                res = s[l:r+1]
            l -= 1
            r += 1
        # Even length
        l, r = i, i+1
        while l >= 0 and r < len(s) and s[l] == s[r]:
            if (r - l + 1) > len(res):
                res = s[l:r+1]
            l -= 1
            r += 1
    return res
```
</details>

---

### Problem 9: Minimum Window Substring
**Difficulty**: Medium  
**Pattern**: Sliding Window

**Problem**: Find the minimum window substring of s that contains all characters of t.

**Example**:
```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
```

<details>
<summary>💡 Hint</summary>
Use two pointers and a hash map to track counts.
</details>

<details>
<summary>✅ Solution</summary>

```python
def min_window(s, t):
    from collections import Counter
    need = Counter(t)
    missing = len(t)
    left = start = end = 0
    for right, ch in enumerate(s, 1):
        if need[ch] > 0:
            missing -= 1
        need[ch] -= 1
        if missing == 0:
            while left < right and need[s[left]] < 0:
                need[s[left]] += 1
                left += 1
            if end == 0 or right - left < end - start:
                start, end = left, right
            need[s[left]] += 1
            missing += 1
            left += 1
    return s[start:end]
```
</details>

---

### Problem 10: Decode Ways
**Difficulty**: Medium  
**Pattern**: Dynamic Programming

**Problem**: Given a string containing only digits, return the number of ways to decode it.

**Example**:
```
Input: s = "226"
Output: 3
```

<details>
<summary>💡 Hint</summary>
Use dynamic programming to count ways.
</details>

<details>
<summary>✅ Solution</summary>

```python
def num_decodings(s):
    if not s or s[0] == '0':
        return 0
    n = len(s)
    dp = [0] * (n + 1)
    dp[0] = dp[1] = 1
    for i in range(2, n + 1):
        if s[i-1] != '0':
            dp[i] += dp[i-1]
        if 10 <= int(s[i-2:i]) <= 26:
            dp[i] += dp[i-2]
    return dp[n]
```
</details>

---

## 🔴 Hard Problems

### Problem 11: Edit Distance
**Difficulty**: Hard  
**Pattern**: Dynamic Programming

**Problem**: Find the minimum number of operations to convert one string to another.

**Example**:
```
Input: word1 = "horse", word2 = "ros"
Output: 3
```

<details>
<summary>💡 Hint</summary>
Use DP table to store subproblem results.
</details>

<details>
<summary>✅ Solution</summary>

```python
def min_distance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(m + 1):
        for j in range(n + 1):
            if i == 0:
                dp[i][j] = j
            elif j == 0:
                dp[i][j] = i
            elif word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
    return dp[m][n]
```
</details>

---

### Problem 12: Wildcard Matching
**Difficulty**: Hard  
**Pattern**: Dynamic Programming

**Problem**: Implement wildcard pattern matching with support for '?' and '*'.

**Example**:
```
Input: s = "aa", p = "a*"
Output: True
```

<details>
<summary>💡 Hint</summary>
Use DP with two indices for s and p.
</details>

<details>
<summary>✅ Solution</summary>

```python
def is_match(s, p):
    m, n = len(s), len(p)
    dp = [[False] * (n + 1) for _ in range(m + 1)]
    dp[0][0] = True
    for j in range(1, n + 1):
        if p[j-1] == '*':
            dp[0][j] = dp[0][j-1]
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if p[j-1] == '*':
                dp[i][j] = dp[i][j-1] or dp[i-1][j]
            elif p[j-1] == '?' or s[i-1] == p[j-1]:
                dp[i][j] = dp[i-1][j-1]
    return dp[m][n]
```
</details>

---

### Problem 13: Regular Expression Matching
**Difficulty**: Hard  
**Pattern**: Dynamic Programming

**Problem**: Implement regular expression matching with support for '.' and '*'.

**Example**:
```
Input: s = "aab", p = "c*a*b"
Output: True
```

<details>
<summary>💡 Hint</summary>
Use DP with careful handling of '*' and '.' cases.
</details>

<details>
<summary>✅ Solution</summary>

```python
def is_match(s, p):
    m, n = len(s), len(p)
    dp = [[False] * (n + 1) for _ in range(m + 1)]
    dp[0][0] = True
    for j in range(1, n + 1):
        if p[j-1] == '*':
            dp[0][j] = dp[0][j-2]
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if p[j-1] == '.' or s[i-1] == p[j-1]:
                dp[i][j] = dp[i-1][j-1]
            elif p[j-1] == '*':
                dp[i][j] = dp[i][j-2] or (dp[i-1][j] and (p[j-2] == '.' or p[j-2] == s[i-1]))
    return dp[m][n]
```
</details>

---

### Problem 14: Word Ladder
**Difficulty**: Hard  
**Pattern**: BFS

**Problem**: Find the length of shortest transformation sequence from beginWord to endWord.

**Example**:
```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
```

<details>
<summary>💡 Hint</summary>
Use BFS and transform one letter at a time.
</details>

<details>
<summary>✅ Solution</summary>

```python
def ladder_length(beginWord, endWord, wordList):
    from collections import deque
    word_set = set(wordList)
    queue = deque([(beginWord, 1)])
    while queue:
        word, length = queue.popleft()
        if word == endWord:
            return length
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                next_word = word[:i] + c + word[i+1:]
                if next_word in word_set:
                    word_set.remove(next_word)
                    queue.append((next_word, length + 1))
    return 0
```
</details>

---

### Problem 15: Longest Valid Parentheses
**Difficulty**: Hard  
**Pattern**: Stack, Dynamic Programming

**Problem**: Find the length of the longest valid (well-formed) parentheses substring.

**Example**:
```
Input: s = "(()"
Output: 2
```

<details>
<summary>💡 Hint</summary>
Use a stack or DP to track valid substrings.
</details>

<details>
<summary>✅ Solution</summary>

```python
def longest_valid_parentheses(s):
    stack = [-1]
    max_len = 0
    for i, ch in enumerate(s):
        if ch == '(': stack.append(i)
        else:
            stack.pop()
            if stack:
                max_len = max(max_len, i - stack[-1])
            else:
                stack.append(i)
    return max_len
```
</details>

---

## Common Interview Patterns
- **Two Pointers:** For palindrome, reverse, and partition problems.
- **Sliding Window:** For substring and anagram problems.
- **Hash Map/Array:** For frequency analysis, anagrams, and unique character problems.
- **KMP/Trie:** For advanced substring and prefix search.

## Common Mistakes
- Not handling Unicode or special characters.
- Off-by-one errors in substring/slice indices.
- Forgetting string immutability in some languages.

## Interview Tips
- Clarify if the string can contain spaces, punctuation, or Unicode.
- Ask about case sensitivity and allowed character set.
- Consider edge cases: empty string, single character, all same characters.

## Further Practice
- [LeetCode String Problems](https://leetcode.com/tag/string/)
- [GeeksforGeeks String Practice](https://www.geeksforgeeks.org/string-data-structure/)
- [InterviewBit Strings](https://www.interviewbit.com/courses/programming/topics/strings/)
