# Regions Cut By Slashes

```text
In a N x N grid composed of 1 x 1 squares, each 1 x 1 square consists of a /, \, or blank space.  These characters divide the square into contiguous regions.(Note that backslash characters are escaped, so a \ is represented as "\\".)Return the number of regions.Example 1:Input:[  " /",  "/ "]Output: 2Explanation: The 2x2 grid is as follows:Example 2:Input:[  " /",  "  "]Output: 1Explanation: The 2x2 grid is as follows:Example 3:Input:[  "\\/",  "/\\"]Output: 4Explanation: (Recall that because \ characters are escaped, "\\/" refers to \/, and "/\\" refers to /\.)The 2x2 grid is as follows:Example 4:Input:[  "/\\",  "\\/"]Output: 5Explanation: (Recall that because \ characters are escaped, "/\\" refers to /\, and "\\/" refers to \/.)The 2x2 grid is as follows:Example 5:Input:[  "//",  "/ "]Output: 3Explanation: The 2x2 grid is as follows:Note:1 <= grid.length == grid[0].length <= 30grid[i][j] is either '/', '\', or ' '.
```

分析

把一个格子/或者\扩展成9个格子0，然后\or/标记visited。然后dfs从0开始计算连通块个数

```text
class Solution:    def regionsBySlashes(self, grid: List[str]) -> int:        if not grid or not grid[0]:            return 0        res = 0        d = [-1, 0, 1, 0, -1]        n, m = len(grid)*3, len(grid[0])*3        def dfs(x, y):                        if g[x][y] !=0:                return                        g[x][y] = -1            for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:                if 0 <= nx < n and 0 <= ny < m and g[nx][ny] ==0:                    dfs(nx, ny)        g = [[0]*m for _ in range(n)]        for i in range(len(grid)):              for j in range(len(grid[0])):                                if grid[i][j] == "\\":                    g[i*3][j*3] = g[i*3+1][j*3+1]=g[i*3+2][j*3+2] = -1                if grid[i][j] ==  "/":                    g[i*3][j*3+2] = g[i*3+1][j*3+1]=g[i*3+2][j*3] = -1         for i in range(n):                                   for j in range(m):                if g[i][j] == 0:                    dfs(i,j)                    res += 1        return res
```

Union Find的做法

结果就是多少个爹的个数，用set。这里map函数不用（）

把一个格子分成4块，顺时针标记4个颜色，对/ 03，12连.对\01，23连。记住相邻格子的13连， 上下格子的20连

[https://leetcode.com/problems/regions-cut-by-slashes/discuss/205680/JavaC%2B%2BPython-Split-4-parts-and-Union-Find](https://leetcode.com/problems/regions-cut-by-slashes/discuss/205680/JavaC%2B%2BPython-Split-4-parts-and-Union-Find)

```text
class Solution:    def regionsBySlashes(self, grid: List[str]) -> int:            n, m = len(grid), len(grid[0])        f = {}        def find(x):            f.setdefault(x,x)            if f[x]!= x:                f[x] = find(f[x])            return f[x]        def union(x,y):             f[find(x)] = find(y)        for x in range(n):              for y in range(m):                if y:                    union((x,y-1,1),(x,y,3)) #左右2个相邻格子的1，3连                if x:                    union((x,y,0),(x-1,y,2))#上下2个相连格子的2，0连，记住顺序                if grid[x][y] != "\\":                    union((x,y,0),(x,y,3))                    union((x,y,1),(x,y,2))                if grid[x][y] !=  "/":                    union((x,y,0),(x,y,1))                    union((x,y,2),(x,y,3))                           return len(set(map(find,f)))
```

