# Build Post Office

Given a 2D grid, each cell is either an house 1 or empty 0 \(the number zero, one\), find the place to build a post office, the distance that post office to all the house sum is smallest. Return the smallest distance. Return -1 if it is not possible.

Notice

You can pass through house and empty.

You only build post office on an empty.

Example

Given a grid:

0 1 0 0

1 0 1 1

0 1 0 0

return 6. \(Placing a post office at \(1,1\), the distance that post office to all the house sum is smallest.\)

分析

```text
先考虑对于一维数组，计算数x到各个数值的距离
for example: A = [1， 2, 5, 4，6]
x = 3时： dis(A, 3) = ｜1 － 3｜＋ |2 - 3| + |4 - 3| + |5 - 3| + |6 - 3|
优化方法是：
1. 先排序A
2. 二分搜索找到3 应该插入的位置： A： ［1， 2， 4 ， 5， 6］，二分搜索得知3应该插入到index = 2 的位置
3. 对于A中位于index = 2之前的数，它们到3的距离是：
  smallPartDis = （3 －1） ＋ （3 － 2） ＝ 3 ＊ 2 － （1 ＋ 2）= 3 * id - (1 +  2)

对于A中位于index = 2之后的数，它们到3的距离是：
 largePartDis = （4 －3） ＋ （5 － 3） ＋ （6 － 3）＝ （4 ＋ 5 ＋ 6） － 3 ＊ 3  
  = (4 ＋ 5 ＋ 6) - 3 * (A.size() - id)

4. 为方便计算，我们算出A的prefix sum, 初始化preSum size 为A.size() + 1, preSum[0] = 0
这样： 
smallPartDis ＝ 3 ＊ 2 － preSum[2]
largePartDis = preSum.back() - preSum[id] - 3 *  (A.size() - id)

对于二维数组, (x, y) 到各个post office的距离是：
dis = |x1 - x| + |y1 - y| + |x2 - x| + |y2 - y| + |x3 - x| + |y3 - y|
可以转化为两个对于x 和y的一维数组：
dis = （|x1 - x| + + |x2 - x| ＋ |x3 - x|） +  （|y1 - y|  ＋ |y2 - y| +  |y3 - y|）
```

答案

```text
public class Solution {
    public int shortestDistance(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0] ==null || matrix[0].length == 0 ) {
            return -1;
        }

        int n = matrix.length, m = matrix[0].length;
        int row[] = new int[m + 1];
        int col[] = new int[n + 1];
        int[] sumX = new int[m + 1];
        int[] sumY = new int[n + 1];
        int[][] empty = new int[n * m][2];
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (matrix[i][j] == 1) {
                    row[j] = j;
                    col[i] = i;
                } else {
                    empty[i * m + j][0] = i;
                    empty[i * m + j][1] = j;
                }
            }
        }

        for (int i = 1; i <= n; i++) {
            sumY[i] = sumY[i - 1] + col[i - 1];
        }
        for (int j = 1; j <= m; j++) {
            sumX[j] = sumX[j - 1] + row[j - 1];
        }

        for (int[] pos : empty) {
            int x = getDistance(pos[0], col, sumY);
            int y = getDistance(pos[1], row, sumX);
            min = Math.min(min, x + y);
        }

        return min == Integer.MAX_VALUE ? -1 : min;
    }

    private int getDistance(int x, int[] positions, int[] sum){
        int pos = find(x, positions);
        int dis = pos * x - sum[pos];
        dis += sum[sum.length - 1] - sum[pos] - x * (sum.length - 1 - pos);
        return dis;
    }

    private int find(int x, int[] pos){
        int s = 0, e = pos.length - 1, m;
        while(s + 1 < e){
            m = s + (e - s)/2;
            if(pos[m] < x){
                s = m;
            }else if(pos[m] >= x){
                e = m;
            }
        }
        if(pos[s] == x)
            return s;
        if(pos[e] == x)
            return e;

        return -1;
    }
}
```

