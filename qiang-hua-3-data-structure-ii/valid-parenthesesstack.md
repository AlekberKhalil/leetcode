# Valid Parentheses（stack\)

Given a string containing just the characters`'('`,`')'`,`'{'`,`'}'`,`'['`and`']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```text
Input: "()"Output: true
```

**Example 2:**

```text
Input: "()[]{}"Output: true
```

**Example 3:**

```text
Input: "(]"Output: false
```

**Example 4:**

```text
Input: "([)]"Output: false
```

**Example 5:**

```text
Input: "{[]}"Output: true
```

分析

loop input, stack 只进头不进尾，遇头压入遇尾弹出计算。

最后判断栈是否空

```text
class Solution:    def isValid(self, s):        """        :type s: str        :rtype: bool        """        stack = []        left = "({["        right = ")}]"        for i in s:            if i in left:                stack.append(i)            else:                if not stack or stack[-1] != left[right.index(i)]:                    return False                else:                    stack.pop()        return not stack
```

