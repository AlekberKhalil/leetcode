# Swim in Rising Water

On an N x N`grid`, each square`grid[i][j]`represents the elevation at that point`(i,j)`.

Now rain starts to fall. At time`t`, the depth of the water everywhere is`t`. You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares individually are at most `t`. You can swim infinite distance in zero time. Of course, you must stay within the boundaries of the grid during your swim.

You start at the top left square`(0, 0)`. What is the least time until you can reach the bottom right square`(N-1, N-1)`?

**Example 1:**

```text
Input: [[0,2],[1,3]]Output: 3Explanation:At time 0, you are in grid location (0, 0).You cannot go anywhere else because 4-directionally adjacent neighbors have a higher elevation than t = 0.You cannot reach point (1, 1) until time 3.When the depth of water is 3, we can swim anywhere inside the grid.
```

**Example 2:**

```text
Input: [[0,1,2,3,4],[24,23,22,21,5],[12,13,14,15,16],[11,17,18,19,20],[10,9,8,7,6]]Output: 16Explanation: 0  1  2  3  424 23 22 21  512 13 14 15 1611 17 18 19 2010  9  8  7  6The final route is marked in bold.We need to wait until time 16 so that (0, 0) and (4, 4) are connected.
```

**Note:**

```text
2 <= N <= 50.grid[i][j] is a permutation of [0, ..., N*N - 1].
```

分析

此题和trapping rain water 类似，建立一个三元组的类，包含x,y,height

利用priority queue，此处lamda 来表示comparator, init priority queue可以不需size

此处矩阵的visited可以用二维boolean表示。记得遍历完一定要标记！！！！！

int\[\] dir = {-1,0,1,0,-1};这种四个方向遍历x,y坐标很好用

```text
class Solution { class Cell {    int x;    int y;    int height;    public Cell(int x, int y, int height) {        this.x = x;        this.y = y;        this.height = height;    }}    public int swimInWater(int[][] grid) {        int n = grid.length;               PriorityQueue<Cell> pq = new PriorityQueue<>((a,b) -> (a.height - b.height));        //学习visite数组这种写法，boolean二维数组解决        boolean[][] visited = new boolean[n][n];        pq.offer(new Cell(0,0,grid[0][0]));        visited[0][0] = true;        int[] dir = {-1, 0, 1, 0, -1};//这种x,y的递增写法很好用。        int ans = grid[0][0];        while(!pq.isEmpty()) {            Cell cur = pq.poll();            ans = Math.max(ans, cur.height);            //这里记得得到结果            if(cur.x == n - 1 && cur.y == n-1) {                return ans;            }            for(int i = 0; i < 4; i++) {                int nx = cur.x + dir[i], ny = cur.y + dir[i + 1];                if(nx < 0 || ny < 0 || nx >= n|| ny >= n || visited[nx][ny]){                    continue;                }                pq.offer(new Cell(nx, ny, grid[nx][ny]));                visited[nx][ny] = true; //不要忘记标记visit数组！！！！！            }        }        return ans;    }}
```

