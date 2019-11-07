# Pacific Atlantic Water Flow

Given an`m x n`matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions \(up, down, left, or right\) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

**Note:**

1. The order of returned grid coordinates does not matter.
2. Both m and n are less than 150.

**Example:**

```text
Given the following 5x5 matrix:  Pacific ~   ~   ~   ~   ~        ~  1   2   2   3  (5) *       ~  3   2   3  (4) (4) *       ~  2   4  (5)  3   1  *       ~ (6) (7)  1   4   5  *       ~ (5)  1   1   2   4  *          *   *   *   *   * AtlanticReturn:[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
```

分析

类似_longest increasing path in matrix_

但是这里从结果出发，从四条边开始往里走 标记可达的点用visited。

这里有2个visited 表示2个海洋，最近结果要同时满足这俩visited.

```text
class Solution:    d = [-1, 0, 1, 0, -1]    m = n = 0    def pacificAtlantic(self, matrix: List[List[int]]) -> List[List[int]]:        if not matrix or not matrix:            return []        self.n, self.m = len(matrix), len(matrix[0])        av = [[0] * self.m for _ in range(self.n)]        pv = [[0] * self.m for _ in range(self.n)]        for i in range(self.n):            self.dfs(matrix,i,0,pv)            self.dfs(matrix,i,self.m-1,av)        for j in range(self.m):            self.dfs(matrix,0,j,pv)            self.dfs(matrix,self.n-1,j,av)        res = []        for i in range(self.n):             for j in range(self.m):                if av[i][j] and pv[i][j]:                    res.append([i,j])        return res    def dfs(self,matrix,x,y,visited):        visited[x][y] = 1        nxy = [(x+self.d[i],y+self.d[i+1]) for i in range(4) ]        for nx,ny in nxy:            if 0 <= nx < self.n and 0 <= ny < self.m and  not visited[nx][ny] and matrix[nx][ny] >= matrix[x][y]:                self.dfs(matrix,nx,ny,visited)
```

