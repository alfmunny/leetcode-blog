+++
title = "967 - Numbers With Same Consecutive Differences"
date = 2020-08-18T14:27:00+02:00
lastmod = 2020-08-18T14:27:45+02:00
tags = ["medium", "array", "queue", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/numbers-with-same-consecutive-differences/)


## Problem {#problem}

```text
Return all non-negative integers of length N such that the absolute difference between every two consecutive digits is K.

Note that every number in the answer must not have leading zeros except for the number 0 itself. For example, 01 has one leading zero and is invalid, but 0 is valid.

You may return the answer in any order.

Example 1:

Input: N = 3, K = 7
Output: [181,292,707,818,929]
Explanation: Note that 070 is not a valid number, because it has leading zeroes.
Example 2:

Input: N = 2, K = 1
Output: [10,12,21,23,32,34,43,45,54,56,65,67,76,78,87,89,98]
```


## Solution {#solution}

It is a simple queue problem.

Two corner cases to notice:

1.  remember to include 0 in the answers if the N == 1
2.  if K == 0, do not add +K, -K twice. They have the same value.

<!--listend-->

```python
class Solution:
    def numsSameConsecDiff(self, N: int, K: int) -> List[int]:
        ans = [i for i in range(1, 10)]

        if N == 1:
            return [0] + ans

        digits = 10 ** (N-1)

        while ans[0] / digits < 1:
            cur = ans.pop(0)
            last_digit = cur % 10
            if K == 0:
                ans.append(cur * 10 + last_digit)
            else:
                if last_digit + K < 10:
                    ans.append(cur * 10 + last_digit + K)
                if last_digit - K >= 0:
                    ans.append(cur * 10 + last_digit - K)
        return ans
```
