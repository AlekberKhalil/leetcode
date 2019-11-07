# Knight Probability in Chessboard

On an`N`x`N`chessboard, a knight starts at the`r`-th row and`c`-th column and attempts to make exactly`K`moves. The rows and columns are 0 indexed, so the top-left square is`(0, 0)`, and the bottom-right square is`(N-1, N-1)`.

A chess knight has 8 possible moves it can make, as illustrated below. Each move is two squares in a cardinal direction, then one square in an orthogonal direction.

![](https://assets.leetcode.com/uploads/2018/10/12/knight.png)

Each time the knight is to move, it chooses one of eight possible moves uniformly at random \(even if the piece would go off the chessboard\) and moves there.

The knight continues moving until it has made exactly`K`moves or has moved off the chessboard. Return the probability that the knight remains on the board after it has stopped moving.

**Example:**

```text
Input:
 3, 2, 0, 0

Output:
 0.0625

Explanation:
 There are two moves (to (1,2), (2,1)) that will keep the knight on the board.
From each of those positions, there are also two moves that will keep the knight on the board.
The total probability the knight stays on the board is 0.0625.
```

**Note:**

* `N`

  will be between 1 and 25.

* `K`

  will be between 0 and 100.

* The knight always initially starts on the board.

分析

8个方向界内的1相加，总数/8\*\*k

DP: python无法三维数组？？？ 所以k loop内每次新建一个arr和旧arr交替。2个初始值不同

```text
class Solution:
    def knightProbability(self, N: int, K: int, r: int, c: int) -> float:
        p1 = [[1]*N for _ in range(N)] #初始1
        for k in range(K):
            p0 = [[0]*N for _ in range(N)]#初始0
            for i in range(N):
                for j in range(N):
                    for x, y in ((-1, -2), (-2, -1), (-2, 1), (-1, 2), (1, 2), (2, 1), (2, -1), (1, -2)):
                        ni,nj = i+x,j+y
                        if 0 <= ni < N and 0 <= nj < N:
                            p0[i][j] += p1[ni][nj]
            p1 = p0
        return  p1[r][c]/8**K
```

用DFS的memorization，一定记得key 是k+i+j，不能只有i,j。错很久

```text
class Solution:
    def knightProbability(self, N: int, K: int, r: int, c: int) -> float:
        m = {}#DICT的key tuple有k啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊
        def dfs(i,j,k):            
            if k == 0:
                return 1.0
            if (i,j,k) in m:
                return m[(i,j,k)]

            pp = 0.0    
            for x, y in ((-1, -2), (-2, -1), (-2, 1), (-1, 2), (1, 2), (2, 1), (2, -1), (1, -2)):
                ni,nj = i+x,j+y
                if 0 <= ni < N and 0 <= nj < N:
                    pp += dfs(ni,nj,k-1)/8
            m[(i,j,k)] = pp
            return pp


        return dfs(r,c,K)
```

