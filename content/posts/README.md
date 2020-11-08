+++
lastmod = 2020-10-11T18:56:32+02:00
tags = ["medium", "tree", "recursive", "1-pass"]
categories = ["leetcode"]
draft = false
+++

## Beautiful Arrangement {#beautiful-arrangement}

[leetcode](https://leetcode.com/problems/beautiful-arrangement/)


### Problem {#problem}

```text
Suppose you have N integers from 1 to N. We define a beautiful arrangement as an array that is constructed by these N numbers successfully if one of the following is true for the ith position (1 <= i <= N) in this array:

The number at the ith position is divisible by i.
i is divisible by the number at the ith position.


Now given N, how many beautiful arrangements can you construct?

Example 1:

Input: 2
Output: 2
Explanation:

The first beautiful arrangement is [1, 2]:

Number at the 1st position (i=1) is 1, and 1 is divisible by i (i=1).

Number at the 2nd position (i=2) is 2, and 2 is divisible by i (i=2).

The second beautiful arrangement is [2, 1]:

Number at the 1st position (i=1) is 2, and 2 is divisible by i (i=1).

Number at the 2nd position (i=2) is 1, and i (i=2) is divisible by 1.


Note:

N is a positive integer and will not exceed 15.
```


### Solution {#solution}

```python
class Solution:
    def countArrangement(self, N: int) -> int:
        self.ans = 0
        self.mark = [False for i in range(N+1)]
        self.dfs(N, self.mark, [])
        return self.ans

    def dfs(self, N, mark, path):
        if len(path) == N:
            self.ans += 1

        for n in range(1, N+1):
            index = len(path) + 1
            if mark[n] or (n % index != 0 and index % n != 0):
                continue
            mark[n] = True
            self.dfs(N, self.mark, path + [n])
            mark[n] = False
```
