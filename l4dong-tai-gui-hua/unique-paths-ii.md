# Unique Paths II

Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as`1`and`0`respectively in the grid.

For example,

There is one obstacle in the middle of a 3x3 grid as illustrated below.

```text
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```

The total number of unique paths is`2`.

分析

当前点可达时，两个方向的path相加，不可达则reset为0。

如果初始状态可达，则f\[1\]\[1\]是1，要单独判断。

```text
class Solution {
    public int uniquePathsWithObstacles(int[][] board) {
        if(board == null || board.length == 0 || board[0] == null || board[0].length == 0)
            return 0;
        int n = board.length;
        int m = board[0].length;
        int[][] f= new int[n + 1][m + 1];
        for(int i = 1; i <= n; i ++){               
            for(int j = 1; j <= m; j ++){                            
                if(i == 1 && j == 1)
                    f[1][1] = board[i - 1][j - 1] == 0 ? 1 : 0;
                else
                    f[i][j] = board[i - 1][j - 1] == 0 ? f[i-1][j] + f[i][j - 1] : 0;
            }            
        }
        return f[n][m];
    }
}
```

