# String Data Structure

## Table of Contents
1. [Introduction to Strings](#introduction)
2. [String Declaration and Initialization](#declaration)
3. [String Operations](#operations)
4. [String Methods](#methods)
5. [String and Arrays](#string-and-arrays)
6. [Common String Problems](#problems)
7. [Best Practices](#best-practices)

## Introduction <a name="introduction"></a>
A String is a sequence of characters. In most programming languages, strings are used to represent text and are one of the most commonly used data types. Strings are immutable in many programming languages, meaning once created, their contents cannot be changed.

## String Declaration and Initialization <a name="declaration"></a>

### Different ways to declare strings:
```java
// Using string literal
String str1 = "Hello World";

// Using new keyword
String str2 = new String("Hello World");

// Empty string
String str3 = "";

// Character array to String
char[] charArray = {'H', 'e', 'l', 'l', 'o'};
String str4 = new String(charArray);
```

## String Operations <a name="operations"></a>

### 1. Concatenation
```java
String firstName = "John";
String lastName = "Doe";
String fullName = firstName + " " + lastName;  // "John Doe"

// Using concat() method
String result = firstName.concat(" ").concat(lastName);
```

### 2. String Comparison
```java
String str1 = "Hello";
String str2 = "hello";

// Comparing strings
boolean isEqual = str1.equals(str2);          // false
boolean isEqualIgnoreCase = str1.equalsIgnoreCase(str2);  // true

// Comparing using compareTo()
int comparison = str1.compareTo(str2);        // Returns negative value
```

## String Methods <a name="methods"></a>

### Basic Methods
```java
String text = "Hello World";

// Length
int length = text.length();  // 11

// Accessing characters
char firstChar = text.charAt(0);  // 'H'

// Substring
String sub1 = text.substring(0, 5);  // "Hello"
String sub2 = text.substring(6);     // "World"

// Case conversion
String upper = text.toUpperCase();  // "HELLO WORLD"
String lower = text.toLowerCase();  // "hello world"
```

### Search and Replace
```java
String text = "Hello World";

// Index finding
int indexOfO = text.indexOf('o');    // 4
int lastIndexOfO = text.lastIndexOf('o');  // 7

// Contains
boolean hasWorld = text.contains("World");  // true

// Replace
String newText = text.replace('l', 'L');  // "HeLLo WorLd"
String replaced = text.replaceAll("o", "0");  // "Hell0 W0rld"
```

## String and Arrays <a name="string-and-arrays"></a>

### Converting String to Array
```java
String text = "Hello World";

// To char array
char[] charArray = text.toCharArray();

// Split into string array
String[] words = text.split(" ");  // ["Hello", "World"]
```

### Converting Array to String
```java
char[] charArray = {'H', 'e', 'l', 'l', 'o'};
String str = new String(charArray);

// Using String.join()
String[] words = {"Hello", "World"};
String joined = String.join(" ", words);  // "Hello World"
```

## Common String Problems <a name="problems"></a>

### 1. String Reversal
```java
public static String reverseString(String str) {
    return new StringBuilder(str).reverse().toString();
}
```

### 2. Palindrome Check
```java
public static boolean isPalindrome(String str) {
    String clean = str.toLowerCase().replaceAll("[^a-zA-Z0-9]", "");
    return clean.equals(new StringBuilder(clean).reverse().toString());
}
```

### 3. Removing Duplicates
```java
public static String removeDuplicates(String str) {
    StringBuilder result = new StringBuilder();
    str.chars().distinct().forEach(c -> result.append((char)c));
    return result.toString();
}
```

## Best Practices <a name="best-practices"></a>

1. **String Pool Usage**: Use string literals instead of new String() when possible
   ```java
   // Preferred
   String str1 = "Hello";
   
   // Avoid unless necessary
   String str2 = new String("Hello");
   ```

2. **StringBuilder for Concatenation**: Use StringBuilder for multiple string concatenations
   ```java
   // Bad practice
   String result = "";
   for(int i = 0; i < 100; i++) {
       result += i;
   }

   // Good practice
   StringBuilder result = new StringBuilder();
   for(int i = 0; i < 100; i++) {
       result.append(i);
   }
   ```

3. **Proper Comparison**: Always use equals() for string comparison instead of ==
   ```java
   String str1 = "Hello";
   String str2 = "Hello";
   
   // Wrong way
   if (str1 == str2) { }
   
   // Correct way
   if (str1.equals(str2)) { }
   ```

4. **Null Checks**: Always check for null before performing operations
   ```java
   String str = null;
   
   // Safe way
   if (str != null && !str.isEmpty()) {
       // perform operations
   }
   ```

Remember:
- Strings are immutable - methods return new strings rather than modifying existing ones
- Use appropriate methods for performance-critical applications
- Consider memory usage when working with large strings
- Use StringBuilder for multiple modifications
- Always handle null cases appropriately

## Practice Problems
1. Implement string reversal without using built-in methods
2. Find all permutations of a string
3. Check if two strings are anagrams
4. Find the longest palindromic substring
5. Implement string compression

These problems will help strengthen your understanding of string manipulation and common algorithms.
