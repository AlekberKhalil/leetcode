# Shortest Bridge

In a given 2D binary array`A`, there are two islands. \(An island is a 4-directionally connected group of `1`s not connected to any other 1s.\)

Now, we may change`0`s to`1`s so as to connect the two islands together to form 1 island.

Return the smallest number of`0`s that must be flipped. \(It is guaranteed that the answer is at least 1.\)

**Example 1:**

```text
Input: 
[[0,1],[1,0]]
Output: 
1
```

**Example 2:**

```text
Input: 
[[0,1,0],[0,0,0],[0,0,1]]
Output: 
2
```

**Example 3:**

```text
Input: 
[[1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]
Output: 
1
```

**Note:**

```text
1 <= A.length = A[0].length <= 100
A[i][j] == 0 or A[i][j] == 1
```

分析

dfs+bfs

先dfs把第一个岛都标记visited并且塞进q

再bfs一层层扩展，记得遇到1直接返回。还有入栈时候标记visited

```text
class Solution:
    def shortestBridge(self, A: List[List[int]]) -> int:

        res = float('inf')
        d = [-1,0,1,0,-1]
        n,m = len(A),len(A[0])

        def dfs(x,y):
            if A[x][y] != 1:
                return
            A[x][y] = -1
            q.append((x,y))
            for nx,ny in [(x+d[k],y+d[k+1]) for k in range(4)]:
                if 0<=nx<n and 0<=ny<m and A[nx][ny] == 1:
                    dfs(nx,ny)
        q = []           
        found = False          
        for u in range(n): 
            if found:
                break
            for v in range(m):
                if A[u][v] == 1:
                    dfs(u,v)
                    found = True
                    break

        step = 0
        while q:            
            size = len(q)
            for k in range(size):
                i,j = q.pop(0)  
                for nx,ny in [(i+d[k],j+d[k+1]) for k in range(4)]:
                    if 0<=nx<n and 0<=ny<m and A[nx][ny] != -1:
                        if A[nx][ny] == 1:
                            return step
                        q.append((nx,ny))
                        A[nx][ny] = -1 #入栈时标记visited
            step += 1
        return step
```

