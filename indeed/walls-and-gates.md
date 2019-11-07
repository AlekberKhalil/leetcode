# Walls and Gates\(反向BFS\)

> **Question**

You are given a m x n 2D grid initialized with these three possible values.

1. -1 - A wall or an obstacle.
2. 0 - A gate.
3. INF - Infinity means an empty room. We use the value 231 - 1 =`2147483647`to represent`INF`as you may assume that the distance to a gate is less than`2147483647`
4. Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with`INF`

For example, given the 2D grid:

```text
INF  -1  0  INFINF INF INF  -1INF  -1 INF  -1  0  -1 INF INF
```

After running your function, the 2D grid should be:

```text
 3  -1   0   1 2   2   1  -1 1  -1   2  -1 0  -1   3   4
```

分析

反向BFS，不用空房间做BFS，而用门开始做BFS。初始把所有门都加入Queue

**rooms\[nx\]\[ny\] &lt; rooms\[x\]\[y\] + 1 可以去重，不需要的就不会重复计算了。**

```text
class Main {    public static void wallsAndGates(int[][] rooms) {        if(rooms == null || rooms.length == 0 || rooms[0] == null || rooms[0].length == 0)        return;        Queue<Integer> q = new LinkedList<Integer>();        int n = rooms.length;        int m = rooms[0].length;        int[] dx = {0,1,0,-1};        int[] dy= {1,0,-1,0};        for(int i = 0; i < n; i ++){            for(int j = 0; j < m; j ++){                if(rooms[i][j] == 0){                    q.offer(i * m + j);                }            }        }        while(!q.isEmpty()){            int temp = q.poll();            int x = temp / m, y = temp % m;            for(int i = 0; i < 4; i ++){                int nx = x + dx[i], ny = y + dy[i];                //rooms[nx][ny] < rooms[x][y] + 1 可以去重，不需要的就不会重复计算了。                if(nx < 0 || nx >= rooms.length || ny < 0 || ny >= rooms[0].length || rooms[nx][ny] < rooms[x][y] + 1){                    continue;                }                rooms[nx][ny] = rooms[x][y] + 1;                q.offer(nx * m + ny);            }        }    }    public static void main(String[] args) {        int INF = Integer.MAX_VALUE - 1;        int[][] rooms = {{INF,-1,0,INF},{INF,INF,INF,-1},{INF,-1,INF,-1},{0,-1,INF,INF}};        wallsAndGates(rooms);        for(int[] r : rooms){            for(int i : r){                System.out.print(i + " ");            }            System.out.print("\n");        }    }}
```

python

```text
class Solution:    """    @param rooms: m x n 2D grid    @return: nothing    """    def wallsAndGates(self, rooms):        # write your code here        N=len(rooms)        M=len(rooms[0])        INF = 2147483647        q = []        for i,r in enumerate(rooms):            for j,v in enumerate(r):                if v == 0:                    q.append(i*M+j)        d = [-1,0,1,0,-1]        # visited = [[0]*M for _ in range(N)]        while q:            cur = q.pop(0)            x,y=cur//M,cur%M            # visited[cur[0]][cur[1]] = 1            for i in range(len(d)-1):                nx,ny = x+d[i],y+d[i+1]                if nx < 0 or ny < 0 or nx >= N or ny >= M or rooms[nx][ny] < rooms[x][y] + 1:                    continue                q.append(nx*M+ny)                rooms[nx][ny] = rooms[x][y]+1
```

