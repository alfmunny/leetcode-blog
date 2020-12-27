+++
title = "842 - Split Array into Fibonacci Sequence"
date = 2020-11-25T20:02:00+01:00
lastmod = 2020-11-26T01:21:53+01:00
tags = ["medium", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/split-array-into-fibonacci-sequence/)


## Problem {#problem}

```text
Given a string S of digits, such as S = "123456579", we can split it into a Fibonacci-like sequence [123, 456, 579].

Formally, a Fibonacci-like sequence is a list F of non-negative integers such that:

0 <= F[i] <= 2^31 - 1, (that is, each integer fits a 32-bit signed integer type);
F.length >= 3;
and F[i] + F[i+1] = F[i+2] for all 0 <= i < F.length - 2.
Also, note that when splitting the string into pieces, each piece must not have extra leading zeroes, except if the piece is the number 0 itself.

Return any Fibonacci-like sequence split from S, or return [] if it cannot be done.

Example 1:

Input: "123456579"
Output: [123,456,579]
Example 2:

Input: "11235813"
Output: [1,1,2,3,5,8,13]
Example 3:

Input: "112358130"
Output: []
Explanation: The task is impossible.
Example 4:

Input: "0123"
Output: []
Explanation: Leading zeroes are not allowed, so "01", "2", "3" is not valid.
Example 5:

Input: "1101111"
Output: [110, 1, 111]
Explanation: The output [11, 0, 11, 11] would also be accepted.
Note:

1 <= S.length <= 200
S contains only digits.
```


## Solution {#solution}

```python
class Solution:
    def splitIntoFibonacci(self, S: str) -> List[int]:
        self.upper_bound = 2**31-1
        self.ret = []

        self.dfs(S, 0, [], [])

        return self.ret

    def dfs(self, S, index, ret, path):
        if self.ret:
            return

        if index == len(S) and "".join(map(str, ret)) == S and len(ret) >= 3:
            self.ret = list(ret)
            return
        elif index == len(S):
            return

        path.append(S[index])

        n = int("".join(path))
        if self.isFibonacci(ret, n):
            self.dfs(S, index+1, ret+[n], [])

        self.dfs(S, index+1, ret, path)
        path.pop()

    def isFibonacci(self, sequence, number):
        if number < 0 or number > self.upper_bound:
            return False

        if len(sequence) < 2:
            return True

        return True if number == sequence[-1] + sequence[-2] else False
```
