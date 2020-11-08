+++
title = "354 - Russian Doll Envelopes"
date = 2020-10-11T18:39:00+02:00
lastmod = 2020-10-11T19:24:50+02:00
tags = ["hard", "dp", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/russian-doll-envelopes/)


## Problem {#problem}

```text
You have a number of envelopes with widths and heights given as a pair of integers (w, h). One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

What is the maximum number of envelopes can you Russian doll? (put one inside other)

Note:
Rotation is not allowed.

Example:

Input: [[5,4],[6,4],[6,7],[2,3]]
Output: 3
Explanation: The maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).
```


## Solution {#solution}

```python
class Solution:
    def maxEnvelopes(self, envelopes: List[List[int]]) -> int:
        if not envelopes:
            return 0

        heights = [env[1] for env in sorted(envelopes, key = lambda x: [x[0], -x[1]])]
        print(heights)
        dp = [heights[0]]

        for i in range(1, len(heights)):
            if heights[i] > dp[-1]:
                dp.append(heights[i])
            else:
                l = self.bs(dp, heights[i])

                dp[l] = heights[i]
        return len(dp)

    def bs(self, dp, target):
        r = len(dp) - 1
        l = 0
        while l <= r:
            mid = (l+r) // 2
            if dp[mid] > target:
                r = mid - 1
            elif dp[mid] < target:
                l = mid + 1

            else:
                return mid
        return l
```
