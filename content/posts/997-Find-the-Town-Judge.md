+++
title = "997 - Find the Town Judge"
date = 2020-05-10T21:10:00+02:00
lastmod = 2020-05-10T21:11:19+02:00
tags = ["easy", "hash", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/find-the-town-judge/)


## Problem {#problem}

```text
In a town, there are N people labelled from 1 to N.
There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:

1. The town judge trusts nobody.
2. Everybody (except for the town judge) trusts the town judge.
3. There is exactly one person that satisfies properties 1 and 2.

You are given trust, an array of pairs trust[i] = [a, b] representing that the person labelled a trusts the person labelled b.

If the town judge exists and can be identified, return the label of the town judge.  Otherwise, return -1.

Example 1:

Input: N = 2, trust = [[1,2]]
Output: 2

Example 2:

Input: N = 3, trust = [[1,3],[2,3]]
Output: 3

Example 3:

Input: N = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1

Example 4:

Input: N = 3, trust = [[1,2],[2,3]]
Output: -1

Example 5:

Input: N = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]
Output: 3


Note:

1 <= N <= 1000
trust.length <= 10000
trust[i] are all different
trust[i][0] != trust[i][1]
1 <= trust[i][0], trust[i][1] <= N
```


## Solution {#solution}

Two tables:

1.  one for counting how many trusts each person gets
2.  one for counting how many other people each person trusts

<!--listend-->

```python
class Solution:
    def findJudge(self, N: int, trust: List[List[int]]) -> int:
        people = [0] * (N)
        h = defaultdict(int)

        for t in trust:
            people[t[1]-1] += 1
            h[t[0]-1] = 1

        for i in range(N):
            if people[i] >= N - 1 and h[i] == 0:
                return i+1

        return -1
```
