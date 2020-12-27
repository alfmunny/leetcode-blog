+++
title = "1010 - Pairs of Songs With Total Durations Divisible by 60"
date = 2020-12-14T00:00:00+01:00
lastmod = 2020-12-16T00:48:07+01:00
tags = ["easy", "array", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/)


## Problem {#problem}

```text
You are given a list of songs where the ith song has a duration of time[i] seconds.

Return the number of pairs of songs for which their total duration in seconds is divisible by 60. Formally, we want the number of indices i, j such that i < j with (time[i] + time[j]) % 60 == 0.



Example 1:

Input: time = [30,20,150,100,40]
Output: 3
Explanation: Three pairs have a total duration divisible by 60:
(time[0] = 30, time[2] = 150): total duration 180
(time[1] = 20, time[3] = 100): total duration 120
(time[1] = 20, time[4] = 40): total duration 60
Example 2:

Input: time = [60,60,60]
Output: 3
Explanation: All three pairs have a total duration of 120, which is divisible by 60.


Constraints:

1 <= time.length <= 6 * 104
1 <= time[i] <= 500
```


## Solution {#solution}

```python
class Solution:
    def numPairsDivisibleBy60(self, time: List[int]) -> int:
        counter = Counter()
        ans = 0
        for t in time:
            ans += counter[(60 - t%60)%60]
            counter[t%60] += 1
        return ans
```
