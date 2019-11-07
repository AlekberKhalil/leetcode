# Ternary Expression Parser

Given a string representing arbitrarily nested ternary expressions, calculate the result of the expression. You can always assume that the given expression is valid and only consists of digits`0-9`,`?`,`:`,`T`and`F`\(`T`and`F`represent True and False respectively\).

**Note:**

1. The length of the given string is ≤ 10000.
2. Each number will contain only one digit.
3. The conditional expressions group right-to-left \(as usual in most languages\).
4. The condition will always be either

   `T`

   or

   `F`

   . That is, the condition will never be a digit.

5. The result of the expression will always evaluate to either a digit

   `0-9`

   ,

   `T`

   or

   `F`

   .

**Example 1:**

```text
Input: "T?2:3"Output: "2"Explanation: If true, then result is 2; otherwise result is 3.
```

**Example 2:**

```text
Input: "F?1:T?4:5"Output: "4"Explanation: The conditional expressions group right-to-left. Using parenthesis, it is read/evaluated as:             "(F ? 1 : (T ? 4 : 5))"                   "(F ? 1 : (T ? 4 : 5))"          -> "(F ? 1 : 4)"                 or       -> "(T ? 4 : 5)"          -> "4"                                    -> "4"
```

**Example 3:**

```text
Input: "T?T?F:5:3"Output: "F"Explanation: The conditional expressions group right-to-left. Using parenthesis, it is read/evaluated as:             "(T ? (T ? F : 5) : 3)"                   "(T ? (T ? F : 5) : 3)"          -> "(T ? F : 3)"                 or       -> "(T ? F : 5)"          -> "F"                                    -> "F"
```

分析

用regex配对，自己做的

```text
import reclass Solution:    def parseTernary(self, expression: str) -> str:        return self.dfs(expression)    def dfs(self, expr: str) -> str:        if len(expr) == 5 and self.isTernary(expr):            return self.evalexpr(expr)        for i in reversed(range(len(expr))):            e = expr[i-4:i+1]            if self.isTernary(e):                                return self.dfs(expr[:i-4]+self.evalexpr(e)+expr[i+1:])                   def isTernary(self,expr:str) ->bool:        return re.match(r'^(T|F)\?[TF0-9]:[TF0-9]$',expr)    def evalexpr(self,expr:str) -> str:        return expr[2]  if expr[0] == 'T' else expr[-1]
```

DFS

找到数量相同的?和: 就可以开始切分dfs，参数是start and end

```text
import reclass Solution:    def parseTernary(self, expression: str) -> str:        return self.dfs(expression,0,len(expression)-1)    def dfs(self, expr: str, s:int, e:int) -> str:        if s == e:            return expr[s]        cnt = 0        i = 0        for i in range(s,e+1):            if expr[i] == '?':                cnt += 1            elif expr[i] == ':':                cnt -= 1                if cnt == 0:                    break        return self.dfs(expr, s+2,i-1) if expr[s] == 'T' else self.dfs(expr, i+1, e)
```

stack

遇到栈顶问号，就判断当前C是T/F，弹出4个，弹入结果

```text
class Solution:    def parseTernary(self, expression: str) -> str:        stack = []        for c in reversed(expression):            if stack and stack[-1] == '?':                stack.pop()                c1 = stack.pop()                stack.pop()                c2 = stack.pop()                stack.append(c1) if c == 'T' else stack.append(c2)            else:                stack.append(c)        return stack[0]
```

