# Trapping Rain Water II

Given_n\_x\_m\_non-negative integers representing an elevation map 2d where the area of each cell is\_1\_x\_1_, compute how much water it is able to trap after raining.

![](https://lintcode-media.s3.amazonaws.com/problem/trapping-rain-water-ii.jpg)

分析：

从外围最低点向内灌水 外面形成墙，保证灌水高度不会漏

1 最外围都加入堆，从外往内灌。

2 用堆维护最小值（override compare） 堆里加入三元组（x,y,当前灌水最高高度）

时间复杂度log\(2m+2n\)\*n\*m

农村包围城市，无需双重for loop 依然遍历了所有点，这种从外围然后四点扩展法值得注意。

答案：

```text
 class Cell{    public int x, y, h;    Cell(int xx, int yy, int hh){        x = xx;        y = yy;        h = hh;    }}public class Solution{    int[] dx = {1, -1, 0, 0};    int[] dy = {0, 0, 1, -1};    public int trapRainWater(int[][] heights){        if(heights.length == 0)            return 0;        PriorityQueue<Cell> q = new PriorityQueue<Cell>(1, new Comparator<Cell>(){            public int compare(Cell x, Cell y){                return x.h - y.h;            }        });        int n = heights.length;        int m = heights[0].length;        int[][] visit = new int[n][m];        //初始化        for(int i = 0; i < n; i ++){            q.offer(new Cell(i, 0, heights[i][0]));            q.offer(new Cell(i, m-1, heights[i][m-1]));            visit[i][0] = 1;            visit[i][m-1] = 1;        }        for(int i = 0; i < m; i ++){            q.offer(new Cell(0, i, heights[0][i]));            q.offer(new Cell(n-1, i, heights[n-1][i]));            visit[0][i] = 1;            visit[n-1][i] = 1;        }        int ans = 0;        while(!q.isEmpty()){            Cell now = q.poll();            for(int i = 0; i < 4; i ++){                int nx = now.x + dx[i];                int ny = now.y + dy[i];                if(0 <= nx && nx < n && 0 <= ny && ny < m && visit[nx][ny] == 0){                    visit[nx][ny] = 1;                    q.offer(new Cell(nx, ny, Math.max(now.h, heights[nx][ny])));                    ans += Math.max(0, now.h - heights[nx][ny]);                }            }        }         return ans;    }}
```

Python

```text
class Solution:    def trapRainWater(self, heightMap: List[List[int]]) -> int:        if not heightMap or not heightMap[0]:            return 0        n,m = len(heightMap),len(heightMap[0])        q = [(heightMap[0][j],0,j) for j in range(m)] + [(heightMap[i][0],i,0) for i in range(n)] + [(heightMap[n-1][j],n-1,j) for j in range(m)] + [(heightMap[i][m-1],i,m-1) for i in range(n)]        seen = {(0,j) for j in range(m)} | {(x,0) for x in range(n)}| {(n-1,j) for j in range(m)} | {(x,m-1) for x in range(n)}        heapq.heapify(q)        d = [-1,0,1,0,-1]        res = 0        while q:            h,x,y = heapq.heappop(q)            for nx,ny in [(x+d[i],y+d[i+1]) for i in range(4)]:                if 0 <= nx < n and 0 <= ny < m and (nx,ny) not in seen:                    if heightMap[nx][ny] < h:                        res += h - heightMap[nx][ny]                    heapq.heappush(q,(max(h, heightMap[nx][ny]),nx,ny))                    seen.add((nx,ny))        return res
```

