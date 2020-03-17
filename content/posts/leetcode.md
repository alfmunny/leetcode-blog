+++
title = "LeetCode"
author = ["alfmunny"]
lastmod = 2020-03-16T01:14:52+01:00
categories = ["leetcode"]
draft = false
+++

<div class="ox-hugo-toc toc">
<div></div>

<div class="heading">Table of Contents</div>

- [41 - First Missing Positive](#41-first-missing-positive)
- [48. Rotate Image](#48-dot-rotate-image)
- [53. Maximum Subarray](#53-dot-maximum-subarray)
- [55. Jump Game](#55-dot-jump-game)
- [62. Unique Paths](#62-dot-unique-paths)
- [64. Minimum Path Sum](#64-dot-minimum-path-sum)
- [70. Climbing Stairs](#70-dot-climbing-stairs)
- [91. Decode Ways](#91-dot-decode-ways)
- [509. Fibonacci Number](#509-dot-fibonacci-number)
- [75. Sort Colors](#75-dot-sort-colors)
- [78 - Subsets](#78-subsets)
- [79 - Word Search](#79-word-search)

</div>
<!--endtoc-->


## 41 - First Missing Positive {#41-first-missing-positive}


### Problem {#problem}

```text
Given an unsorted integer array, find the smallest missing positive integer.

Example 1:

Input: [1,2,0]
Output: 3

Example 2:

Input: [3,4,-1,1]
Output: 2

Example 3:

Input: [7,8,9,11,12]
Output: 1

Note:

Your algorithm should run in O(n) time and uses constant extra space.
```


### Notes {#notes}

Run in O(n) time and uses constant extra space

1.  Say the length of the array is l, the number must be in 1...l+1 (also l possible numbers)

    For example

    [1, 2, 3, 4], the first missing positive is 5.

    [7, 8, 9, 10], the first missing positive is 1

    It means you can use the array as a constant space. The result must be (one of the indexes + 1).

2.  We put the number in the right place. When it is 10, we swap it with A[9].

After all the numbers are in the right place, the first one, whose index + 1 != number, it is the missing one


#### How to put the numer in the right place {#how-to-put-the-numer-in-the-right-place}

Use the \`while\` to swap the numbers. Only \`if\` can not do the same job.

Consider nums = [3, 4, -1, 1].

Only with if:

First Loop: swap 3 and -1

nums = [-1, 4, 3, 1]

Second Loop: swap 4 and 1

nums = [-1, 1, 3, 4]

And the process stops. Because 4 is already in the right place. You miss to put the 1 in the right place.

So you have to do it recursively, with \`while\`.


### Solution {#solution}

```python
class Solution(object):
    def firstMissingPositive(self, nums):
        l = len(nums)
        for i in range(l):
            # Note!: here has to be using while
            while (nums[i] > 0 and nums[i] <= l and nums[nums[i] - 1] != nums[i]):
                nums[nums[i]-1], nums[i] = nums[i], nums[nums[i]-1]

        for i, n in enumerate(nums):
            if (n != i+1):
                return i + 1

        return l + 1

print(Solution().firstMissingPositive([1, -1, 3, 4]))
```


## [48. Rotate Image](https://leetcode.com/problems/rotate-image/) {#48-dot-rotate-image}


### Problem {#problem}

```text
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Note:

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:

Given input matrix =
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
Example 2:

Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
],

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```


### Notes {#notes}


#### Naive solution, to do it one by one. {#naive-solution-to-do-it-one-by-one-dot}

**Important**:

You go from the outside into the middle. So the main loop is half of the dimension.

The inner loop should also shrink its size everytime. Begins at i and ends and n-2-i, **not n-1-i**.

Because you don't want to swap the last one. The last one n-1-i has already been swapped with the i.


#### Another solution: how to rotate a matrix faster {#another-solution-how-to-rotate-a-matrix-faster}

Swap the diagnoal elements and reverse each line in the matrix.

| 1 | 2 | 3 | swap | 1 | 4 | 7 | reverse | 7 | 4 | 1 |
|---|---|---|------|---|---|---|---------|---|---|---|
| 4 | 5 | 6 | ---> | 2 | 5 | 8 | ------> | 8 | 5 | 2 |
| 7 | 8 | 9 |      | 3 | 6 | 9 |         | 9 | 6 | 3 |


### Solution {#solution}


#### Solution 1: Straightforward {#solution-1-straightforward}

```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        for i in range(n//2):
            # Shrink the dimension
            # Do not include the last element
            for j in range(i, n-i-1):
                tmp = matrix[i][j]
                matrix[i][j] = matrix[n-1-j][i]
                matrix[n-1-j][i] = matrix[n-1-i][n-1-j]
                matrix[n-1-i][n-1-j] = matrix[j][n-1-i]
                matrix[j][n-1-i] = tmp

matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
Solution().rotate(matrix)
[print(*line) for line in matrix]
```


#### Solution 2: {#solution-2}

```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        for i in range(n):
            for j in range(i, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        for i in range(n):
            matrix[i].reverse()

matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
Solution().rotate(matrix)
[print(*line) for line in matrix]
```


## [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/) {#53-dot-maximum-subarray}


### Problem {#problem}

```text
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Follow up:

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```


### Notes {#notes}

Dynamic programming problem.

Use nums[i] always store the maximum sum.

maxSum(i) = maxSum(i-1) + nums[i] only if maxSum(i-1) > 0


### Solution {#solution}


#### Solution 1: use a extra dp array {#solution-1-use-a-extra-dp-array}

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        curSum = maxSum = nums[0]

        for num in nums[1:]:
          curSum = max(num, curSum+num)
          maxSum = max(curSum, maxSum)

        return maxSum

print(Solution().maxSubArray([-2,1,-3,4,-1,2,1,-5,4]))
```


#### Solution 2: no extra space, in place modify {#solution-2-no-extra-space-in-place-modify}

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        if len(nums) == 0:
            return 0

        ret = nums[0]

        for i in range(1, len(nums)):
            if nums[i - 1] > 0:
                nums[i] += nums[i - 1]

            ret = max(ret, nums[i])

        return ret
print(Solution().maxSubArray([-2,1,-3,4,-1,2,1,-5,4]))
```


## [55. Jump Game](https://leetcode.com/problems/jump-game/) {#55-dot-jump-game}


### Problem {#problem}

```text
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

Example 1:

Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
Example 2:

Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
```


### Notes {#notes}

Greedy algorithm. There are 2 approaches, from head or from tail.


#### Start from head {#start-from-head}

always remember the furthest reachable index.

```python
reach = max(i + nums[i], reach) if i <= reach
```


#### Start from tail {#start-from-tail}

always remember the last position it can reach.

```python
lastPos = i if i + nums[i] >= lastPos
```


### Solition {#solition}


#### Solution 1: start from head {#solution-1-start-from-head}

```python
class Solution():
    def canJump(self, nums):
        reach = 0

        for i in range(len(nums)):
            if i <= reach:
                reach = max(i + nums[i], reach)

        return reach >= len(nums) - 1

print(Solution().canJump([ 2,3,1,1,4 ]))
print(Solution().canJump([ 3,2,1,0,4 ] ))
```


#### Solution 2: start from tail {#solution-2-start-from-tail}

```python
class Solution():
    def canJump(self, nums):
        lastPos = len(nums) - 1
        for i in reversed(range(len(nums))):
            if i + nums[i] >= lastPos:
                lastPos = i

        return lastPos == 0

print(Solution().canJump([ 2,3,1,1,4 ]))
print(Solution().canJump([ 3,2,1,0,4 ] ))
```


## [62. Unique Paths](https://leetcode.com/problems/unique-paths/) {#62-dot-unique-paths}


### Problem {#problem}

```text
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

Note: m and n will be at most 100.

Example 1:

Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
Example 2:

Input: m = 7, n = 3
Output: 28
```


### Notes {#notes}

It is a DP problem.

1.  There are only two possibilities to arrive at the finish point
    1.  arrive at that point from above
    2.  arrive at that point from left

2.  So the ways to arrive at current point is equal to the ways from above plus the ways from left. dp[i][j] = dp[i][j-1] + dp[i - 1][j]
3.  Dynamic programming. Maintain a two dimensional matrix.
4.  Optimize it to one dimension.
5.  Complexity O(m \* n)


#### UniquePath with 2-D DP {#uniquepath-with-2-d-dp}

```python
dp[i][j] = dp[i-1][j] + dp[i][j-1]
```

After you have the edge, you go levelly to the bottom.


#### UniquePath with 1-D DP {#uniquepath-with-1-d-dp}

```python
dp[j] = dp[j - 1] + dp[j]
```


### Solution {#solution}


#### Solution 1: 2-D DP {#solution-1-2-d-dp}

```python
class Solution():
    def uniquePath(self, m, n):
        dp = [[1 for j in range(n)] for i in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i][j - 1] + dp[i - 1][j]

        return dp[-1][-1] if m and n else 0
```


#### Solution 2: 1-D DP {#solution-2-1-d-dp}

```python
class Solution():
    def uniquePath(self, m, n):
        dp = [1] * n

        for i in range(1, m):
            for j in range(1, n):
                dp[j] = dp[j - 1] + dp[j]

        return dp[-1] if m and n else 0
```


## [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/) {#64-dot-minimum-path-sum}


### Problem {#problem}

```text
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example:

Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```


### Notes {#notes}

Thinking: ~~It seems to be a greedy algorithm problem.~~

It is a dp problem.

dp equation:

dp[i][j] = min(dp[i][j-1], dp[i-1][j]) + grid[i][j]

Remember to handle the edge cases.


### Solution {#solution}


#### Solution 1: 2D DP {#solution-1-2d-dp}

-   Inplace DP

<!--listend-->

```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m = len(grid)
        n = len(grid[0])

        for i in range(m):
            for j in range(n):
                if i == 0:
                    if j == 0:
                        continue
                    else:
                        grid[i][j] += grid[i][j-1]
                else:
                    if j == 0:
                        grid[i][j] += grid[i-1][j]
                    else:
                        grid[i][j] += min(grid[i-1][j], grid[i][j-1])
        return grid[-1][-1] if m and n else 0


grid = [[1,3,1],[1,5,1],[4,2,1]]

print(Solution().minPathSum(grid))
```

-   Additional DP with auxiliary columns

<!--listend-->

```python
import sys
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m = len(grid)
        n = len(grid[0])

        dp = [[ 0 for i in range(n+1)] for j in range(m+1)]

        for i in range(len(dp)):
          dp[i][0] = sys.maxsize

        for i in range(len(dp[0])):
            dp[0][i] = sys.maxsize

        dp[1][1] = grid[0][0]

        for i in range(1, m+1):
            for j in range(1, n+1):
                if i == 1 and j == 1:
                    continue
                else:
                    dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i-1][j-1]


        return dp[-1][-1] if m and n else 0


grid = [[1,3,1],[1,5,1],[4,2,1]]

print(Solution().minPathSum(grid))
```


#### Solution 2: 1D DP {#solution-2-1d-dp}

```python
import sys
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m = len(grid)
        n = len(grid[0])

        dp = [sys.maxsize for i in range(n+1)]
        dp[1] = grid[0][0]

        for i in range(m):
            for j in range(n):
              if i == 1 and j == 1:
                  continue
              else:
                dp[j+1] = min(dp[j+1], dp[j]) + grid[i][j]

        return dp[-1] if m and n else 0


grid = [[1,3,1],[1,5,1],[4,2,1]]

print(Solution().minPathSum(grid))
```


## [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) {#70-dot-climbing-stairs}


### Problem {#problem}

```text
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:

Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
Example 2:

Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```


### Notes {#notes}

The distinct ways to take n stair cases:

1.  take one step at last, the distinct ways to take n-1 stair cases  -> f(n-1) ways
2.  take two steps at last, the distinct ways to take n-2 stair cases -> f(n-2) ways

So f(n) = f(n-1) + f(n-2)


### Solution {#solution}

```python
class Solution():
    def climbStairs(self, n):
        if n < 2:
            return n

        dp = [0] * n

        dp[0] = 1
        dp[1] = 2

        for i in range(2, n):
            dp[i] = dp[i-1] + dp[i-2]

        return dp[-1]
```


## [91. Decode Ways](https://leetcode.com/problems/decode-ways) {#91-dot-decode-ways}


### Problem {#problem}

```text
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given a non-empty string containing only digits, determine the total number of ways to decode it.

Example 1:

Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
Example 2:

Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```


### Notes {#notes}

DP problem.

1.  Initialize dp array with dp[0] = 1 as padding, the rest of them are 0.
2.  Start from the first index of the string.
    1.  If dp[i] is in range 1 to 9, dp[i] = dp[i-1]. The ways of decode will not increase, if it is 0, it remains 0.
    2.  If dp[i] is in range 10 to 26, dp[i] += dp[i-1]. The ways of decode increase by one, if it is 00, it remains 0.

**Important**:

1.  Corner cases: "0" -> 0, "1002" -> 0
2.  Notice the padding


### Solution {#solution}

```python
class Solution():
    def numsDecodings(self, s):

        if not s:
          return 0

        n = len(s)

        dp = [0] * (n + 1)

        dp[0] = 1

        for i in range(1, n+1):

            if s[i-1: i] != '0':
                dp[i] = dp[i-1]

            if i != 1 and '10' <= s[i-2:i] <= '26':
                dp[i] += dp[i-2]

        return dp[-1]
```


## [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) {#509-dot-fibonacci-number}


### Problem {#problem}

```text
The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), for N > 1.
Given N, calculate F(N).



Example 1:

Input: 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
Example 2:

Input: 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
Example 3:

Input: 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```


### Notes {#notes}

DP Problem.

**Important**:

Note how long is the dp array. It shoud be N+1, since we start with the number 0.


### Solution {#solution}

```python
class Solution(object):
    def fib(self, N):
        """
        :type N: int
        :rtype: int
        """
        if N < 2:
            return N

        dp = [0] * (N + 1)

        dp[0] = 0
        dp[1] = 1

        for i in range(2, N + 1):
            dp[i] = dp[i - 1] + dp[i - 2]

        return dp[-1]
```


## [75. Sort Colors](https://leetcode.com/problems/sort-colors/) {#75-dot-sort-colors}


### Problem {#problem}

```text
Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

Example:

Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
Follow up:

A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
Could you come up with a one-pass algorithm using only constant space?
```


### Notes {#notes}


#### First attempt is to use two pointer. {#first-attempt-is-to-use-two-pointer-dot}

There is a but a corner case: when two pointer are both at 1. How should we move the pointer.

We can use a another `while` unter this situation, initialize another pointer and search for 0 or 2 between
these two pointers. See Soution 1


#### Three Way Partition {#three-way-partition}

three pointer, one for each.

**Important**:

Notice the condition for `while`: while mi <= hi

the middle move forward:

1.  middle == 0, switch with left one, left + 1, middle + 1
2.  middle == 1, continue
3.  middle == 2, swtich with right one, right - 1


### Solution {#solution}


#### Solution 1 {#solution-1}

```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """

        lo = 0
        hi = len(nums) - 1

        while (lo < hi):
            if nums[lo] == 0:
                lo += 1
            elif nums[hi] == 2:
                hi -= 1
            elif nums[lo] == 1 and nums[hi] == 1:
                mi = lo + 1
                while (mi < hi):
                    if nums[mi] == 2 or nums[mi] == 0:
                        nums[mi], nums[hi] = nums[hi], nums[mi]
                        break
                    else:
                        mi += 1
                if mi == hi:
                    return
            else:
                nums[lo], nums[hi] = nums[hi], nums[lo]
```


#### Solution 2: Three way partition {#solution-2-three-way-partition}

Notice the condition for `while`:

It has to be <=.
Because you every element behind hi, you have seen it.
But not the element at hi. You have to check it at last.

```python
class Solution(object):
    def sortColors(self, nums):

        lo, mi, hi = 0, 0, len(nums) - 1

        while mi <= hi: # Nottice!: here has to be <=
            if nums[mi] == 0:
                nums[mi], nums[lo] = nums[lo], nums[mi]
                lo += 1
                mi += 1
            elif nums[mi] == 2:
                nums[mi], nums[hi] = nums[hi], nums[mi]
                hi -= 1
            else:
                mi += 1
```


## 78 - Subsets {#78-subsets}


### Problem {#problem}

[leetcode](https://leetcode.com/problems/subsets/)

```text
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:

Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```


### Notes {#notes}

Three strategies to solve a subset problem:

Recursion, Backtracking, Bitmask


#### Recursion {#recursion}

Iterative version:

```text
Start from empty array [[]].

Step 1: Take 1 into consideration, and add 1 to existing array [[], [1]]

Step 2: Take 2 into consideration, and add 2 to existing array [[], [1], [2], [1, 2]]

Step 3: Take 3 into consideration, and add 3 to existing array [[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]
```

DFS version:

```text
[[]]
[[], [1]],
[[], [1], [1, 2]]
[[], [1], [1, 2], [1, 2, 3]]
[[], [1], [1, 2], [1, 2, 3], [1, 3]]
[[], [1], [1, 2], [1, 2, 3], [1, 3], [2]]
[[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3]]
[[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3], [3]]
```


#### Backtrack {#backtrack}

Backtrack needs to know how many steps it shoud take to end.

```text
[1, 2, 3]

Step 1: subsets of length 0: [[]]
Step 2: subsets of length 1: [[1], [2], [3]]
Step 3: subsets of length 2: [[1, 2], [2, 3], [1, 3]]
Step 4: subsets of length 3: [[1, 2, 3]]
```


#### Bitmask {#bitmask}

> The idea is that we map each subset to a bitmask of length n,
> where 1 on the ith position in bitmask means the presence of nums[i] in the subset,
> and 0 means its absence.

[1, 2, 3]

```text
[0, 0, 0] -> []
[0, 0, 1] -> [3]
[0, 1, 0] -> [2]
[1, 0, 0] -> [1]
[1, 0, 1] -> [1, 3]
[0, 1, 1] -> [2, 3]
[1, 1, 0] -> [1, 2]
[1, 1, 1] -> [1, 2, 3]
```


### Solution {#solution}


#### Solution 1: dfs (recursion) {#solution-1-dfs--recursion}

```python
class Solution(object):
    def subsets(self, nums):
        res = []
        self.dfs(sorted(nums), 0, [], res)
        return res

    def dfs(self, nums, index, path, res):
        res.append(path)
        for i in range(index, len(nums)):
            self.dfs(nums, i + 1, path + [nums[i]], res)

print(Solution().subsets([1, 2, 3]))
```


#### Solution 2: iterative {#solution-2-iterative}

```python
class Solution:

    def subsets(self, nums):
        res = [[]]
        for i in sorted(nums):
            res += [item+[i] for item in res]

        return res

print(Solution().subsets([1, 2, 3]))
```


#### Solution 3: backtrack {#solution-3-backtrack}

```python

class Solution(object):

    def subsets(self, nums):
        output = []
        for k in range(0, len(nums)+1):
            temp = []
            self.backtrack(0, k, nums, temp, output)

        return output

    def backtrack(self, begin, length, nums, temp, output):

        if length == len(temp):
            output.append(temp[:])

        for i in range(begin, len(nums)):
            temp.append(nums[i])
            self.backtrack(i+1, length, nums, temp, output)
            temp.pop()


print(Solution().subsets([1, 2, 3]))
```


#### Solution 4: bitmask {#solution-4-bitmask}

```python

class Solution():
  def subsets(self, nums):
    n = len(nums)
    output = []
    for i in range(2**n, 2**(n+1)):
      bitmask = bin(i)[3:]
      output.append([nums[i] for i in range(n) if bitmask[i] == '1' ])

    return output
```


## 79 - Word Search {#79-word-search}


### Problem {#problem}

[leetcode](https://leetcode.com/problems/word-search/)

```text
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

Example:

board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```


### Notes {#notes}


### Solution {#solution}


#### Solution 1: Backtrack {#solution-1-backtrack}

```python
class Solution:
    def exist(self, board, word):
        m = [[0 for j in range(len(board[0]))] for i in range(len(board))]
        for i in range(len(board)):
            for j in range(len(board[0])):
                if self.exist_rec(board, word, i, j, m):
                    return True
        return False

    def exist_rec(self, board, word, i, j, m):
        if len(word) == 0:
            return True

        if i < 0 or j < 0 or i >= len(board) or j >= len(board[0]):
            return False

        if board[i][j] == word[0] and m[i][j] == 0:
            m[i][j] = 1

            if self.exist_rec(board, word[1:], i - 1, j, m) or \
            self.exist_rec(board, word[1:], i + 1, j, m) or \
            self.exist_rec(board, word[1:], i, j - 1, m) or \
            self.exist_rec(board, word[1:], i, j + 1, m):
                return True
            else:
                m[i][j] = 0

        return False

board = [["A", "B", "C", "E"], ["S", "F", "C", "S"], ["A", "D", "E", "E"]]
word = "ABCCED"
```
