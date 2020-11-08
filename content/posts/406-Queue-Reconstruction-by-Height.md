+++
title = "406 - Queue Reconstruction by Height"
date = 2020-06-08T22:47:00+02:00
lastmod = 2020-06-08T22:48:15+02:00
tags = ["medium", "array", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/queue-reconstruction-by-height/)


## Problem {#problem}

```text
Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers (h, k), where h is the height of the person and k is the number of people in front of this person who have a height greater than or equal to h. Write an algorithm to reconstruct the queue.

Note:
The number of people is less than 1,100.

Example

Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```


## Solution {#solution}

```python
class Solution:
    def main(self, people):
        people.sort(key=lambda p: (-p[0], p[1]))
        ans = []

        for p in people:
            ans.insert(p[1], p)
```
