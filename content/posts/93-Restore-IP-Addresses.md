+++
title = "93 - Restore IP Addresses"
date = 2020-08-27T01:10:00+02:00
lastmod = 2020-08-27T01:11:35+02:00
tags = ["medium", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/restore-ip-addresses/)


## Problem {#problem}

```text
Given a string s containing only digits. Return all possible valid IP addresses that can be obtained from s. You can return them in any order.

A valid IP address consists of exactly four integers, each integer is between 0 and 255, separated by single points and cannot have leading zeros. For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses and "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses.



Example 1:

Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
Example 2:

Input: s = "0000"
Output: ["0.0.0.0"]
Example 3:

Input: s = "1111"
Output: ["1.1.1.1"]
Example 4:

Input: s = "010010"
Output: ["0.10.0.10","0.100.1.0"]
Example 5:

Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]


Constraints:

0 <= s.length <= 3000
s consists of digits only.
```


## Solution {#solution}

```python
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        if len(s) > 12:
            return []

        ans = []
        self.dfs(s, 0, ans, [])
        return ans

    def dfs(self, s, start, ans, path):
        if start >= len(s):
            if len(path) == 4:
                ans.append(".".join(path))
            return

        for i in range(start, min(len(s), start+3)):
            number = s[start:i+1]
            if len(number) > 1 and number[0] == "0":
                continue

            if int(number) <= 255:
                path.append(number)
                self.dfs(s, i+1, ans, path)
                path.pop()
```
