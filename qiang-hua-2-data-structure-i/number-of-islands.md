# Number of Islands

Given a boolean 2D matrix,`0`is represented as the sea,`1`is represented as the island. If two 1 is adjacent, we consider them in the same island. We only consider up/down/left/right adjacent.

Find the number of islands.

**Example**

Given graph:

```text
[
  [1, 1, 0, 0, 0],
  [0, 1, 0, 0, 1],
  [0, 0, 0, 1, 1],
  [0, 0, 0, 0, 0],
  [0, 0, 0, 0, 1]
]
```

return`3`.

分析：

Union Find并查集，用BFS也能做。

```text
(x,y)->idid = mx+y -> x = id/m y = id%m (M是矩阵宽）
```

```text
class UnionFind { 

    private int[] father = null;
    private int count;

    private int find(int x) {
        if (father[x] == x) {
            return x;
        }
        return father[x] = find(father[x]);
    }

    public UnionFind(int n) {
        // initialize your data structure here.
        father = new int[n];
        for (int i = 0; i < n; ++i) {
            father[i] = i;
        }
    }

    public void connect(int a, int b) {
        // Write your code here
        int root_a = find(a);
        int root_b = find(b);
        if (root_a != root_b) {
            father[root_a] = root_b;
            count --;
        }
    }

    public int query() {
        // Write your code here
        return count;
    }

    public void set_count(int total) {
        count = total;
    }
}

public class Solution {
    /**
     * @param grid a boolean 2D matrix
     * @return an integer
     */
    public int numIslands(boolean[][] grid) {
        // Write your code here
        if(grid == null || grid.length == 0 || grid[0] == null || grid[0].length == 0)
            return 0;
        int n = grid.length;
        int m = grid[0].length;

        UnionFind f = new UnionFind(m*n);
        int count = 0;
        for(int i = 0; i < n; i ++){
            for(int j = 0; j < m; j ++){
                if(grid[i][j]){
                    count ++;
                }

            }
        }
        f.set_count(count);

        for(int i = 0; i < n; i ++)
            for(int j = 0; j < m; j ++)
                if(grid[i][j]){
                    if(i < n-1 && grid[i+1][j]){
                        f.connect(i * m + j, (i + 1) * m + j);
                    }
                    if(i > 0 && grid[i-1][j]){
                        f.connect(i * m + j, (i - 1) * m + j);
                    }
                    if(j > 0 && grid[i][j-1]){
                        f.connect(i * m + j, i * m + j - 1);
                    }
                    if(j < m-1 && grid[i][j+1]){
                        f.connect(i * m + j, i * m + j + 1);
                    }
                }

    //此处for loop 可用以下代码替代
            int[] dx = {1, -1, 0, 0};
            int[] dy = {0, 0, 1, -1};
            for(int i = 0; i < n; i ++){
                for(int j = 0; j < m; j ++){
                    for(int k = 0; k < 4; k++){
                        int ni = i + dx[k];
                        int nj = j + dy[k];
                        if(ni < 0 || ni >= n || nj < 0 || nj >= m || !grid[i][j] || !grid[ni][nj])
                            continue;
                        f.connect(i * m + j, ni * m + nj);
                    }
                }
            }


        return f.query();
    }
}
```

