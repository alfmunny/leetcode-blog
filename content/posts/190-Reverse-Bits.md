+++
title = "190 - Reverse Bits"
date = 2020-07-13T00:28:00+02:00
lastmod = 2020-07-13T00:43:19+02:00
tags = ["easy", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/reverse-bits/)


## Problem {#problem}

```text
Reverse bits of a given 32 bits unsigned integer.

Example 1:

Input: 00000010100101000001111010011100
Output: 00111001011110000010100101000000
Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.

Example 2:

Input: 11111111111111111111111111111101
Output: 10111111111111111111111111111111
Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is 10111111111111111111111111111111.

Note:

Note that in some languages such as Java, there is no unsigned integer type. In this case, both input and output will be given as signed integer type and should not affect your implementation, as the internal binary representation of the integer is the same whether it is signed or unsigned.
In Java, the compiler represents the signed integers using 2's complement notation. Therefore, in Example 2 above the input represents the signed integer -3 and the output represents the signed integer -1073741825.
```


## Solution {#solution}


### Solution 1: Reverse bit one by one {#solution-1-reverse-bit-one-by-one}

```python
class Solution:
    def reverseBits(self, n: int) -> int:
        res = 0
        shift = 31
        while n:
            res += (n & 1) << shift
            n = n >> 1
            shift -= 1
        return res
```


### Solution 2: Reverse bit with masks {#solution-2-reverse-bit-with-masks}

1.  First we swith first 16 bits and last 16 bits
2.  Repeat this operation in each half part. For example switch the first 8 bits and last 8 bits in the left 16 bits. Do the same in the right one
3.  Until only switch one bit

<!--listend-->

```python
class Solution:
    def reverseBits(self, n: int) -> int:
        n = (n << 16 | n >> 16)
        n = ((n & 0xff00ff00) >> 8 | (n & 0x00ff00ff) << 8)
        n = ((n & 0xf0f0f0f0) >> 4 | (n & 0x0f0f0f0f) << 4)
        n = ((n & 0xcccccccc) >> 2 | (n & 0x33333333) << 2)
        n = ((n & 0xaaaaaaaa) >> 1 | (n & 0x55555555) << 1)
        return n
```
