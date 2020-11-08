+++
title = "1032 - Stream of Characters"
date = 2020-08-23T16:34:00+02:00
lastmod = 2020-08-23T17:22:19+02:00
tags = ["hard", "trie", "1-fail", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/stream-of-characters/)


## Problem {#problem}

```text
Implement the StreamChecker class as follows:

StreamChecker(words): Constructor, init the data structure with the given words.
query(letter): returns true if and only if for some k >= 1, the last k characters queried (in order from oldest to newest, including this letter just queried) spell one of the words in the given list.


Example:

StreamChecker streamChecker = new StreamChecker(["cd","f","kl"]); // init the dictionary.
streamChecker.query('a');          // return false
streamChecker.query('b');          // return false
streamChecker.query('c');          // return false
streamChecker.query('d');          // return true, because 'cd' is in the wordlist
streamChecker.query('e');          // return false
streamChecker.query('f');          // return true, because 'f' is in the wordlist
streamChecker.query('g');          // return false
streamChecker.query('h');          // return false
streamChecker.query('i');          // return false
streamChecker.query('j');          // return false
streamChecker.query('k');          // return false
streamChecker.query('l');          // return true, because 'kl' is in the wordlist


Note:

1 <= words.length <= 2000
1 <= words[i].length <= 2000
Words will only consist of lowercase English letters.
Queries will only consist of lowercase English letters.
The number of queries is at most 40000.
```


## Solution {#solution}

It's clearly a trie problem. But how to optimize it?

We must keep trace of the stream, and try to search the every pattern in the trace.
But that would be LTE.

In order not to loop through every starting point of the trace, we do it reversely, so we only need to start from the beginning once and stop for the existing word.

For example:

["dlab", "xlab"]

Create a reversed trie ["bald", "balx"]

trace = "", max length of trace = 4, because, all words in the trie are not longer than 4.

"b": trace = "b", search for "b" in the trie, False
"a": trace = "ba", search for "ba" in the trie, False
"l": trace = "bal", search for "bal" in the trie, False
"d": trace = "bald",  search for "bald" in the trie, True
"x": trace = "aldx", search for "aldx" in the trie, False

Steps:

1.  create the trie with reversed words
2.  keep the track of the stream with a max possible length
3.  search the track of the stream in the "reversed" trie.

<!--listend-->

```python
class StreamChecker:

    def __init__(self, words: List[str]):
        self.root = TrieNode()

        for w in words:
            x = self.root
            for c in reversed(w):
                if c in x.children:
                    x = x.children[c]
                else:
                    x.children[c] = TrieNode()
                    x = x.children[c]
            x.is_word = True

        self.s = ""
        self.w = max(map(len, words))

    def query(self, letter: str) -> bool:

        self.s = (letter+self.s)[:self.w]
        x = self.root
        res = False

        for c in self.s:
            if c in x.children:
                x = x.children[c]
                if x.is_word:
                    return True
            else:
                return False

        return res


class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False
```

Simplified Version

```python
import collections
from functools import reduce

class StreamChecker:
    def __init__(self, words):
        T = lambda: collections.defaultdict(T)
        self.trie = T()
        for w in words: reduce(dict.__getitem__, w[::-1], self.trie)["#"] = True
        self.s = ""
        self.w = max(map(len, words))

    def query(self, letter):
        self.s = (letter + self.s)[:self.w]
        cur = self.trie
        for c in self.s:
            if c in cur:
                cur = cur[c]
                if c["#"] == True:
                    return True
            else:
                break

        return False
```
