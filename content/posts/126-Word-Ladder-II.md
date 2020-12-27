+++
title = "126 - Word Ladder II"
date = 2020-11-22T00:36:00+01:00
lastmod = 2020-11-22T00:39:14+01:00
tags = ["hard", "graph", "1-hint", "bfs", "dfs"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/word-ladder-ii/)


## Problem {#problem}

```text
Given two words (beginWord and endWord), and a dictionary's word list, find all shortest transformation sequence(s) from beginWord to endWord, such that:

Only one letter can be changed at a time
Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
Note:

Return an empty list if there is no such transformation sequence.
All words have the same length.
All words contain only lowercase alphabetic characters.
You may assume no duplicates in the word list.
You may assume beginWord and endWord are non-empty and are not the same.
Example 1:

Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output:
[
  ["hit","hot","dot","dog","cog"],
  ["hit","hot","lot","log","cog"]
]
Example 2:

Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: []

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```


## Solution {#solution}

```python
class Solution:
    def findLadders(self, beginWord: str, endWord: str, wordList: List[str]):
        if endWord not in wordList:
            return []

        h = Counter(set(wordList))
        paths = defaultdict(set)
        queue = [beginWord]
        h[beginWord] = 0
        levels = []
        seen = False
        while queue and not seen:
            tmp = []
            while queue:
                w = queue.pop()
                if w == endWord:
                    seen = True
                for i in range(len(w)):
                    for j in range(26):
                        to = w[:i] + chr(ord('a') + j) + w[i+1:]
                        if to != w and h[to]:
                            tmp.append(to)
                            paths[w].add(to)
            for t in tmp:
                h[t] = 0

            levels.append(list(tmp))
            queue = tmp

        ret = []
        self.dfs(beginWord, endWord, paths, [], ret)
        return ret

    def dfs(self, beginWord, endWord, paths, path, ret):
        if beginWord == endWord:
            ret.append(path+[beginWord])
            return

        for x in paths[beginWord]:
            self.dfs(x, endWord, paths, path+[beginWord], ret)
```
