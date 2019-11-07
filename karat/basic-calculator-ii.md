# Basic Calculator II

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only**non-negative**integers,`+`,`-`,`*`,`/`operators and empty spaces. The integer division should truncate toward zero.

**Example 1:**

```text
Input: "3+2*2"Output: 7
```

**Example 2:**

```text
Input: " 3/2 "Output: 1
```

**Example 3:**

```text
Input: " 3+5 / 2 "Output: 5
```

分析

计算机的题目好像都是op在前，数字带着op走，或者入栈，或者入expression带着走。

注意这里2个陷阱：最后一个数也要加入栈，所以ii == n-1 不是else

/的时候 3/2和-3/2要额外处理。用ceil和floor

```text
class Solution:    def calculate(self, s):        """        :type s: str        :rtype: int        """        stack = []        op ='+'        snum =''        n = len(s)        res = 0        for ii,i in enumerate(s):            if i.isdigit():                snum += i            if i in "+-*/" or ii == n-1:                if op == '+':                    stack.append(int(snum))                elif op == '-':                    stack.append(-int(snum))                elif op == '*':                    cur = stack.pop()                    stack.append(cur*int(snum))                elif op == '/':                    cur = stack.pop()/int(snum)                    stack.append(math.floor(cur)) if cur >= 0 else stack.append(math.ceil(cur))                snum =''                op = i        for i in stack :            res += i        return res
```

