+++
title = "691 - Stickers to Spell Word"
date = 2020-11-22T18:35:00+01:00
lastmod = 2020-11-22T18:37:35+01:00
tags = ["hard", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/stickers-to-spell-word/)


## Problem {#problem}

```text
We are given N different types of stickers. Each sticker has a lowercase English word on it.

You would like to spell out the given target string by cutting individual letters from your collection of stickers and rearranging them.

You can use each sticker more than once if you want, and you have infinite quantities of each sticker.

What is the minimum number of stickers that you need to spell out the target? If the task is impossible, return -1.

Example 1:

Input:

["with", "example", "science"], "thehat"
Output:

3
Explanation:

We can use 2 "with" stickers, and 1 "example" sticker.
After cutting and rearrange the letters of those stickers, we can form the target "thehat".
Also, this is the minimum number of stickers necessary to form the target string.
Example 2:

Input:

["notice", "possible"], "basicbasic"
Output:

-1
Explanation:

We can't form the target "basicbasic" from cutting letters from the given stickers.
Note:

stickers has length in the range [1, 50].
stickers consists of lowercase English words (without apostrophes).
target has length in the range [1, 15], and consists of lowercase English letters.
In all test cases, all words were chosen randomly from the 1000 most common US English words, and the target was chosen as a concatenation of two random words.
The time limit may be more challenging than usual. It is expected that a 50 sticker test case can be solved within 35ms on average.
```


## Solution {#solution}

```python
class Solution:
    def minStickers(self, stickers: List[str], target: str) -> int:
        self.ret = float("inf")
        self.stickers = stickers
        self.dfs([], target, 0, 0)
        return self.ret if self.ret < float("inf") else -1

    def dfs(self, pool, target, index, num_s):
        if num_s >= self.ret:
            return
        if index >= len(target):
            self.ret = num_s
            return
        if target[index] in pool:
            pool.remove(target[index])
            self.dfs(pool, target, index+1, num_s)
            pool.append(target[index])
        else:
            for w in self.stickers:
                if target[index] in w:
                    new_chars = list(w)
                    new_chars.remove(target[index])
                    self.dfs(pool + new_chars, target, index+1, num_s+1)
```
