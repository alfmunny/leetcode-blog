+++
title = "212 - Word Search II"
date = 2020-07-01T00:49:00+02:00
lastmod = 2020-07-01T00:52:05+02:00
tags = ["hard", "trie", "dfs", "backtrack", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/word-search-ii)


## Problem {#problem}

```text
Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

Example:

Input:
board = [
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
words = ["oath","pea","eat","rain"]

Output: ["eat","oath"]


Note:

All inputs are consist of lowercase letters a-z.
The values of words are distinct.
```


## Solution {#solution}

DFS the matrix.

To break the dfs earlier, a Trie data structure is introduced to check wether the path is a valid combination

```python
class TrieNode:
    def __init__(self):
        self.children = defaultdict(TrieNode)
        self.isWord = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for w in word:
            node = node.children[w]
        node.isWord = True

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        trie = Trie()
        node = trie.root
        for w in words:
            trie.insert(w)
        ans = []
        for i in range(len(board)):
            for j in range(len(board[0])):
                self.dfs(board, i, j, node, "", ans)
        return ans


    def dfs(self, board, i, j, node, path, ans):
        if node.isWord:
            ans.append(path)
            node.isWord = False

        if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]) or board[i][j] not in node.children:
            return

        val = board[i][j]
        board[i][j] = "#"
        for pair in [[0, 1], [1, 0], [0, -1], [-1, 0]]:
            self.dfs(board, i+pair[0], j+pair[1], node.children[val], path+val, ans)
        board[i][j] = val
```
