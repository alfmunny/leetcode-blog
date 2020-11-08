+++
title = "733 - Flood Fill"
date = 2020-05-09T15:50:00+02:00
lastmod = 2020-05-09T16:11:16+02:00
tags = ["easy", "stack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/flood-fill/)


## Problem {#problem}

```text
An image is represented by a 2-D array of integers, each integer representing the pixel value of the image (from 0 to 65535).

Given a coordinate (sr, sc) representing the starting pixel (row and column) of the flood fill, and a pixel value newColor, "flood fill" the image.

To perform a "flood fill", consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color as the starting pixel), and so on. Replace the color of all of the aforementioned pixels with the newColor.

At the end, return the modified image.

Example 1:
Input:
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation:
From the center of the image (with position (sr, sc) = (1, 1)), all pixels connected
by a path of the same color as the starting pixel are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected
to the starting pixel.
Note:

The length of image and image[0] will be in the range [1, 50].
The given starting pixel will satisfy 0 <= sr < image.length and 0 <= sc < image[0].length.
The value of each color in image[i][j] and newColor will be an integer in [0, 65535].
```


## Solution {#solution}

Stack.

1.  Add the starting point to stack
2.  Stack pop. Fill the point, add its valid neighbours to the stack.
3.  Repeat 2 until stack is empty

**Important**:

When the color to fill is the same as the starting  point. We don't need to continue.
Otherwise you will be always adding the same points again and again into the stack.

```python
class Solution:
    def floodFill(self, image, sr: int, sc: int, newColor: int):
        oldColor = image[sr][sc]
        stack = []
        if newColor != oldColor:
            stack.append([sr, sc])

        m = len(image)
        n = len(image[0])

        while stack:
            p = stack.pop()
            x, y = p

            image[x][y] = newColor

            for v in [[1, 0], [0, 1]]:
                for s in [1, -1]:
                    r = v[0] * s
                    c = v[1] * s
                    if 0 <= x + r < m and 0 <= y + c < n and image[x + r][y + c] == oldColor:
                        stack.append([x + r, y + c])

        return image
```
