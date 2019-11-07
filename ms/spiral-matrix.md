# Spiral Matrix

Given a matrix of _m_ x _n_ elements \(_m_ rows, _n_ columns\), return all elements of the matrix in spiral order.

**Example 1:**

```text
Input:[ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ]]Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

```text
Input:[  [1, 2, 3, 4],  [5, 6, 7, 8],  [9,10,11,12]]Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

分析

上下左右同时来，最后上下左右相碰就结束。 注意判断res.size&lt;size 不是 ==！！！

```text
class Solution {    public List<Integer> spiralOrder(int[][] matrix) {         List<Integer> res = new ArrayList<>();        if(matrix == null || matrix.length == 0)            return res;                int n = matrix.length,m = matrix[0].length;        int sr = 0, er = matrix.length-1, sc = 0, ec = matrix[0].length-1;        int size = n*m;        while(er >=sr && ec>=sc){ //相交即可 不可越界            for(int i = sc; i <= ec && res.size() < size; i ++){ //注意这里要判断res.size<size!!!!!                res.add(matrix[sr][i]);            }            sr ++;            for(int i = sr; i <= er&& res.size() < size; i ++){                res.add(matrix[i][ec]);            }            ec -- ;            for(int i = ec; i >=sc&& res.size() < size; i --){                res.add(matrix[er][i]);            }            er --;            for(int i = er; i >=sr&& res.size() < size; i --){                res.add(matrix[i][sc]);            }            sc ++;                    }        return res;    }}
```

