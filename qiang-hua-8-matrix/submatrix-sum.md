# Submatrix Sum

Given an integer matrix, find a submatrix where the sum of numbers is zero. Your code should return the coordinate of the left-up and right-down number.

**Example**

Given matrix

```text
[
  [1 ,5 ,7],
  [3 ,7 ,-8],
  [4 ,-8 ,9],
]
```

return`[(1,1), (2,2)]`

分析

subarray sum的matrix变种

presum的计算法：此处是每一列的sum

```text
sumY[i][j] = i-1 < 0 ? 0 : sumY[i-1][j] + matrix[i][j];
```

矩阵和的计算法：以x,y为终点的方块面积，计算时候外面左边和上面包一层0。

1. 先求每一列的和，然后在此基础上求每一行的和，就是以xy结尾的矩阵和。

```text
sumY[i][j] = i-1 < 0 ? 0 : sumY[i-1][j] + matrix[i][j];
sum[i][j] = sum[i][j-1] + sumY[i-1][j-1];
```

2.左边+上面-重合部分+当前点matrix\[i\]\[j\]

```text
sum[i+1][j+1] = matrix[i][j] + sum[i+1][j] + sum[i][j+1] - sum[i][j];
```

代码说明：预处理得到以0，0为起点，x,y为终点的矩阵和，x轴上设置low,high，然后遍历y轴j，得到以0为起点，j轴为终点的矩形面积。

用Hashmap存储以0轴为起点，y轴为终点，low和high内切的矩形面积。如果下一次再遇到这个面积，说明中间有一段包含的面积是0。

tricky点：结果里起点左边直接用，终点坐标都要-1

答案

注释的部分是另一种矩阵和的做法。

```text
public int[][] submatrixSum(int[][] matrix) {
    // Write your code here
    if(matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0)
        return null;
    int n = matrix.length;
    int m = matrix[0].length;
    int[][] ret = new int[2][2];
    int[][] sumY = new int[n][m];
    int[][] sum = new int[n+1][m+1];


    for(int j = 0; j < m; j++)
    {
        for(int i = 0; i < n; i++){
            sumY[i][j] = i-1 < 0 ? 0 : sumY[i-1][j] + matrix[i][j];
        }
    }

    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= m; j++){
            sum[0][j] = 0;
            sum[i][j] = sum[i][j-1] + sumY[i-1][j-1];
        }
    }

//     int n = matrix.length;
//     int m = matrix[0].length;
//     int[][] ret = new int[2][2];
//     // pre-compute: sum[i][j] = sum of submatrix [(0, 0), (i, j)]
//     int[][] sum = new int[n+1][m+1];
//     for (int j=0; j<=m; ++j) sum[0][j] = 0;
//     for (int i=1; i<=n; ++i) sum[i][0] = 0;
//     for (int i=0; i<n; ++i) {
//         for (int j=0; j<m; ++j)
//             sum[i+1][j+1] = matrix[i][j] + sum[i+1][j] + sum[i][j+1] - sum[i][j];
//     }
    for(int l = 0; l < n; l++)
    {
        for(int h = l + 1; h <= n; h++){
            HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
            for(int j = 0; j <= m; j++){
                int diff = sum[h][j] - sum[l][j];
                if(map.containsKey(diff)){
                    int k = map.get(diff);
                    ret[0][0] = l;
                    ret[0][1] = k;
                    ret[1][0] = h-1;
                    ret[1][1] = j-1;
                }else{
                    map.put(diff, j);
                }
            }
        }
    }
    return ret;
}
```

