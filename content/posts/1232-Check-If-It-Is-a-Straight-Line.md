+++
title = "1232 - Check If It Is a Straight Line"
date = 2020-05-09T01:18:00+02:00
lastmod = 2020-05-09T01:23:22+02:00
tags = ["easy", "geometry", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/check-if-it-is-a-straight-line/)


## Problem {#problem}

```text
You are given an array coordinates, coordinates[i] = [x, y],
where [x, y] represents the coordinate of a point.

Check if these points make a straight line in the XY plane.
```


## Solution {#solution}

**Important**

Notice the divider. It may be zero, when the lines are horizontal.

```python
class Solution:
    def checkStraightLine(self, coordinates: List[List[int]]) -> bool:
        p1 = coordinates[0]
        p2 = coordinates[1]
        slope = self.slope(p1, p2)

        for i in range(2, len(coordinates)):
            if self.slope(coordinates[0], coordinates[i]) != slope:
                return False

        return True

    def slope(self, p1, p2):
        if p1[1] == p2[1]:
            return sys.maxsize

        return (p1[0] - p2[0]) / (p1[1] - p2[1])
```
