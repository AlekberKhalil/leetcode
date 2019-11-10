# Walls and Gates\(反向BFS\)

> **Question**

You are given a m x n 2D grid initialized with these three possible values.

1. -1 - A wall or an obstacle.
2. 0 - A gate.
3. INF - Infinity means an empty room. We use the value 231 - 1 =`2147483647`to represent`INF`as you may assume that the distance to a gate is less than`2147483647`
4. Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with`INF`

For example, given the 2D grid:

```text
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
```

After running your function, the 2D grid should be:

```text
 3  -1   0   1
 2   2   1  -1
 1  -1   2  -1
 0  -1   3   4
```

分析

反向BFS，不用空房间做BFS，而用门开始做BFS。初始把所有门都加入Queue

**rooms\[nx\]\[ny\] &lt; rooms\[x\]\[y\] + 1 可以去重，不需要的就不会重复计算了。**

```text
class Main {
    public static void wallsAndGates(int[][] rooms) {
        if(rooms == null || rooms.length == 0 || rooms[0] == null || rooms[0].length == 0)
        return;
        Queue<Integer> q = new LinkedList<Integer>();
        int n = rooms.length;
        int m = rooms[0].length;
        int[] dx = {0,1,0,-1};
        int[] dy= {1,0,-1,0};
        for(int i = 0; i < n; i ++){
            for(int j = 0; j < m; j ++){
                if(rooms[i][j] == 0){
                    q.offer(i * m + j);
                }
            }
        }
        while(!q.isEmpty()){
            int temp = q.poll();
            int x = temp / m, y = temp % m;
            for(int i = 0; i < 4; i ++){
                int nx = x + dx[i], ny = y + dy[i];
                //rooms[nx][ny] < rooms[x][y] + 1 可以去重，不需要的就不会重复计算了。
                if(nx < 0 || nx >= rooms.length || ny < 0 || ny >= rooms[0].length || rooms[nx][ny] < rooms[x][y] + 1){
                    continue;
                }
                rooms[nx][ny] = rooms[x][y] + 1;
                q.offer(nx * m + ny);
            }
        }
    }

    public static void main(String[] args) {
        int INF = Integer.MAX_VALUE - 1;
        int[][] rooms = {{INF,-1,0,INF},{INF,INF,INF,-1},{INF,-1,INF,-1},{0,-1,INF,INF}};
        wallsAndGates(rooms);
        for(int[] r : rooms){
            for(int i : r){
                System.out.print(i + " ");
            }
            System.out.print("\n");
        }

    }
}
```

python

不用 seen, 替代的是每次比较rooms\[nx\]\[ny\] &gt; rooms\[x\]\[y\] + 1， 不行就不入Q

```text
class Solution:
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """
        if not rooms:
            return
        n,m = len(rooms),len(rooms[0])
        d = [-1,0,1,0,-1]
        q = [(x,y) for x in range(n) for y in range(m) if rooms[x][y] == 0]
        
        while q:
            x,y  = q.pop()
            for nx, ny in [(x+d[i],y+d[i+1]) for i in range(4)]:
                if 0 <= nx < n and 0<= ny < m and rooms[nx][ny] != -1 and rooms[nx][ny] > rooms[x][y] + 1:
                    rooms[nx][ny] = rooms[x][y] + 1
                    q.append((nx,ny))
```

