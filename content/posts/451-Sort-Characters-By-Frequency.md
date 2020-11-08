+++
title = "451 - Sort Characters By Frequency"
date = 2020-05-22T14:19:00+02:00
lastmod = 2020-05-22T15:13:31+02:00
tags = ["medium", "array", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/sort-characters-by-frequency/)


## Problem {#problem}

```text
Given a string, sort it in decreasing order based on the frequency of characters.

Example 1:

Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.

Example 2:

Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.

Example 3:

Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```


## Solution {#solution}

1.  Use a map to count the characters.
2.  Loop the map to the characters into a map using the frequency as key. The value will be a list, containing all the characters with the same frequency.
3.  Go through the map.


### Solution 1: Two maps {#solution-1-two-maps}

```python
from collections import defaultdict
class Solution:
    def frequencySort(self, s: str) -> str:
        cnt = defaultdict(int)
        freq = {}
        max_f = 0
        ans = ""

        for c in s:
            cnt[c] += 1

        for c, f in cnt.items():
            if f not in freq:
                freq[f] = []

            freq[f].append(c)
            max_f = max(max_f, f)

        for i in range(max_f, 0, -1):
            if i in freq:
                for c in freq[i]:
                    ans += c * i

        return ans
```


### Solution 2: One liner {#solution-2-one-liner}

```python
from collections import Counter
class Solution:
    def frequencySort(self, s):
        return "".join([c * cnt for c, cnt in Counter(s).most_common()])
```


## Similar Problems {#similar-problems}


### 347. Top K Frequent Element {#347-dot-top-k-frequent-element}

```text
Given a non-empty array of integers, return the k most frequent elements.

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:

Input: nums = [1], k = 1
Output: [1]
Note:

You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
You can return the answer in any order.
```

Solution

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        return [ i for i, cnt in Counter(nums).most_common()[:k]]
```


### 692. Top K Frequent Words {#692-dot-top-k-frequent-words}

```text
Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

Example 1:
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
    Note that "i" comes before "love" due to a lower alphabetical order.
Example 2:
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
Note:
You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
Input words contain only lowercase letters.
Follow up:
Try to solve it in O(n log k) time and O(n) extra space.
```

Solution

```python
class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
        counter = Counter(words)
        return heapq.nsmallest(k,
                               counter,
                               key=lambda word: (-counter[word], word))
```
