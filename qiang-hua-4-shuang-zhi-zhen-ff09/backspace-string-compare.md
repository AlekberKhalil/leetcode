# Backspace String Compare

Given two strings `S` and`T`, return if they are equal when both are typed into empty text editors.`#`means a backspace character.

**Example 1:**

```text
Input: S = "ab#c", T = "ad#c"Output: trueExplanation: Both S and T become "ac".
```

**Example 2:**

```text
Input: S = "ab##", T = "c#d#"Output: trueExplanation: Both S and T become "".
```

**Example 3:**

```text
Input: S = "a##c", T = "#a#c"Output: trueExplanation: Both S and T become "c".
```

**Example 4:**

```text
Input: S = "a#c", T = "b"Output: falseExplanation: S becomes "c" while T becomes "b".
```

Note:

```text
1 <= S.length <= 2001 <= T.length <= 200S and T only contain lowercase letters and '#' characters.
```

分析

栈内只加字母，不加\#，遇到‘\#’，抵消栈内char，字母的话加入。 最后比较S,T剩下的东西

```text
class Solution:    def backspaceCompare(self, S: str, T: str) -> bool:        return self.getChar(S) == self.getChar(T)    def getChar(self, S: str) -> str:        stack = []        for i in S:            if stack and i == '#':                stack.pop()            elif i.isalpha():                stack.append(i)        return ''.join(stack)
```

