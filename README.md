# 🐍 Python Logic Building — Intermediate to Advanced

> A curated set of Python logic-building exercises ranging from intermediate to advanced level.  
> All solutions are written in **pure Python** and tested on **Google Colab**.

---

## 📌 Table of Contents

1. [Reverse a String Without Using Slicing](#1-reverse-a-string-without-using-slicing)
2. [Check if a Number is Armstrong](#2-check-if-a-number-is-armstrong)
3. [Find All Duplicates in a List](#3-find-all-duplicates-in-a-list)
4. [Flatten a Nested List](#4-flatten-a-nested-list)
5. [Fibonacci Using Memoization](#5-fibonacci-using-memoization)
6. [Count Word Frequency in a String](#6-count-word-frequency-in-a-string)
7. [Find the Longest Common Subsequence](#7-find-the-longest-common-subsequence)
8. [Implement a Stack Using a Class](#8-implement-a-stack-using-a-class)
9. [Binary Search (Recursive)](#9-binary-search-recursive)
10. [Generate All Permutations of a String](#10-generate-all-permutations-of-a-string)
11. [Detect a Cycle in a Linked List](#11-detect-a-cycle-in-a-linked-list)
12. [Matrix Multiplication Without NumPy](#12-matrix-multiplication-without-numpy)
13. [Find the Kth Largest Element](#13-find-the-kth-largest-element)
14. [Validate Balanced Parentheses](#14-validate-balanced-parentheses)
15. [Dynamic Programming — 0/1 Knapsack](#15-dynamic-programming--01-knapsack)

---

## 🟡 Intermediate

---

### 1. Reverse a String Without Using Slicing

**Problem:**  
Write a function to reverse a string without using Python's slicing (`[::-1]`) or `reversed()`.

```python
def reverse_string(s):
    result = ""
    for char in s:
        result = char + result
    return result

# Test
print(reverse_string("hello"))       # Output: olleh
print(reverse_string("Python"))      # Output: nohtyP
print(reverse_string("12345"))       # Output: 54321
```

**Output:**
```
olleh
nohtyP
54321
```

---

### 2. Check if a Number is Armstrong

**Problem:**  
An Armstrong number (narcissistic number) is a number that equals the sum of its own digits each raised to the power of the number of digits. Write a function to check this.  
Example: `153 = 1³ + 5³ + 3³`

```python
def is_armstrong(n):
    digits = str(n)
    power = len(digits)
    return sum(int(d) ** power for d in digits) == n

# Test
for num in [153, 370, 371, 9474, 100, 200]:
    print(f"{num} → {'Armstrong ✅' if is_armstrong(num) else 'Not Armstrong ❌'}")
```

**Output:**
```
153 → Armstrong ✅
370 → Armstrong ✅
371 → Armstrong ✅
9474 → Armstrong ✅
100 → Not Armstrong ❌
200 → Not Armstrong ❌
```

---

### 3. Find All Duplicates in a List

**Problem:**  
Given a list of integers, return all elements that appear more than once. Do not use any external libraries.

```python
def find_duplicates(lst):
    seen = set()
    duplicates = set()
    for item in lst:
        if item in seen:
            duplicates.add(item)
        else:
            seen.add(item)
    return sorted(list(duplicates))

# Test
print(find_duplicates([1, 2, 3, 2, 4, 3, 5]))   # Output: [2, 3]
print(find_duplicates([10, 20, 10, 30, 20, 20])) # Output: [10, 20]
print(find_duplicates([1, 2, 3]))                # Output: []
```

**Output:**
```
[2, 3]
[10, 20]
[]
```

---

### 4. Flatten a Nested List

**Problem:**  
Write a recursive function that takes a deeply nested list and returns a flat list of all values.

```python
def flatten(nested):
    result = []
    for item in nested:
        if isinstance(item, list):
            result.extend(flatten(item))
        else:
            result.append(item)
    return result

# Test
print(flatten([1, [2, 3], [4, [5, 6]], 7]))          # Output: [1, 2, 3, 4, 5, 6, 7]
print(flatten([[1, [2]], [3, [4, [5]]]]))              # Output: [1, 2, 3, 4, 5]
print(flatten([1, 2, 3]))                              # Output: [1, 2, 3]
```

**Output:**
```
[1, 2, 3, 4, 5, 6, 7]
[1, 2, 3, 4, 5]
[1, 2, 3]
```

---

### 5. Fibonacci Using Memoization

**Problem:**  
Compute the nth Fibonacci number using memoization (top-down dynamic programming) to avoid redundant calculations.

```python
def fibonacci(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    return memo[n]

# Test
for i in [0, 1, 5, 10, 20, 50]:
    print(f"fibonacci({i}) = {fibonacci(i)}")
```

**Output:**
```
fibonacci(0) = 0
fibonacci(1) = 1
fibonacci(5) = 5
fibonacci(10) = 55
fibonacci(20) = 6765
fibonacci(50) = 12586269025
```

---

### 6. Count Word Frequency in a String

**Problem:**  
Given a sentence, return a dictionary of each word and how many times it appears. Ignore case and punctuation.

```python
import string

def word_frequency(sentence):
    sentence = sentence.lower()
    sentence = sentence.translate(str.maketrans("", "", string.punctuation))
    words = sentence.split()
    freq = {}
    for word in words:
        freq[word] = freq.get(word, 0) + 1
    return dict(sorted(freq.items(), key=lambda x: -x[1]))

# Test
text = "The cat sat on the mat. The cat sat."
print(word_frequency(text))
```

**Output:**
```
{'the': 3, 'cat': 2, 'sat': 2, 'on': 1, 'mat': 1}
```

---

### 7. Find the Longest Common Subsequence

**Problem:**  
Given two strings, find the length of their longest common subsequence (LCS). A subsequence doesn't have to be contiguous.

```python
def lcs(s1, s2):
    m, n = len(s1), len(s2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s1[i - 1] == s2[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    return dp[m][n]

# Test
print(lcs("ABCBDAB", "BDCAB"))   # Output: 4
print(lcs("AGGTAB", "GXTXAYB"))  # Output: 4
print(lcs("ABC", "AC"))          # Output: 2
```

**Output:**
```
4
4
2
```

---

### 8. Implement a Stack Using a Class

**Problem:**  
Implement a `Stack` class with `push`, `pop`, `peek`, `is_empty`, and `size` methods — without using any built-in stack libraries.

```python
class Stack:
    def __init__(self):
        self._data = []

    def push(self, item):
        self._data.append(item)

    def pop(self):
        if self.is_empty():
            raise IndexError("Pop from empty stack")
        return self._data.pop()

    def peek(self):
        if self.is_empty():
            raise IndexError("Peek from empty stack")
        return self._data[-1]

    def is_empty(self):
        return len(self._data) == 0

    def size(self):
        return len(self._data)

    def __str__(self):
        return f"Stack({self._data})"

# Test
s = Stack()
s.push(10)
s.push(20)
s.push(30)
print(s)           # Stack([10, 20, 30])
print(s.peek())    # 30
print(s.pop())     # 30
print(s.size())    # 2
print(s.is_empty()) # False
```

**Output:**
```
Stack([10, 20, 30])
30
30
2
False
```

---

### 9. Binary Search (Recursive)

**Problem:**  
Implement binary search recursively. Return the index of the target in a sorted list, or `-1` if not found.

```python
def binary_search(arr, target, low, high):
    if low > high:
        return -1
    mid = (low + high) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search(arr, target, mid + 1, high)
    else:
        return binary_search(arr, target, low, mid - 1)

# Test
arr = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
print(binary_search(arr, 23, 0, len(arr) - 1))   # Output: 5
print(binary_search(arr, 72, 0, len(arr) - 1))   # Output: 8
print(binary_search(arr, 99, 0, len(arr) - 1))   # Output: -1
```

**Output:**
```
5
8
-1
```

---

### 10. Generate All Permutations of a String

**Problem:**  
Write a function to generate all possible permutations of a given string without using `itertools`.

```python
def permutations(s):
    if len(s) <= 1:
        return [s]
    result = []
    for i, char in enumerate(s):
        rest = s[:i] + s[i+1:]
        for perm in permutations(rest):
            result.append(char + perm)
    return result

# Test
perms = permutations("ABC")
print(perms)
print(f"Total permutations: {len(perms)}")
```

**Output:**
```
['ABC', 'ACB', 'BAC', 'BCA', 'CAB', 'CBA']
Total permutations: 6
```

---

## 🔴 Advanced

---

### 11. Detect a Cycle in a Linked List

**Problem:**  
Given a linked list, detect whether it contains a cycle using Floyd's Tortoise and Hare algorithm.

```python
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None

def has_cycle(head):
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False

# Test — create a cycle: 1 -> 2 -> 3 -> 4 -> 2 (cycle)
n1, n2, n3, n4 = Node(1), Node(2), Node(3), Node(4)
n1.next = n2
n2.next = n3
n3.next = n4
n4.next = n2  # cycle here

print(has_cycle(n1))  # Output: True

# No cycle
a, b, c = Node(1), Node(2), Node(3)
a.next = b
b.next = c
print(has_cycle(a))   # Output: False
```

**Output:**
```
True
False
```

---

### 12. Matrix Multiplication Without NumPy

**Problem:**  
Multiply two matrices using only Python lists. Raise an error if dimensions are incompatible.

```python
def matrix_multiply(A, B):
    rows_A, cols_A = len(A), len(A[0])
    rows_B, cols_B = len(B), len(B[0])

    if cols_A != rows_B:
        raise ValueError(f"Incompatible dimensions: {cols_A} vs {rows_B}")

    result = [[0] * cols_B for _ in range(rows_A)]
    for i in range(rows_A):
        for j in range(cols_B):
            for k in range(cols_A):
                result[i][j] += A[i][k] * B[k][j]
    return result

# Test
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]
C = matrix_multiply(A, B)
for row in C:
    print(row)
```

**Output:**
```
[19, 22]
[43, 50]
```

---

### 13. Find the Kth Largest Element

**Problem:**  
Find the Kth largest element in an unsorted list in O(n log n) time without using `sort()` directly on the full list — use a min-heap of size K.

```python
import heapq

def kth_largest(nums, k):
    min_heap = []
    for num in nums:
        heapq.heappush(min_heap, num)
        if len(min_heap) > k:
            heapq.heappop(min_heap)
    return min_heap[0]

# Test
print(kth_largest([3, 2, 1, 5, 6, 4], 2))         # Output: 5
print(kth_largest([3, 2, 3, 1, 2, 4, 5, 5, 6], 4)) # Output: 4
print(kth_largest([1], 1))                          # Output: 1
```

**Output:**
```
5
4
1
```

---

### 14. Validate Balanced Parentheses

**Problem:**  
Given a string with `(`, `)`, `{`, `}`, `[`, `]`, determine if it is valid. Every opening bracket must be closed in the correct order.

```python
def is_balanced(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    for char in s:
        if char in mapping:
            top = stack.pop() if stack else '#'
            if mapping[char] != top:
                return False
        else:
            stack.append(char)
    return not stack

# Test
tests = ["()", "()[]{}", "(]", "([)]", "{[]}", "(((" ]
for t in tests:
    print(f"{t!r:12} → {'Valid ✅' if is_balanced(t) else 'Invalid ❌'}")
```

**Output:**
```
'()'         → Valid ✅
'()[]{}'     → Valid ✅
'(]'         → Invalid ❌
'([)]'       → Invalid ❌
'{[]}'       → Valid ✅
'((('        → Invalid ❌
```

---

### 15. Dynamic Programming — 0/1 Knapsack

**Problem:**  
Given a list of items with weights and values, and a maximum weight capacity, find the maximum value you can carry. Each item can only be picked once.

```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            # Don't take item i
            dp[i][w] = dp[i - 1][w]
            # Take item i (if it fits)
            if weights[i - 1] <= w:
                dp[i][w] = max(dp[i][w], dp[i - 1][w - weights[i - 1]] + values[i - 1])

    return dp[n][capacity]

# Test
weights = [1, 3, 4, 5]
values  = [1, 4, 5, 7]
capacity = 7
print(f"Max value: {knapsack(weights, values, capacity)}")  # Output: 9

weights2 = [2, 3, 4, 5]
values2  = [3, 4, 5, 6]
capacity2 = 8
print(f"Max value: {knapsack(weights2, values2, capacity2)}")  # Output: 10
```

**Output:**
```
Max value: 9
Max value: 10
```

---

## 🚀 How to Run on Google Colab

1. Open [Google Colab](https://colab.research.google.com/)
2. Create a new notebook
3. Copy any solution code block into a cell
4. Press **Shift + Enter** to run

No additional installations are required — all solutions use Python's standard library only (except `heapq` for Q13, which is built-in).

---

## 📂 Repository Structure

```
📦 python-logic-building
 ┣ 📄 README.md               ← You are here
 ┣ 📄 intermediate/
 ┃ ┣ 📄 01_reverse_string.py
 ┃ ┣ 📄 02_armstrong_number.py
 ┃ ┣ 📄 03_find_duplicates.py
 ┃ ┣ 📄 04_flatten_list.py
 ┃ ┣ 📄 05_fibonacci_memo.py
 ┃ ┣ 📄 06_word_frequency.py
 ┃ ┣ 📄 07_lcs.py
 ┃ ┣ 📄 08_stack_class.py
 ┃ ┣ 📄 09_binary_search.py
 ┃ ┗ 📄 10_permutations.py
 ┗ 📄 advanced/
   ┣ 📄 11_linked_list_cycle.py
   ┣ 📄 12_matrix_multiply.py
   ┣ 📄 13_kth_largest.py
   ┣ 📄 14_balanced_parentheses.py
   ┗ 📄 15_knapsack.py
```

---

## 🧠 Concepts Covered

| Topic | Questions |
|---|---|
| String Manipulation | Q1, Q6, Q10 |
| Number Theory | Q2 |
| Lists & Sets | Q3, Q4 |
| Recursion | Q4, Q5, Q9, Q10 |
| Dynamic Programming | Q5, Q7, Q15 |
| OOP & Data Structures | Q8, Q11 |
| Searching & Sorting | Q9, Q13 |
| Linked Lists | Q11 |
| Matrix Operations | Q12 |
| Stack Applications | Q14 |

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">Made with ❤️ for Python learners | Happy Coding! 🐍</p>
