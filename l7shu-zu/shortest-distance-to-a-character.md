# Shortest Distance to a Character

Given a string`S` and a character`C`, return an array of integers representing the shortest distance from the character`C`in the string.

**Example 1:**

```text
Input: S = "loveleetcode", C = 'e'Output: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]
```

**Note:**

```text
S string length is in [1, 10000].C is a single character, and guaranteed to be in string S.All letters in S and C are lowercase.
```

分析

左右各遍历一遍，得到min distance

```text
class Solution:    def shortestToChar(self, S: str, C: str) -> List[int]:                ll = len(S)        res = [ll]*ll        pos = -ll #注意此处取值弄成最大就好        for i in range(ll):            if S[i] == C:                pos = i                res[i] = 0            else:                res[i] = min(res[i],abs(pos - i))        for i in range(ll-1,-1,-1):            if S[i] == C:                pos = i                res[i] = 0            else:                res[i] = min(res[i],abs(pos - i))        return res
```

