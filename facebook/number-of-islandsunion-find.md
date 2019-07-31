# Number of Islands\(union find\)

Given a 2d grid map of`'1'`s \(land\) and`'0'`s \(water\), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

```text
Example 1:

Input:
11110
11010
11000
00000

Output: 1
Example 2:

Input:
11000
11000
00100
00011

Output: 3
```

分析

parent也可以用数组，也可以初始都指向-1，记得后面find也用-1比较就好

这里union时候是向4个方向扩展，\[-1,0,1,0,-1\]，以及 for i in range\(4\) 错半死啊！！！！

4个方向扩展要判断边界和grid == 1

```text
import collections


class Solution:
    parent = []
    count = 0

    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid or not len(grid[0]):
            return 0
        n = len(grid)
        m = len(grid[0])
        self.parent = [-1] * m * n#可以用数组而不是dict，初始化为-1时候，后面find也是-1


        # parent = collections.defautdict(int)
        for i in range(n):
            for j in range(m):
                # self.parent[i*m+j] = i*m+j
                if grid[i][j] == '1':
                    self.count += 1

        d = [-1, 0, 1, 0, -1]#错半死

        for i in range(n):
            for j in range(m):
                if grid[i][j] == '1':
                    cur = i * m + j
                    for di in range(4):
                        ni = i + d[di]
                        nj = j + d[di + 1]
                        if self.isBound(ni,nj,n,m) and grid[ni][nj] == '1':
                            nn = ni * m + nj
                            self.union(cur, nn)
        return self.count

    def find(self, x):
        if self.parent[x] == -1:
            return x
        self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        rx = self.find(x)
        ry = self.find(y)
        if rx != ry:
            self.parent[rx] = ry
            self.count -= 1



    def isBound(self,x,y,n,m):
        if x < 0 or x >= n or y < 0 or y >= m:
            return False;
        return True;
```

