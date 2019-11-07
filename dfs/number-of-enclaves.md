# Number of Enclaves

```text
Given a 2D arrayA, each cell is 0 (representing sea) or 1 (representing land)
```

A move consists of walking from one land square 4-directionally to another land square, or off the boundary of the grid.

Return the number of land squares in the grid for which we**cannot**walk off the boundary of the grid in any number of moves.

**Example 1:**

```text
Input: 
[[0,0,0,0],[1,0,1,0],[0,1,1,0],[0,0,0,0]]
Output: 
3
Explanation: 

There are three 1s that are enclosed by 0s, and one 1 that isn't enclosed because its on the boundary.
```

**Example 2:**

```text
Input: 
[[0,1,1,0],[0,0,1,0],[0,0,1,0],[0,0,0,0]]
Output: 
0
Explanation: 

All 1s are either on the boundary or can reach the boundary.
```

**Note:**

```text
1 <= A.length <= 500
1 <= A[i].length <= 500
0 <= A[i][j] <= 1
All rows have the same size.
```

分析

从边缘1开始往内不断扩张并flip，最后数剩下1就是答案

```text
class Solution:
    def numEnclaves(self, A: List[List[int]]) -> int:
        if not A or not A[0]:
            return 0
        res = float('inf')
        d = [-1, 0, 1, 0, -1]
        n, m = len(A), len(A[0])
        def dfs(x, y):           
            if A[x][y] == -1:
                return            
            A[x][y] = -1
            for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:
                if 0 <= nx < n and 0 <= ny < m and A[nx][ny] == 1:
                    dfs(nx, ny)

        for i in range(n):
            for j in range(m):
                if (i==0 or i == n-1 or j == 0 or j == m-1) and A[i][j] == 1:
                    dfs(i,j)
        cnt = 0            
        for i in range(n):
            for j in range(m):
                if A[i][j] == 1:
                    cnt += 1
        return cnt
```

BFS

```text
class Solution:
    def numEnclaves(self, A: List[List[int]]) -> int:
        if not A or not A[0]:
            return 0
        res = float('inf')
        d = [-1, 0, 1, 0, -1]
        n, m = len(A), len(A[0])

        for i in range(n):
            for j in range(m):
                if (i==0 or i == n-1 or j == 0 or j == m-1) and A[i][j] == 1:
                    q = [(i,j)]
                    while q:
                        x,y=q.pop()
                        if A[x][y] == -1:
                            continue            
                        A[x][y] = -1
                        for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:
                            if 0 <= nx < n and 0 <= ny < m and A[nx][ny] == 1:
                                q.append((nx, ny))
        cnt = 0            
        for i in range(n):
            for j in range(m):
                if A[i][j] == 1:
                    cnt += 1
        return cnt
```

BFS基础上再加union find

```text
class Solution:
    def numEnclaves(self, A: List[List[int]]) -> int:
        if not A or not A[0]:
            return 0
        res = float('inf')
        d = [-1, 0, 1, 0, -1]
        n, m = len(A), len(A[0])

        f={}
        def find(x):
            f.setdefault(x,x)
            if f[x]!=x:
                f[x] = find(f[x])
            return f[x]
        def union(x,y):
            f[find(x)]=find(y)

        for i in range(n):
            for j in range(m):
                if (i==0 or i == n-1 or j == 0 or j == m-1) and A[i][j] == 1:
                    q= [(i,j)]
                    while q:
                        x,y=q.pop()
                        if A[x][y] == -1:
                            continue
                        A[x][y] = -1
                        for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:
                            if 0 <= nx < n and 0 <= ny < m and A[nx][ny] == 1:
                                q.append((nx, ny))
                                union((nx, ny),(i,j))

        cnt = 0            
        for i in range(n):
            for j in range(m):
                if A[i][j] == 1 and (i,j) not in f:
                    cnt += 1
        return cnt
```

