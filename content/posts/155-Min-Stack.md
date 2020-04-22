+++
title = "155 - Min Stack"
date = 2020-04-10T20:47:00+02:00
lastmod = 2020-04-10T20:47:45+02:00
tags = ["easy", "stack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problemset/all/?search=Min%20Stack)


## Problem {#problem}

```text
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.


Example:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```


## Solution {#solution}

Use a second stack to keep track of the min value.
Pay attention to the return value. Remember to return None when there is no result.

```python
class MinStack:
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []
        self.min = []

    def push(self, x: int) -> None:
        self.stack.append(x)
        if not self.getMin() or self.getMin() >= x:
            self.min.append(x)

    def pop(self) -> None:
        if self.stack:
            x = self.stack.pop()
            if x == self.min[-1]:
                self.min.pop()

    def top(self) -> int:
        if self.stack:
            return self.stack[-1]
        else:
            return None

    def getMin(self) -> int:
        if self.min:
            return self.min[-1]
        else:
            return None
```
