# Number of Distinct Islands

Given a non-empty 2D array`grid`of 0's and 1's, an**island**is a group of`1`'s \(representing land\) connected 4-directionally \(horizontal or vertical.\) You may assume all four edges of the grid are surrounded by water.

Count the number of**distinct**islands. An island is considered to be the same as another if and only if one island can be translated \(and not rotated or reflected\) to equal the other.

**Example 1:**

```text
11000
11000
00011
00011
```

Given the above grid map, return

`1`

.

**Example 2:**

```text
11011
10000
00001
11011
```

Given the above grid map, return

`3`

.

Notice that:

```text
11
1
```

and

```text
 1
11
```

are considered different island shapes, because we do not consider reflection / rotation.

**Note:**The length of each dimension in the given`grid`does not exceed 50.

分析

和题二的区别就是二8个方向，这里只要相同。

每次dfs得到一个联通块，然后在本块里的所有坐标-minx, -miny。加入set。结果就set长度

```text
class Solution:
    def numDistinctIslands(self, grid: List[List[int]]) -> int:
        if not grid or not grid[0]:
            return 0
        n, m = len(grid), len(grid[0])        
        d = [-1, 0, 1, 0, -1]

        ss = set()

        def dfs(i,j,q):
            q.append((i,j))
            if grid[i][j] == -1:
                return
            grid[i][j] = -1
            nxy = [(i + d[k], j + d[k + 1]) for k in range(4)]
            for nx,ny in nxy:
                if 0<= nx < n and 0<= ny< m and grid[nx][ny] == 1:
                    q.append((nx,ny))
                    dfs(nx,ny,q)

        for i in range(n):        
            for j in range(m):
                if grid[i][j] == 1:
                    q = []
                    dfs(i, j, q)
                    if q:
                        mini,minj = min(x for x,y in q), min(y for x,y in q)
                        f = tuple(sorted((x-mini, y-minj) for x, y in q))
                        ss.add(f)

        return len(ss)
```

