+++
title = "84 - Largest Rectangle in Histogram"
date = 2020-03-23T00:36:00+01:00
lastmod = 2020-04-09T23:13:45+02:00
tags = ["hard", "array", "stack", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/largest-rectangle-in-histogram/)


## Problem {#problem}

```text
Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

Example:

Input: [2,1,5,6,2,3]
Output: 10
```

![](/ox-hugo/2020-03-23_00-34-37_histogram.png)
Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].

![](/ox-hugo/2020-03-23_00-35-27_histogram_area.png)
The largest rectangle is shown in the shaded area, which has area = 10 unit.


## Notes {#notes}

Main idea is to caculate both left edge and right edge for every entry in the array

Two ways of solution.


### Brute Force {#brute-force}

Generate two arrays left[] and right[] to keep the two edges of every entry.

1.  one loop to caculate left[].
2.  one loop to caculate right[].
3.  one loop to go through all the edges to caculate the square.


### Improvement of the brute force {#improvement-of-the-brute-force}

We can:

store the number of the left bars, which are >= current bar, in left[]

store the number of the right bars, which are >= current bar, in right[]

How to avoid duplicating searching.

1.  left[current] = left[current - 1]
2.  jump left[current - 1] steps to check the next interval of the array


### Stack {#stack}

Create a stack to store the index of the entry.

1.  if current entry is smaller than the top, we find the right edge of the top entry. pop it out and caculate the the max square of the top entry
2.  if current entry is not smaller than the top, push it into stack
3.  go through the left entries in the stack. The lefts ones are all have the longest bar at the top.


## Solution {#solution}


### Solution 1: brute-force {#solution-1-brute-force}

```python
class Solution:
    def largestRectangleArea(self, heights):

        if not heights:
            return 0

        n = len(heights)
        res = 0

        left = [ i for i in range(n) ]
        right = [ i for i in range(n) ]

        # caculate for the left edge
        for i in range(n):
            p = i
            while p >= 0:
                if heights[p] < heights[i]:
                    break
                p -= 1
            left[i] = p

        # caculate for the right edge
        for i in range(n):
            p = i
            while p < n:
                if heights[p] < heights[i]:
                    break
                p += 1
            right[i] = p

        for i in range(n):
            res = max(res, heights[i] * (right[i] - left[i] - 1))

        return res

print(Solution().largestRectangleArea([2, 1, 5, 6, 2, 3]))
```

O(n^2)

It will execeed time limit on leetcode.

```text
10
```


### Solution 2: improved version {#solution-2-improved-version}

```python
class Solution:
    def largestRectangleArea(self, heights):
        if not heights:
            return 0

        res = 0
        n = len(heights)
        left = [1] * n
        right = [1] * n

        # caculate left[]
        for i in range(n):
            p = i - 1
            while p >= 0:
                if heights[p] >= heights[i]:
                    left[i] += left[p]
                    # jump backward
                    p -= left[p]
                else:
                    break

        # caculate right[]
        for i in range(n - 1, -1, -1):
            p = i + 1
            while p < n:
                if heights[p] >= heights[i]:
                    right[i] += right[p]
                    # jump forward
                    p += right[p]
                else:
                    break

        for i in range(n):
            res = max(res, heights[i] * (left[i] + right[i] - 1))

        return res

print(Solution().largestRectangleArea([2, 1, 5, 6, 2, 3]))
```

Generale Case: O(n), because it uses the jump
Worst Case: O(n^2)


### Solution 3: stack {#solution-3-stack}

```python
class Solution:
    def largestRectangleArea(self, heights):

        stack = []
        n = len(heights)
        res = 0
        index = 0

        while index < n:

            if not stack or heights[stack[-1]] <= heights[index]:
                stack.append(index)
                index += 1
            else:
                top = stack.pop()
                area = (heights[top] *
                        ((index - stack[-1] - 1) if stack else index))

                res = max(res, area)

        while stack:
            h = stack.pop()
            res = max(
                r
```
