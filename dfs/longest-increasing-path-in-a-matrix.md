# Longest Increasing Path in a Matrix

Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary \(i.e. wrap-around is not allowed\).

**Example 1:**

```text
Input: nums = 
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
] 
Output: 4 
Explanation: The longest increasing path is [1, 2, 6, 9].
```

**Example 2:**

```text
Input: nums = 
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
] 
Output: 4 
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```

分析

memorize 用dp数组记录已经算过的，dp这里也起了visited的作用

几个边界条件

1visited dfs开始就用DP返回

2 x,y过界和没有递增，在for loop里continue掉

DFS

```text
class Solution:
    d = [-1,0,1,0,-1]
    n=m=0
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        if not matrix or not matrix[0]:
            return 0
        self.n,self.m=len(matrix),len(matrix[0])
        res = 0
        dp = [[0]*self.m for _ in range(self.n)]
        for i in range(self.n):
            for j in range(self.m):
                res = max(res, self.dfs(matrix,dp,i,j))
        return res



    def dfs(self,matrix: List[List[int]],dp: List[List[int]], x:int, y:int) -> int:
        if dp[x][y]:
            return dp[x][y]        

        nxy = [(x+self.d[i],y+self.d[i+1]) for i in range(4) ]  

        maxStep = max([self.dfs(matrix,dp,nx,ny) for nx,ny in nxy if nx < self.n and nx>= 0 and ny < self.m and ny>=0 and matrix[nx][ny] > matrix[x][y] ] or [0])
        dp[x][y] = 1 + maxStep


        return 1+maxStep
```

BFS

每次while找出不可达点（出度为0），每一次while loop就是一层，层里是当前Level里所有的不可达点，加入visited。

全部遍历完，多少level层数就是最长的Path。

```text
class Solution:
    d = [-1,0,1,0,-1]
    n=m=0
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        if not matrix or not matrix[0]:
            return 0
        self.n,self.m = len(matrix),len(matrix[0])

        res = 0
        cnt = self.m * self.n

        while cnt:
            visted = set()
            for i in range(self.n):
                for j in range(self.m):    
                    if matrix[i][j] == float('-inf'):
                        continue
                    if (i == 0 or matrix[i][j] >= matrix[i-1][j]) and (i == self.n-1 or matrix[i][j] >= matrix[i+1][j]) and (j == 0 or matrix[i][j] >= matrix[i][j - 1]) and (j == self.m - 1 or matrix[i][j] >= matrix[i][j + 1]):
                        visted.add((i,j))
            for i,j in visted:
                matrix[i][j] = float('-inf')
                cnt -= 1
            res +=1
        return res
```

