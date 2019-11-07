# Bomb Enemy

Given a 2D grid, each cell is either a wall`'W'`, an enemy`'E'`or empty`'0'`\(the number zero\), return the maximum enemies you can kill using one bomb.  
The bomb kills all the enemies in the same row and column from the planted point until it hits the wall since the wall is too strong to be destroyed.  
**Note:**You can only put the bomb at an empty cell.

**Example:**

```text
Input: [["0","E","0","0"],["E","0","W","E"],["0","E","0","0"]]Output: 3 Explanation: For the given grid,0 E 0 0 E 0 W E 0 E 0 0Placing a bomb at (1,1) kills 3 enemies.
```

分析

一遍循环，每次遇到0行列或者W都视为初始，计算该行列里E的总值=rowhit+colhit\[j\]. 遇到0时候就可以直接用了。

注意这里rowhit直接数字，colhit【】要数组，因为遍历的方向性。

遇到w视为开始，再遇到视为结束，注意小loop里计算rowhit colhit，再遇到W直接终止。

```text
class Solution:    def maxKilledEnemies(self, A: List[List[str]]) -> int:        if not A or not A[0]:            return 0        n, m = len(A), len(A[0])        rowhit = 0        colhit = [0]*m #遍历时候row顺序，但是col需要记录整个数组        res = 0        for i in range(n):            for j in range(m):                if not j or A[i][j-1] == 'W':                    rowhit = 0                    for k in range(j, m):#等于while就算当前这个row所有E                        if A[i][k] == 'W':#小loop里计算rowhit colhit，再遇到W直接终止。                            break                        if A[i][k] == 'E':                            rowhit += 1                if not i or A[i-1][j] == 'W':#等于while就算当前这个col所有E                    colhit[j] = 0                    for k in range(i, n):                        if A[k][j] == 'W':                            break                        if A[k][j] == 'E':                            colhit[j] += 1                   if A[i][j] == '0':                    res = max(res,rowhit + colhit[j])        return res
```

