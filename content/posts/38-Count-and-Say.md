+++
title = "38 - Count and Say"
date = 2020-06-08T23:28:00+02:00
lastmod = 2020-06-08T23:28:30+02:00
tags = ["easy", "array", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/count-and-say/)


## Problem {#problem}

```text
The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence. You can do so recursively, in other words from the previous member read off the digits, counting the number of digits in groups of the same digit.

Note: Each term of the sequence of integers will be represented as a string.



Example 1:

Input: 1
Output: "1"
Explanation: This is the base case.
Example 2:

Input: 4
Output: "1211"
Explanation: For n = 3 the term was "21" in which we have two groups "2" and "1", "2" can be read as "12" which means frequency = 1 and value = 2, the same way "1" is read as "11", so the answer is the concatenation of "12" and "11" which is "1211".
```


## Solution {#solution}

```python
class Solution:
    def countAndSay(self, n: int) -> str:
        s = "1"

        for i in range(n-1):
            say = s[0]
            count = 0
            tmp = ""
            for c in s:
                if c == say:
                    count += 1
                else:
                    tmp = tmp + str(count) + say
                    say = c
                    count = 1
            s = tmp + str(count) + say
        return s
```
