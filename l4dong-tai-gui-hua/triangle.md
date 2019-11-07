# Triangle

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```text
[     [2],    [3,4],   [6,5,7],  [4,1,8,3]]
```

The minimum path sum from top to bottom is`11`\(i.e.,2+3+5+1= 11\).

分析

这里没判断triangle的null和大小也行？

从底部向上，选更小那个加

类似minimal path sum, 要求最小的，row0 col0都设为最大防止干扰。dp还是m\*n ： f = \[\[float\('inf'\)\] \* \(m + 1\) for \_ in range\(n+1\)\]

```text
f[i][j] = Math.min(f[i + 1][j], f[i + 1][j + 1]) + triangle.get(i).get(j);
```

```text
class Solution {    public int minimumTotal(List<List<Integer>> triangle) {        int n = triangle.size();        int[][] f = new int[n][triangle.get(n-1).size()];        for(int i = 0; i < triangle.get(n - 1).size(); i ++){            f[n-1][i] = triangle.get(n - 1).get(i);        }        for(int i = n - 2; i >= 0; i --){            for(int j = 0; j < i + 1; j ++){                f[i][j] = Math.min(f[i + 1][j], f[i + 1][j + 1]) + triangle.get(i).get(j);            }        }        return f[0][0];    }}
```

