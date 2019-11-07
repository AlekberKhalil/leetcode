# Minimum Score Triangulation of Polygon

Given`N`, consider a convex`N`-sided polygon with vertices labelled`A[0], A[i], ..., A[N-1]` in clockwise order.

Suppose you triangulate the polygon into`N-2`triangles. For each triangle, the value of that triangle is the**product** of the labels of the vertices, and the\_total score\_of the triangulation is the sum of these values over all`N-2`triangles in the triangulation.

Return the smallest possible total score that you can achieve with some triangulation of the polygon.

1. **Example 1:**

```text
Input: 
[1,2,3]
Output: 
6
Explanation: 
The polygon is already triangulated, and the score of the only triangle is 6.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/05/01/minimum-score-triangulation-of-polygon-1.png)

```text
Input: 
[3,7,4,5]
Output: 
144
Explanation: 
There are two triangulations, with possible scores: 3*7*5 + 4*5*7 = 245, or 3*4*5 + 3*4*7 = 144.  The minimum score is 144.
```

**Example 3:**

```text
Input: 
[1,3,1,4,1,5]
Output: 
13
Explanation: 
The minimum score triangulation has score 1*1*3 + 1*1*4 + 1*1*5 + 1*1*1 = 13.
```

**Note:**

```text
3 <= A.length <= 50
1 <= A[i] <= 100
```

分析

```text
i,j 段内loop段内的点K  minnum = min(minnum, A[left]*A[right]*A[k] + dfs(left, k) + dfs(k, right))
```

注意初始化可以为最大，前三个点设为0

top down dfs

```text
class Solution:
    def minScoreTriangulation(self, A: List[int]) -> int:
        n = len(A)
        dp = [[float('inf')] *n for _ in range(n)]
        def dfs(i,j):
            if j - i + 1 < 3: #初始化为最大，但是前三个数要初始为0
                return 0
            if dp[i][j] != float('inf'):
                return dp[i][j]
            res =   float('inf') 
            for k in range(i+1,j): #注意此处范围，i.j内不含i,j
                    res = min(res, dfs(i,k) + A[i]*A[j]*A[k] + dfs(k,j))
            dp[i][j] = res
            return res

        return dfs(0,n-1)
```

bottom up DP

遍历长度d&gt;\[2-n\] ,left \[0- n-d\]

从小长度到大长度。 其他遍历法要倒序

```text
class Solution:
    def minScoreTriangulation(self, A: List[int]) -> int:
        n = len(A)
        dp = [[0] *n for _ in range(n)]

        for l in range(2,n):
            for left in range(n-l): 
                right = left + l
                dp[left][right] = float('inf')
                for k in range(left+1,right): #注意此处范围，i.j内不含i,j
                    dp[left][right] = min(dp[left][right], dp[left][k] + A[left]*A[right]*A[k] + dp[k][right])


        return dp[0][n-1]
```

