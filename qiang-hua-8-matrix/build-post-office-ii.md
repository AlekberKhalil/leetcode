# Build Post Office II

Given a 2D grid, each cell is either a wall `2`, an house `1`or empty `0` \(the number zero, one, two\), find a place to build a post office so that the sum of the distance from the post office to all the houses is smallest.

Return the smallest sum of distance. Return `-1` if it is not possible.

## Notice

* You cannot pass through wall and house, but can pass through empty.
* You only build post office on an empty.

**Example**

Given a grid:

```text
0 1 0 0 01 0 0 2 10 1 0 0 0
```

return `8`, You can build at `(1,1)`. \(Placing a post office at \(1,1\), the distance that post office to all the house sum is smallest.\)

[**Challenge**](http://www.lintcode.com/en/problem/build-post-office-ii/#challenge)

Solve this problem within `O(n^3)` time.

分析

将数组扫描一遍找到所有房子。+

1. 为每一个房子建立一个距离矩阵，计算该房子到所有0点的距离。即distance\[i\]\[j\]\[k\]为k房子到grid\[i\]\[j\]上的点的距离。计算距离的时候用bfs搜索。
2. 然后遍历图上所有为0的点，查询k张距离矩阵，将所有房子到该点的距离加起来即为在该点建邮局的距离总和。若在查询过程中遇到某个点在某张距离矩阵上的值为无穷大，则说明该点无法到达该房子，直接停止搜索即可。
3. 选3中距离最小的点即可。

答案

```text
public class Solution {    public int shortestDistance(int[][] matrix) {        if (matrix == null || matrix.length == 0 || matrix[0] ==null || matrix[0].length == 0 ) {            return -1;        }        int n = matrix.length, m = matrix[0].length;        int min = Integer.MAX_VALUE;        int[][][] distance = new int [n*m][n][m];        for(int i = 0; i < n * m; i++){            for(int j = 0; j < n; j++){                Arrays.fill(distance[i][j], Integer.MAX_VALUE);            }        }        int cnt = 0;        for (int i = 0; i < n; i++) {            for (int j = 0; j < m; j++) {                if (matrix[i][j] == 1) {                    bfs(i, j, matrix, distance, cnt ++);                }            }        }        for (int i = 0; i < n; i++)            for (int j = 0; j < m; j++) {                if(matrix[i][j] == 0){                    int sum = 0;                    for(int l = 0; l < cnt ; l++){                        if(distance[l][i][j] == Integer.MAX_VALUE){                            sum = Integer.MAX_VALUE;                            break;                        }                        sum += distance[l][i][j];                    }                    min = Math.min(min, sum);                }        }        return min;    }    private void bfs(int x, int y, int[][] matrix, int[][][] distance, int cnt){        int[] dx = {0, 0 , 1, -1};        int[] dy = {1, -1, 0, 0};        Queue<int[]> q = new LinkedList<int[]>();        int n = matrix.length, m = matrix[0].length;        boolean[] visited = new boolean[m * n];        q.offer(new int[]{x,y});        visited[x * m + y] = true;        int dis = 0;        while (!q.isEmpty()){            int size = q.size();            for(int i = 0; i < size; i++){                int[] cur = q.poll();                if(matrix[cur[0]][cur[1]] == 0){                    distance[cnt][cur[0]][cur[1]] = dis;                }                for(int j = 0; j < 4; j ++){                    int nx = cur[0] + dx[j];                    int ny = cur[1] + dy[j];                    if(nx < 0 || nx >= n || ny < 0 || ny >= m || visited[nx * m + ny] || matrix[nx][ny] != 0){                        continue;                    }else{                        q.offer(new int[]{nx, ny});                        visited[nx * m + ny] = true;                    }                }            }            dis ++;        }    }}
```

