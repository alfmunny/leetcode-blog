+++
title = "118 - Pascal's Triangle"
date = 2020-06-17T23:54:00+02:00
lastmod = 2020-06-17T23:56:03+02:00
tags = ["easy", "array", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/pascals-triangle/)


## Problem {#problem}

```text
Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

Example:

Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```


## Solution {#solution}

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        ans = []

        for i in range(1, numRows+1):
            level = [1] * i

            if ans:
                for j in range(1, i-1):
                    level[j] = ans[-1][j-1] + ans[-1][j]

            ans.append(level)

        return ans
```
