# Palindromic Substrings\(dp\)

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**

```text
Input:
 "abc"

Output:
 3

Explanation:
 Three palindromic strings: "a", "b", "c".
```

**Example 2:**

```text
Input:
 "aaa"

Output:
 6

Explanation:
 Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

**Note:**

1. The input string length won't exceed 1000.

分析

dp， 注意count 用法 dp.count\(1\)不行 count只能用在一元数组

```text
class Solution:
    def countSubstrings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s or len(s) == 0:
            return 0
        n = len(s)
        dp = [[0]*n for _ in range(n)]
        cnt = dp[0][0] = 1
        for i in range(1,n):
            dp[i][i] = 1
            cnt += 1
            for j in range(i):
                if s[i] == s[j] and (i == 1 + j or dp[j+1][i-1] == 1):
                    dp[j][i] = 1
                    cnt += 1
        return cnt
```

