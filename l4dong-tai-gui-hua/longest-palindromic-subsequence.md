# Longest Palindromic Subsequence

Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

**Example 1:**  
Input:

```text
"bbbab"
```

Output:

```text
4
```

One possible longest palindromic subsequence is "bbbb".

**Example 2:**  
Input:

```text
"cbbd"
```

Output:

```text
2
```

One possible longest palindromic subsequence is "bb".

分析

```text
dp[i,j]当前范围内最大的回文。
State transition:
dp[i][j] = dp[i+1][j-1] + 2 if s.charAt(i) == s.charAt(j)
otherwise, dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1])
Initialization: dp[i][i] = 1
```

```text
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        n = len(s)
        f = [[0]*(n+1) for _ in range(n+1)]

        for i in reversed(range(n+1)):
            f[i][i] =1
            for j in range(i+1,n+1):                
                if s[i-1] == s[j-1]:
                    f[i][j] = f[i+1][j-1]+2
                else:
                    f[i][j] = max(f[i+1][j],f[i][j-1])

        return f[1][n]
```

用start 和len来Loop

```text
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        n = len(s)
        f = [[0]*(n+1) for _ in range(n+1)]
        for i in range(n+1):
            f[i][i] = 1

        for ln in range(1,n+1):            
            for start in range(1,n+1-ln):                
                if s[start-1] == s[start+ln-1]:
                    f[start][start+ln] = f[start+1][start+ln-1]+2
                else:
                    f[start][start+ln] = max(f[start+1][start+ln],f[start][start+ln-1])

        return f[1][n]
```

