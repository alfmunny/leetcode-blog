+++
title = "378 - Kth Smallest Element in a Sorted Matrix"
date = 2020-11-19T15:55:00+01:00
lastmod = 2020-11-20T21:30:20+01:00
tags = ["array", "heap", "bs", "medium"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)


## Problem {#problem}

```text
Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

Example:

matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```


## Solution {#solution}


### Solution 1: Heap with marker {#solution-1-heap-with-marker}

Maintain a heap, pop the first one, and push the right one and lower one into the heap.

But we need a mark matrix to tell if the one to be pushed was not visited before,
since it may have been in the heap when we push the lower one, and now we come to this one from left to right.

```python
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        if not matrix or not matrix[0]:
            return None
        n = len(matrix)
        heap = []
        heapq.heapify(heap)
        heapq.heappush(heap, (matrix[0][0], [0, 0]))
        mark = [[False] * n for _ in range(n)]
        while k > 0:
            ret = heapq.heappop(heap)
            i, j = ret[1]
            if i+1 < n and not mark[i+1][j]:
                heapq.heappush(heap, (matrix[i+1][j], [i+1, j]))
                mark[i+1][j] = True
            if j+1 < n and not mark[i][j+1]:
                heapq.heappush(heap, (matrix[i][j+1], [i, j+1]))
                mark[i][j+1] = True
            k -= 1

        return ret[0]
```


### Solution 2: Heap without marker {#solution-2-heap-without-marker}

We can eliminate the marker by push the first column into the heap at once. Then we only need to traverse from left to right.

```python
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        n = len(matrix)
        heap = [(row[0], index, 0) for index, row in enumerate(matrix)]
        heapify(heap)
        while k > 0:
            ret, i, j = heapq.heappop(heap)
            if j+1 < n:
                heappush(heap, (matrix[i][j+1], i, j+1))
            k -= 1
        return ret
```


### Solution 3: Binary Search {#solution-3-binary-search}

```python
class Solution:
    def kthSmallest(self, matrix):
        lo, hi = len(matrix), len(matrix[0])
        while lo < hi:
            mid = (lo+hi)//2
            if sum(bisect.bisect_right(matrix[row], mid) for row in matrix) < k:
                lo = mid+1
            else:
                hi = mid
```
