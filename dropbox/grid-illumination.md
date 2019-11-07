# Grid Illumination



On a `N x N` grid of cells, each cell `(x, y)` with `0 <= x < N` and `0 <= y < N` has a lamp.

Initially, some number of lamps are on.  `lamps[i]` tells us the location of the `i`-th lamp that is on.  Each lamp that is on illuminates every square on its x-axis, y-axis, and both diagonals \(similar to a Queen in chess\).

For the i-th query `queries[i] = (x, y)`, the answer to the query is 1 if the cell \(x, y\) is illuminated, else 0.

After each query `(x, y)` \[in the order given by `queries`\], we turn off any lamps that are at cell `(x, y)` or are adjacent 8-directionally \(ie., share a corner or edge with cell `(x, y)`.\)

Return an array of answers.  Each value `answer[i]` should be equal to the answer of the `i`-th query `queries[i]`.

**Example 1:**

```text
Input: N = 5, lamps = [[0,0],[4,4]], queries = [[1,1],[1,0]]Output: [1,0]Explanation: Before performing the first query we have both lamps [0,0] and [4,4] on.The grid representing which cells are lit looks like this, where [0,0] is the top left corner, and [4,4] is the bottom right corner:1 1 1 1 11 1 0 0 11 0 1 0 11 0 0 1 11 1 1 1 1Then the query at [1, 1] returns 1 because the cell is lit.  After this query, the lamp at [0, 0] turns off, and the grid now looks like this:1 0 0 0 10 1 0 0 10 0 1 0 10 0 0 1 11 1 1 1 1Before performing the second query we have only the lamp [4,4] on.  Now the query at [1,0] returns 0, because the cell is no longer lit.
```

分析

N 皇后 sodoku

此做法python TLE

```text
from collections import Counterclass Solution:    def gridIllumination(self, N: int, lamps: List[List[int]], queries: List[List[int]]) -> List[int]:        lamps = set(list(map(tuple, lamps)))        h,v,l,r = Counter(),Counter(),Counter(),Counter()        res = []        for x,y in lamps:            h[x]+=1            v[y]+=1            l[x+y]+=1            r[x-y]+=1        for x,y in queries:            if (x,y) in lamps or h[x] or v[y] or l[x+y] or r[x-y]:                res.append(1)            else:                res.append(0)            for nx in range(x-1,x+2):                for ny in range(y-1,y+2):                    if (nx,ny) in lamps:                        lamps.remove((nx,ny))                        h[nx] -= 1                        if h[nx] == 0:                            del h[nx]                        v[ny] -= 1                        if v[ny] == 0:                            del v[ny]                        l[nx+ny] -= 1                        if l[nx+ny] == 0:                            del l[nx+ny]                        r[nx-ny] -= 1                        if r[nx-ny] == 0:                            del r[nx-ny]        return res                                                                
```

