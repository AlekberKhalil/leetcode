# Ugly Number II

Write a program to find the`n`-th ugly number.

Ugly numbers are**positive numbers**whose prime factors only include`2, 3, 5`.

**Example:**

```text
Input: n = 10Output: 12Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
```

**Note:**

1. `1`

   is typically treated as an ugly number.

2. `n`

   **does not exceed 1690**

分析

2，3，5 3个数字分别计个数，最后N=N2+N3+N5

loop i，每次新i值取3个数能到的最小值，然后把那个数的cnt++，每个N2，N3,N5等于是断点，决定踩哪个断点到最新的min。

```text
class Solution:    def nthUglyNumber(self, n: int) -> int:        i2=i3=i5=0        dp = [0]*n        dp[0]=1        for i in range(1,n):            dp[i] = min(dp[i2]*2,dp[i3]*3,dp[i5]*5)            if dp[i] == dp[i2]*2:                i2+=1            if dp[i] == dp[i3]*3:                i3+=1            if dp[i] == dp[i5]*5:                i5+=1        return dp[n-1]
```

