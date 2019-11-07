# Out of Boundary Paths

```text
There is an m by n grid with a ball. Given the start coordinate (i,j) of the ball, you can move the ball to adjacent cell or cross the grid boundary in four directions (up, down, left, right). However, you can at most move N times. Find out the number of paths to move the ball out of grid boundary. The answer may be very large, return it after mod 109 + 7.



Example 1:

Input: m = 2, n = 2, N = 2, i = 0, j = 0
Output: 6
Explanation:

Example 2:

Input: m = 1, n = 3, N = 3, i = 0, j = 1
Output: 12
Explanation:



Note:

Once you move the ball out of boundary, you cannot move it back.
The length and height of the grid is in range [1,50].
N is in range [0,50].
```

分析

记忆化搜索

落入范围内的，步数不够就是0，步数够就4个方向继续延展

不在范围内，就是最终答案了

```text
class Solution:
    def findPaths(self, m: int, n: int, N: int, i: int, j: int) -> int:
        if not m or not n:
            return 0
        MOD = 10**9 + 7
        res = 0
        d = [-1,0,1,0,-1]
        mm = collections.defaultdict(int)

        def dfs(i,j,step):
            if (i,j,step) in mm:
                return mm[(i,j,step)]
            if 0<=i<m and 0<=j<n:#范围内
                if step == 0:
                    mm[(i,j,step)] = 0
                    return 0
                for x,y in [(i+1,j),(i-1,j),(i,j+1),(i,j-1)]:
                    mm[(i,j,step)] += dfs(x,y,step-1)
                return mm[(i,j,step)]%MOD
            else:#不在范围内
                mm[(i,j,step)] = 1
                return 1



        return dfs(i,j,N)%MOD
```

DP:

At time t, let's maintain`cur[r][c]`= the number of paths to`(r, c)`with`t`moves, and`nxt[r][c]`= the number of paths to`(r, c)`with`t+1`moves.

A ball at`(r, c)`at time`t`, can move in one of four directions. **If it stays on the board, then it contributes to a path that takes`t+1`moves. If it falls off the board, then it contributes to the final answer.**

```text
class Solution:
    def findPaths(self, m: int, n: int, N: int, i: int, j: int) -> int:
        if not m or not n:
            return 0
        MOD = 10**9 + 7
        res = 0
        d = [-1,0,1,0,-1]
        mm = collections.defaultdict(int)
        res = 0
        cur = [[0]*n for k in range(m)]
        cur[i][j] = 1

        for t in range(N):
            temp = [[0]*n for k in range(m)]
            for i in range(m):
                for j in range(n):
                    for x,y in [(i+1,j),(i-1,j),(i,j+1),(i,j-1)]:
                        if 0<=x<m and 0<=y<n:
                            temp[i][j] += cur[x][y] #界限内，当前ij可由四周走入 step-1
                        else:
                            res += cur[i][j]#界限外，入答案
                            res %=MOD
            cur[:] = temp[:]

        return res%MOD
```

