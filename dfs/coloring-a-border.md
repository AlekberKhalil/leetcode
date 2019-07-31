# Coloring A Border

Given a 2-dimensional `grid`of integers, each value in the grid represents the color of the grid square at that location.

Two squares belong to the same\_connected component\_if and only if they have the same color and are next to each other in any of the 4 directions.

The \_border\_of a connected component is all the squares in the connected component that are either 4-directionally adjacent to a square not in the component, or on the boundary of the grid \(the first or last row or column\).

Given a square at location `(r0, c0)` in the grid and a`color`, color the border of the connected component of that square with the given`color`, and return the final`grid`.

分析

和普通一样遍历连通，区别是先标记-1 再四个方向dfs，如果都能走，cnt==4时候证明是内部点，重回旧色。

DFS:原图标记

```text
class Solution:
    def colorBorder(self, A: List[List[int]], r0: int, c0: int, color: int) -> List[List[int]]:
        if not A or not A[0]:
            return A

        d = [-1, 0, 1, 0, -1]
        n, m = len(A), len(A[0])
        bclr = A[r0][c0]
        def dfs(x,y):
            nonlocal bclr
            if A[x][y] == -bclr:
                return
            A[x][y] = -bclr
            cnt = 0
            for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:
                if not (0 <= nx < n and 0 <= ny < m and abs(A[nx][ny]) == bclr):
                    continue
                cnt += 1 #正负色都行，所以上面是abs(A[nx][ny]) == bclr
                if A[nx][ny] == bclr:   dfs(nx,ny)#正色才能继续dfs

            if cnt == 4:
                A[x][y] = bclr
        dfs(r0,c0)
        for i in range(n):
            for j in range(m):
                if A[i][j] < 0:
                    A[i][j] = color
        return A
```

用set和Border标记

```text
class Solution:
     def colorBorder(self, A: List[List[int]], r0: int, c0: int, color: int) -> List[List[int]]:
        if not A or not A[0]:
            return A

        d = [-1, 0, 1, 0, -1]
        n, m = len(A), len(A[0])
        bclr = A[r0][c0]
        visited = set()
        border =set()
        def dfs(x,y):
            nonlocal bclr
            if A[x][y] == bclr:
                for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:
                    if 0 <= nx < n and 0 <= ny < m and A[nx][ny] == bclr:
                        if (nx,ny) not in visited:
                            visited.add((nx,ny))
                            dfs(nx,ny)
                    else:
                        border.add((x,y))
        dfs(r0,c0)
        for i,j in border:
            A[i][j] = color
        return A
```

和以上基本一致的BFS，用set标记visited

```text
class Solution:
     def colorBorder(self, A: List[List[int]], r0: int, c0: int, color: int) -> List[List[int]]:
        if not A or not A[0]:
            return A

        d = [-1, 0, 1, 0, -1]
        n, m = len(A), len(A[0])
        bclr = A[r0][c0]
        visited = set()
        border =set()
        q = [(r0,c0)]
        for x,y in q:
            for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:
                if 0 <= nx < n and 0 <= ny < m and A[nx][ny] == bclr:
                    if (nx,ny) not in visited:
                        visited.add((nx,ny))
                        q.append((nx,ny))
                else:
                    border.add((x,y))

        for i,j in border:
            A[i][j] = color
        return A
```

