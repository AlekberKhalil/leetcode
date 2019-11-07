# Minimum Add to Make Parentheses Valid

Given a string `S`of`'('`and`')'`parentheses, we add the minimum number of parentheses \(`'('`or`')'`, and in any positions \) so that the resulting parentheses string is valid.

Formally, a parentheses string is valid if and only if:

* It is the empty string, or
* It can be written as

  `AB`

   \(

  `A`

  concatenated with

  `B`

  \), where

  `A`

  and

  `B`

  are valid strings, or

* It can be written as

  `(A)`

  , where

  `A`

  is a valid string.

Given a parentheses string, return the minimum number of parentheses we must add to make the resulting string valid.

**Example 1:**

```text
Input: "())"Output: 1
```

**Example 2:**

```text
Input: "((("Output: 3
```

**Example 3:**

```text
Input: "()"Output: 0
```

**Example 4:**

```text
Input: "()))(("Output: 4
```

分析

注意这里不能单纯比较\(\)个数，也要比较出场顺序。所以counter是算顺序，）stk是算残余多少的 （

```text
class Solution:    def minAddToMakeValid(self, S):        """        :type S: str        :rtype: int        """        left = right = 0        for i in S:            if i == '(':                left +=1            elif left<=0:#都平衡了，再多个)就不行了 所以要<=                right+=1            else:                left -= 1        return left + right
```

