+++
title = "1306 - Jump Game III"
author = ["alfmunny"]
date = 2020-03-22T20:42:00+01:00
lastmod = 2020-03-22T21:00:28+01:00
tags = ["medium", "array", "dfs"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/jump-game-iii/submissions/)


## Problem {#problem}

```text
Given an array of non-negative integers arr, you are initially positioned at start index of the array. When you are at index i, you can jump to i + arr[i] or i - arr[i], check if you can reach to any index with value 0.

Notice that you can not jump outside of the array at any time.

Example 1:

Input: arr = [4,2,3,0,3,1,2], start = 5
Output: true
Explanation:
All possible ways to reach at index 3 with value 0 are:
index 5 -> index 4 -> index 1 -> index 3
index 5 -> index 6 -> index 4 -> index 1 -> index 3

Example 2:

Input: arr = [4,2,3,0,3,1,2], start = 0
Output: true
Explanation:
One possible way to reach at index 3 with value 0 is:
index 0 -> index 4 -> index 1 -> index 3

Example 3:

Input: arr = [3,0,2,1,2], start = 2
Output: false
Explanation: There is no way to reach at index 1 with value 0.

Constraints:

1 <= arr.length <= 5 * 10^4
0 <= arr[i] < arr.length
0 <= start < arr.length
```


## Notes {#notes}

Use dfs to search for 0. Mark the visited place to trigger stop.

**Important**:

Remember to reset the mark if can not find along the path, so that it can search into another path.


## Solution {#solution}

```python
class Solution:
    def canReach(self, arr, start):
        if start >= len(arr) or start < 0:
            return False

        if arr[start] == 0:
            return True

        if arr[start] == -1:
            return False

        step = arr[start]
        arr[start] = -1

        if self.canReach(arr, start - step) or self.canReach(arr, start + step):
            return True
        else:
            arr[start] = step
            return False
```
