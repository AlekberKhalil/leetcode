# Unique Paths

A robot is located at the top-left corner of amxngrid \(marked 'Start' in the diagram below\).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid \(marked 'Finish' in the diagram below\).

How many possible unique paths are there?

![](https://leetcode.com/static/images/problemset/robot_maze.png)

Above is a 3 x 7 grid. How many possible unique paths are there?

**Note:**mandnwill be at most 100.

分析

也是dp， 第一行/列是0，f\[1\]\[1\]是1。画图就知道

```text
class Solution {    public int uniquePaths(int m, int n) {        if(m == 0 || n == 0)            return 0;        int[][] f = new int[n + 1][m + 1];        for(int i = 1; i <= n; i ++){            // f[i][0] = Integer.MAX_VALUE;            for(int j = 1; j <= m; j ++){                // f[0][j] = Integer.MAX_VALUE;            if(i == 1 && j == 1){                f[i][j] = 1;            }else                f[i][j] = f[i - 1][j] + f[i][j - 1];            }        }        return f[n][m];    }}
```

