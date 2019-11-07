# 01 Matrix\(DP\)

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

**Example 1:**

```text
Input:

[[0,0,0],
 [0,1,0],
 [0,0,0]]


Output:

[[0,0,0],
 [0,1,0],
 [0,0,0]]
```

**Example 2:**

```text
Input:

[[0,0,0],
 [0,1,0],
 [1,1,1]]


Output:

[[0,0,0],
 [0,1,0],
 [1,2,1]]
```

**Note:**

1. The number of elements of the given matrix will not exceed 10,000.
2. There are at least one 0 in the given matrix.
3. The cells are adjacent in only four directions: up, down, left and right.

分析

DP

类似数组左右遍历，Matrix先左上，再右下遍历，得到最小的距离，记住这里右下的遍历顺序要反。

之前错误是一次性4个方向遍历

```text
class Solution:
    def updateMatrix(self, matrix: List[List[int]]) -> List[List[int]]:
        if not matrix or not matrix[0]:
            return[]
        n,m = len(matrix),len(matrix[0])
        rr = n*m
        res = [[float('inf')]*m for _ in range(n)]
        for x in range(n):
            for y in range(m):
                if matrix[x][y] == 0:
                    res[x][y] = 0
                else:
                    up = res[x][y-1] if y-1 >=0 else rr                  
                    left = res[x-1][y] if x-1>=0 else rr                 
                    res[x][y] = min(up,left) + 1                
        for x in reversed(range(n)):
            for y in reversed(range(m)):
                if matrix[x][y] == 0:
                    res[x][y] = 0
                else:                   
                    down =res[x][y+1] if y+1<m else rr                 
                    right =res[x+1][y] if x+1<n else rr
                    res[x][y] = min(down+1,right+1,res[x][y])    
        return res
```

BFS

反向，就是以0为圆心4个方向层层扩展，每次扩展d+1。

```text
class Solution:
    def updateMatrix(self, matrix: List[List[int]]) -> List[List[int]]:
        if not matrix or not matrix[0]:
            return[]
        n,m = len(matrix),len(matrix[0])
        rr = n*m
        res = [[rr]*m for _ in range(n)]
        q = [(x,y,0) for x in range(n) for y in range(m) if matrix[x][y] == 0]
        while q:
            x,y,d = q.pop(0)
            if res[x][y]!=rr:
                continue
            res[x][y] = d                            
            if x+1<n:
                q.append((x+1,y,d+1))
            if y + 1 < m:
                q.append((x,y+1,d+1))
            if x-1>=0:
                q.append((x-1,y,d+1))
            if y - 1 >=0:
                q.append((x,y-1,d+1))                  

        return res
```

