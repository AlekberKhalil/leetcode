# Search a 2D Matrix II

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

**Example:**

Consider the following matrix:

```text
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = `5`, return `true`.

Given target = `20`, return `false`.

分析

和Search a 2D Matrix I的区别是 1的pre row【-1】都&lt; 下面的row【0】。

二分思想，把Matrix分成四份，每次&gt;target, 去掉最后一块，&gt;target,去掉第一块，另外三块做递归。 参数用左上和右下坐标代表一块矩形

**这里注意 i&lt;&lt;1 得到的是整数和下限！！！！**

第二种做法，直接起始点从右上角开始，或者向下或者向左。

```text
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix or not matrix[0]:
            return False
        n,m = len(matrix),len(matrix[0])
        def helper(upperLeft,lowerRight):
            x1,y1 = upperLeft
            x2,y2 = lowerRight
            if x1 > x2 or y1 > y2 or x2 >= n or y2 >= m:
                return False
            if x1==x2 and y1==y2:
                return matrix[x1][y1] == target
            x = (x1+x2)>>1
            y = (y1+y2)>>1
                       
            if matrix[x][y] < target:                
                return helper((x+1,y1),(x2,y)) or helper((x1,y+1),(x,y2)) or helper((x+1,y+1),lowerRight)
            elif matrix[x][y] > target:
                 return helper(upperLeft,(x,y)) or helper((x+1,y1),(x2,y)) or helper((x1,y+1),(x,y2))
            else:
                return True
            
        return helper((0,0),(n-1,m-1))
                
            
        
```



