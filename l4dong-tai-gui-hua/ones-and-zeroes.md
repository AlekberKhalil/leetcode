# Ones and Zeroes

In the computer world, use restricted resource you have to generate maximum benefit is what we always want to pursue.

For now, suppose you are a dominator of**m**`0s`and**n**`1s`respectively. On the other hand, there is an array with strings consisting of only`0s`and`1s`.

Now your task is to find the maximum number of strings that you can form with given**m**`0s`and**n**`1s`. Each`0`and`1`can be used at most**once**.

**Note:**

1. The given numbers of

   `0s`

   and

   `1s`

   will both not exceed

   `100`

2. The size of given string array won't exceed

   `600`

   .

**Example 1:**

```text
Input:
 Array = {"10", "0001", "111001", "1", "0"}, m = 5, n = 3

Output:
 4


Explanation:
 This are totally 4 strings can be formed by the using of 5 0s and 3 1s, which are “10,”0001”,”1”,”0”
```

**Example 2:**

```text
Input:
 Array = {"10", "0", "1"}, m = 1, n = 1

Output:
 2


Explanation:
 You could form "10", but then you'd have nothing left. Better form "0" and "1".
```

分析

01背包，把value拆成0,1，变成2个循环而已。记得倒序

这里value范围必须是cnt0-&gt;m cnt1&gt;n？？？

```text
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        if not m or not n:
            return m|n
        ll = len(strs)
        dp = [[0]*(m+1) for _ in range(n+1)]
        def count(s):
            return sum(1 for c in s if c == '0'), sum(1 for c in s if c == '1')

        for k in range(ll):
            cnt0,cnt1 = count(strs[k])
            for x in range(n,cnt1-1,-1):#1
                for y in range(m,cnt0-1,-1):#0                    
                    #if x>=cnt1 and y>=cnt0:
                    dp[x][y] = max(dp[x][y],dp[x-cnt1][y-cnt0]+1)
        return dp[n][m]
```

