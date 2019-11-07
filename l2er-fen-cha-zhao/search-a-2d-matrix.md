# search a 2D matrix

Write an efficient algorithm that searches for a value in anmxnmatrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

For example,

Consider the following matrix:

```text
[  [1,   3,  5,  7],  [10, 11, 16, 20],  [23, 30, 34, 50]]
```

Given**target**=`3`, return`true`.

分析

1. 2次二分，先找column,再找row.第一次用column用0，loop row. 最后判断row &lt;= target。第二次row用前面二分结果，loop column.
2. ```text
   start = 0, end = row * column - 1;int mid = start + (end - start) / 2;int number = matrix[mid / column][mid % column];
   ```

答案

```text
class Solution {    public boolean searchMatrix(int[][] matrix, int target) {        if(matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0)            return false;        int n = matrix.length;        int mm = matrix[0].length;        //row        int s = 0, e = n - 1, row = 0;               while(s + 1 < e){            int m = s + (e - s)/2;            if(matrix[m][0] == target){                return true;            }else if(matrix[m][0] < target){                s = m;            }else{                e = m;            }        }        if(matrix[s][0] <= target){            row = s;        }        if(matrix[e][0] <= target){            row = e;        }        //column        s = 0; e = mm - 1;        while(s + 1 < e){            int m = s + (e - s)/2;            if(matrix[row][m] == target){                return true;            }else if(matrix[row][m] < target){                s = m;            }else{                e = m;            }        }        if(matrix[row][s] == target){            return true;        }        if(matrix[row][e] == target){            return true;        }        return false;    }}
```

