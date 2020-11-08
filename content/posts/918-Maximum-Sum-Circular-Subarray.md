+++
title = "918 - Maximum Sum Circular Subarray"
date = 2020-05-15T22:27:00+02:00
lastmod = 2020-05-15T22:27:43+02:00
tags = ["medium", "array", "dp", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/maximum-sum-circular-subarray/)


## Problem {#problem}

> Given a circular array C of integers represented by A, find the maximum possible sum of a non-empty subarray of C.
>
> Here, a circular array means the end of the array connects to the beginning of the array.  (Formally, C[i] = A[i] when 0 <= i < A.length, and C[i+A.length] = C[i] when i >= 0.)
>
> Also, a subarray may only include each element of the fixed buffer A at most once.  (Formally, for a subarray C[i], C[i+1], ..., C[j], there does not exist i <= k1, k2 <= j with k1 % A.length = k2 % A.length.)
>
> Example 1:
>
> Input: [1,-2,3,-2]
> Output: 3
> Explanation: Subarray [3] has maximum sum 3
>
> Example 2:
>
> Input: [5,-3,5]
> Output: 10
> Explanation: Subarray [5,5] has maximum sum 5 + 5 = 10
>
> Example 3:
>
> Input: [3,-1,2,-1]
> Output: 4
> Explanation: Subarray [2,-1,3] has maximum sum 2 + (-1) + 3 = 4
>
> Example 4:
>
> Input: [3,-2,2,-3]
> Output: 3
> Explanation: Subarray [3] and [3,-2,2] both have maximum sum 3
>
> Example 5:
>
> Input: [-2,-3,-1]
> Output: -1
> Explanation: Subarray [-1] has maximum sum -1
>
> Note:
>
> -30000 <= A[i] <= 30000
> 1 <= A.length <= 30000


## Solution {#solution}

Use dp we can solve the problem without circular easily. See problem 53. Maximum Subarray.

So we have a maxSum.

There are only two possibility where the sub array locates.

1.  The sub array is in the loop of array

    ----[-----]----- ------------

    It's `maxSum`.

2.  The sub array connects the next loop.

    ----------[-- ---]----------

    we can rearrange it to:

    [---]------[--]

    The the part outside the maximum subarray is "minimum subarray".

    And we can calculate the `minSum` with the same algorithm for `maxSum`.

The results is

```python
max(maxSum, s - minSum)
```

Corner case:

When all elements are negative, the maxSum is also negative. and s - minSum would be 0. max(maxSum, s - minSum) is 0.

But according to the description, we should return maxSum.

```python
class Solution:
    def maxSubarraySumCircular(self, A):
        curMin = 0
        curMax = 0
        minSum = sys.maxsize
        maxSum = -sys.maxsize
        s = 0
        for c in A:
            s += c
            curMax = max(c, curMax + c)
            maxSum = max(maxSum, curMax)
            curMin = min(c, curMin + c)
            minSum = min(minSum, curMin)

        return max(maxSum, s - minSum) if maxSum > 0 else maxSum
```
