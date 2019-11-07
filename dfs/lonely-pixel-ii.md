# Lonely Pixel II

Given a picture consisting of black and white pixels, and a positive integer N, find the number of black pixels located at some specific row**R**and column**C**that align with all the following rules:

1. Row R and column C both contain exactly N black pixels.
2. For all rows that have a black pixel at column C, they should be exactly the same as row R

The picture is represented by a 2D char array consisting of 'B' and 'W', which means black and white pixels respectively.

**Example:**

```text
Input:[['W', 'B', 'W', 'B', 'B', 'W'],     ['W', 'B', 'W', 'B', 'B', 'W'],     ['W', 'B', 'W', 'B', 'B', 'W'],     ['W', 'W', 'B', 'W', 'B', 'W']] N = 3Output: 6Explanation: All the bold 'B' are the black pixels we need (all 'B's at column 1 and 3).        0    1    2    3    4    5         column index                                            0    [['W', 'B', 'W', 'B', 'B', 'W'],    1     ['W', 'B', 'W', 'B', 'B', 'W'],    2     ['W', 'B', 'W', 'B', 'B', 'W'],    3     ['W', 'W', 'B', 'W', 'B', 'W']]    row indexTake 'B' at row R = 0 and column C = 1 as an example:Rule 1, row R = 0 and column C = 1 both have exactly N = 3 black pixels. Rule 2, the rows have black pixel at column C = 1 are row 0, row 1 and row 2. They are exactly the same as row R = 0.
```

**Note:**

1. The range of width and height of the input 2D array is \[1,200\].

分析

zip\(\*picture\)遍历纵行

纵行B总数有N的 row Index push入 数组colb

再行数遍历，有N个B的行，join变成str入rowstr的set, 同时记录共有几个这样的行。

同时满足cnt++ 结果是cnt\*N

```text
class Solution:    def findBlackPixel(self, picture: List[List[str]], N: int) -> int:             res = 0        for col in zip(*picture):            if col.count('B') == N:                colb = []                rowcnt = 0                rowstr = set()                for i in range(len(col)):                    if col[i] == 'B':                        colb.append(i)                for i in colb:                    if picture[i].count('B') == N:                        rowstr.add(''.join(picture[i]))                        rowcnt += 1 #B的数目都要是N                if len(rowstr) == 1 and rowcnt == N:                    res += 1        return res*N
```

