# Backpack II

Given_n\_items with size Aiand value Vi, and a backpack with size\_m_. What's the maximum value can you put into the backpack?

## Notice

You cannot divide item into small pieces and the total size of items you choose should smaller or equal to m.

**Example**

Given 4 items with size`[2, 3, 5, 7]`and value`[1, 5, 2, 4]`, and a backpack with size`10`. The maximum value is`9`.

分析

背包DP

```text
    public int backPackII(int m, int[] A, int[] V) {        // write your code here        int x = A.length;        int[][] dp = new int[x+1][m+1];        for(int i = 1; i <= x; i++){            dp[i][0] = 0;            for(int j = 1; j <= m; j++){                dp[0][j] = 0;                if(j >= A[i-1]){                    dp[i][j] = dp[i-1][j-A[i-1]] + V[i-1];                }                dp[i][j] = Math.max(dp[i][j], dp[i-1][j]);            }        }        return dp[x][m];    }
```

