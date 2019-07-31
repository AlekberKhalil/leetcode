# Minimum Path Sum

Given amxngrid filled with non-negative numbers, find a path from top left to bottom right whichminimizesthe sum of all numbers along its path.

**Note:**You can only move either down or right at any point in time.

分析

动态分布，从左或者上来的.

因为是最小，所以第一行/列的初始化要是max才能保证不干扰答案。还有f\[1\]\[1\] = grid\[0\]\[0\]。 画图就知道

```text
class Solution {
    public int minPathSum(int[][] grid) {
        if(grid == null || grid.length == 0 || grid[0] == null || grid[0].length == 0)
            return 0;
        int n = grid.length;
        int m = grid[0].length;
        int[][] f = new int[n + 1][m + 1];
        for(int i = 1; i <= n; i ++){
            f[i][0] = Integer.MAX_VALUE;
            for(int j = 1; j <= m; j ++){
                f[0][j] = Integer.MAX_VALUE;
                if(i == 1 && j == 1){
                    f[i][j] = grid[i - 1][j - 1];
                }else
                f[i][j] = Math.min(f[i - 1][j], f[i][j - 1]) + grid[i - 1][j - 1];
            }
        }
        return f[n][m];
    }
}
```

