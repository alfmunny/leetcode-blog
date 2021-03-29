+++
title = "42 - Trapping Rain Water"
date = 2020-12-29T22:25:00+01:00
lastmod = 2020-12-29T22:29:31+01:00
tags = ["hard", "array", "presum", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/trapping-rain-water/)


## Problem {#problem}

```text
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.


Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```


## Solution {#solution}

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        ans = 0
        leftHeight = self.leftMaxHeight(height)
        rightHeight = self.rightMaxHeight(height)

        for i in range(len(height)):
            max_bar = min(leftHeight[i], rightHeight[i])
            if max_bar > height[i]:
                ans += max_bar - height[i]
        return ans

    def leftMaxHeight(self, height):
        ans = [0] * len(height)
        max_left = 0
        for i in range(len(height)):
            ans[i] = max_left
            max_left = max(height[i], max_left)
        return ans

    def rightMaxHeight(self, height):
        ans = [0] * len(height)
        max_right = 0
        for i in range(len(height)-1, -1, -1):
            ans[i] = max_right
            max_right = max(height[i], max_right)
        return ans
```
