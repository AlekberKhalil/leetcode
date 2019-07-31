# k Sum I&II

Given_n\_distinct positive integers, integer\_k_\(_k_&lt;=_n_\) and a number_target_.

Find \_k \_numbers where sum is target. Calculate how many solutions there are?

**Example**

Given`[1,2,3,4]`, k =`2`, target =`5`.

There are`2`solutions:`[1,4]`and`[2,3]`.

Return`2`.

分析：

动态规划。I求个数用动归，II求所有solution用搜索（DFS）。不懂为什么初始化是1

解法：

```text
    public int kSum(int[] A, int k, int target) {
        // write your code here
        if(A== null || A.length == 0)
            return 0;
        int n = A.length;
        int[][][] sum = new int[n+1][k+1][target+1];
        sum[0][0][0] = 1;
        for(int i = 1; i <= n; i ++){
            sum[i][0][0] = 1;
            for(int j = 1; j <= k; j ++){
                for(int t = 0; t <= target; t ++){
                    if(A[i-1] <= t){
                        sum[i][j][t] = sum[i-1][j-1][t - A[i-1]];
                    }
                    sum[i][j][t] += sum[i-1][j][t];
                }
            }
        }
        return sum[n][k][target];
    }
```

## k Sum II

Find all possible k integers where their sum is target.

分析：

DFS

