+++
title = "66 - Plus One"
date = 2020-06-08T23:45:00+02:00
lastmod = 2020-06-11T00:01:44+02:00
tags = ["easy", "array", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/plus-one/)


## Problem {#problem}

```text
Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

Example 1:

Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Example 2:

Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```


## Solution {#solution}

```python
class Solution:
    def plusOne(self, digits):
        add = 1

        for i in range(len(digits) - 1, -1, -1):
            digits[i], add = (digits[i] + add) % 10, (digits[i] + add)//10

        if add:
            digits.insert(0, add)

        return digits
```
