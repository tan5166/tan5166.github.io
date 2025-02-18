---
title: Difference between `push_back` and `+` in string
date: 2025-02-18 23:04:09 +0800
categories: [Data Structure and Algorithms, String] 
tags: [c++, string, time-complexity]     # TAG names should always be lowercase 
math: true
---



In C++, `std::string` is a dynamic container similar to `std::vector`, meaning that its operations have similar performance characteristics. Let's define the following variables:

- `s` is a `std::string`
- `c` is a `char`

When appending characters to a string using `push_back` or the `+` operator, their efficiency differs based on how the operation is performed.

## Characteristics of `push_back`

The `push_back(c)` function appends a character to the end of the string. This operation is typically $O(1)$ because it only modifies the existing storage. However, if the string's capacity is exceeded, a new memory allocation is triggered, causing an $O(n)$ complexity due to copying the existing content to the new space.

## Characteristics of the `+` Operator

Using `+` to concatenate strings or characters has different performance characteristics depending on where the new character is inserted:

- **`s = s + c`** (Appending a character to the end of the string):
   This is usually $O(1)$ if there is enough capacity in the string to accommodate the new character. However, if reallocation is needed, the complexity increases to $O(n)$ due to memory allocation and copying.
- **`s = c + s`** (Prepending a character to the beginning of the string):
   This operation requires creating a new `std::string` instance, copying `c`, and then appending `s` to it. Since the entire original string must be copied into new storage, the complexity is $O(n)$.

## Summary

| Operation        | Time Complexity                        |
| ---------------- | -------------------------------------- |
| `s.push_back(c)` | $O(1)$ ($O(n)$ if reallocation occurs) |
| `s = s + c`      | $O(1)$ ($O(n)$ if reallocation occurs) |
| `s = c + s`      | $O(n)$                                 |

**Key Takeaways:**

- Appending a character to the end of a string (`s + c` or `push_back`) is typically $O(1)$.
- Prepending a character (`c + s`) creates a new string, making it $O(n)$.
- If capacity is exceeded, any modification may trigger reallocation, leading to $O(n)$ complexity.

Understanding these performance differences is crucial when optimizing string operations, especially in scenarios involving frequent concatenation. To improve efficiency, avoid inserting characters at the beginning of a string whenever possible to minimize unnecessary memory allocations and copies.

---

> Thank you for reading! I’d love to hear your thoughts and feedback.
{: .prompt-tip }
