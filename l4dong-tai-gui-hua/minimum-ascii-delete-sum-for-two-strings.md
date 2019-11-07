# Minimum ASCII Delete Sum for Two Strings

Given two strings`s1, s2`, find the lowest ASCII sum of deleted characters to make two strings equal.

**Example 1:**

```text
Input: s1 = "sea", s2 = "eat"Output: 231Explanation: Deleting "s" from "sea" adds the ASCII value of "s" (115) to the sum.Deleting "t" from "eat" adds 116 to the sum.At the end, both strings are equal, and 115 + 116 = 231 is the minimum sum possible to achieve this.
```

**Example 2:**

```text
Input: s1 = "delete", s2 = "leet"Output: 403Explanation: Deleting "dee" from "delete" to turn the string into "let",adds 100[d]+101[e]+101[e] to the sum.  Deleting "e" from "leet" adds 101[e] to the sum.At the end, both strings are equal to "let", and the answer is 100+101+101+101 = 403.If instead we turned both strings into "lee" or "eet", we would get answers of 433 or 417, which are higher.
```

**Note:**

`0<s1.length, s2.length<= 1000`

All elements of each string will have an ASCII value in`[97, 122]`

.分析

2个序列比较的二维dp，注意初始化，dp\[i\]\[0\]和dp\[0\]\[j\]是累计和

```text
class Solution:    def minimumDeleteSum(self, s1: str, s2: str) -> int:        n,m = len(s1),len(s2)        f = [[float('inf')]*(m+1) for _ in range(n+1)]        f[0][0] = 0        for i in range(1,n+1):            f[i][0] = f[i-1][0] + ord(s1[i-1])            for j in range(1,m+1):                f[0][j] = f[0][j-1] + ord(s2[j-1])                if s1[i-1] == s2[j-1]:                    f[i][j] = f[i-1][j-1]                else:                    f[i][j] = min(f[i-1][j] + ord(s1[i-1]), f[i][j-1] + ord(s2[j-1]))        return f[n][m]
```

