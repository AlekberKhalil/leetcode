# Number of Islands

Given a 2d grid map of`'1'`s \(land\) and`'0'`s \(water\), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```text
11110110101100000000
```

Answer: 1

**Example 2:**

```text
11000110000010000011
```

Answer: 3

分析

并查集，connect里，一个头指向另一个头

初始化只有N时，指向自己

连接点时，每个点用x\*m + y表示，2个点都是1时候就connect

开始count == 1的点的总数，每次连接cnt--

每个1的点四个方向扩展，遇到1的话就连接

```text
 class UnionFind{    private int[] father = null;    private int count;    public UnionFind(int n){        father = new int[n];        for(int i = 0; i < n; i ++){            father[i] = i;        }    }    private int find(int x){        if(father[x] == x)            return x;        return father[x] = find(father[x]);    }    public void connect(int x, int y){        int root_x = find(x);        int root_y = find(y);        if(root_x != root_y){            father[root_x] = root_y;//错很久，把一个root指向另一个root            count --;        }            }    public int query(){        return count;    }    public void set_count(int total){        count = total;    }}public class Solution {    int n, m;    public int numIslands(char[][] grid) {        if(grid == null || grid.length == 0 || grid[0] == null || grid[0].length == 0)            return 0;        n = grid.length;        m = grid[0].length;        UnionFind uf = new UnionFind(n*m);        int total = 0;        for(int i = 0; i < n; i ++){            for(int j = 0; j < m; j ++){                if(grid[i][j] == '1'){                                        total ++;  //一个点不能connect,只能计算total这里                                  }            }        }                uf.set_cou(total);        int[] dx = {1, -1, 0, 0};        int[] dy = {0, 0, 1, -1};        for(int i = 0; i < n; i ++){            for(int j = 0; j < m; j ++){                if(grid[i][j] == '1'){                    for(int k = 0; k < 4; k ++){                    int nx = i + dx[k];                    int ny = j + dy[k];                    if(isBound(grid, nx, ny)){                        uf.connect(j + m * i, ny + m * nx);                    }                }                }                            }        }         return uf.query();         }    private boolean isBound(char[][] grid, int x, int y){        if(x < 0 || x >= n || y < 0 || y >= m || grid[x][y] == '0')            return false;        return true;    }}
```

