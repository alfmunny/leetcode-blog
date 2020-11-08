+++
title = "402 - Remove K Digits"
date = 2020-05-13T22:26:00+02:00
lastmod = 2020-05-14T16:58:57+02:00
tags = ["medium", "array", "stack", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/remove-k-digits/)


## Problem {#problem}

> Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.
>
> Note:
> The length of num is less than 10002 and will be ≥ k.
> The given num does not contain any leading zero.
>
> Example 1:
>
> Input: num = "1432219", k = 3
> Output: "1219"
> Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
>
> Example 2:
>
> Input: num = "10200", k = 1
> Output: "200"
> Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
>
> Example 3:
>
> Input: num = "10", k = 2
> Output: "0"
> Explanation: Remove all the digits from the number and it is left with nothing which is 0.


## Solution {#solution}

Stack

Corner cases:

> '1234567' k = 3: k will not be reduced to 0. So stack[:-k or None]
> '10200' k = 1: k can be reduced to 0. stack[:-0] will result in []. So stack[:-k or None]
> '1000000' k = 1: ......lstrip('0') will result 0. So we have to add `or '0'`

```python
class Solution:
    def removeKdigits(self, num, k):
        stack = []
        for c in num:
            while k and stack and stack[-1] > c:
                stack.pop()
                k -= 1
            stack.append(c)

        return ''.join(stack[:-k or None]).lstrip('0') or '0'
```
