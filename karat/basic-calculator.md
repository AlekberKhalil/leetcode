# Basic Calculator

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open`(`and closing parentheses`)`, the plus`+`or minus sign`-`,**non-negative**integers and empty spaces.

**Example 1:**

```text
Input: "1 + 1"Output: 2
```

**Example 2:**

```text
Input: " 2-1 + 2 "Output: 3
```

**Example 3:**

```text
Input: "(1+(4+5+2)-3)+(6+8)"Output: 23
```

  
**分析**

带括号，所以每次相乘带sign，遇到括号把+1/-1sign压入，再压入前面result。遇到\)就弹出站

```text
class Solution:    def calculate(self, s):        """        :type s: str        :rtype: int        """        stack = []        num = 0        res = 0        sign = 1        for ii, i in enumerate(s):            if i.isdigit():                num = num * 10 + int(i)            elif i == '+':                                res += num * sign                sign = 1                num=0            elif i == '-':                               res += num * sign                sign = -1                num = 0            elif i == '(':                stack.append(res)                stack.append(sign)                res = 0                sign = 1            elif i == ')':                                res += num * sign                res = stack.pop() * res + stack.pop()                num = 0        if num:            res += num * sign        return res
```

