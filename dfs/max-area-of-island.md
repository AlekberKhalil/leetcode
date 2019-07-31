# Max Area of Island

Given a non-empty 2D array`grid`of 0's and 1's, an**island**is a group of`1`'s \(representing land\) connected 4-directionally \(horizontal or vertical.\) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. \(If there is no island, the maximum area is 0.\)

**Example 1:**

```text
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,
1
,0,
1
,0,0],
 [0,1,0,0,1,1,0,0,
1
,
1
,
1
,0,0],
 [0,0,0,0,0,0,0,0,0,0,
1
,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

Given the above grid, return

`6`

. Note the answer is not 11, because the island must be connected 4-directionally.

**Example 2:**

```text
[[0,0,0,0,0,0,0,0]]
```

Given the above grid, return

`0`

.

**Note:**The length of each dimension in the given`grid`does not exceed 50.

dfs

每次dfs是一个连通块，计算每块里面多少个。 这里visited直接设置Matrix = -1

```text
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        if not grid or not grid[0]:
            return 0
        n,m = len(grid),len(grid[0])

        d = [-1, 0, 1, 0, -1]

        def dfs(i,j):
            nonlocal cnt
            if grid[i][j] != 1:
                return
            grid[i][j] = -1
            for x, y in [(i + d[k], j + d[k + 1]) for k in range(4)]:
                if 0 <= x < n and 0 <= y < m and grid[x][y] == 1:
                    cnt += 1
                    dfs(x,y)

        res = 0            
        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                    cnt = 1
                    dfs(i,j)
                    res = max(res,cnt)
        return res
```

dfs II

```text
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        if not grid or not grid[0]:
            return 0
        n,m = len(grid),len(grid[0])
        d = [-1,0,1,0,-1]
        def dfs(x,y):
            grid[x][y] = -1
            cnt = 1
            for nx,ny in [(x+d[i],y+d[i+1]) for i in range(4)]:
                if 0 <= nx < n and 0 <= ny < m and grid[nx][ny] == 1:
                    cnt += dfs(nx,ny)
            return cnt
        res = 0
        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                    temp = dfs(i,j)
                    res = max(res,temp)
        return res
    

            
```

BFS

visited在出栈时候设置就一直错，非要在入栈时候设置才行，不知道为什么

```text
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        if not grid or not grid[0]:
            return 0
        n,m = len(grid),len(grid[0])

        d = [-1, 0, 1, 0, -1]

        def bfs(a,b)->int:
            cnt = 1
            q = [(a,b)]
            grid[a][b] = -1
            while q:
                i,j = q.pop(0)              
                for x, y in [(i + d[k], j + d[k + 1]) for k in range(4)]:
                    if 0 <= x < n and 0 <= y < m and grid[x][y] == 1:
                        cnt += 1
                        q.append((x,y))
                        grid[x][y] = -1
            return cnt

        res = 0            
        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:                    
                    cnt = bfs(i,j)
                    res = max(res,cnt)
        return res
```

