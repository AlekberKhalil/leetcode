# Number Of Corner Rectangles（排列组合公式）

## Description

Given a grid where each entry is only 0 or 1, find the number of corner rectangles.

A corner rectangle is 4 distinct 1s on the grid that form an axis-aligned rectangle. Note that only the corners need to have the value 1. Also, all four 1s used must be distinct.

1.The number of rows and columns of grid will each be in the range \[1, 200\].  
2.Each grid\[i\]\[j\] will be either 0 or 1.  
3.The number of 1s in the grid will be at most 6000.

Have you met this question in a real interview?

Yes

## Example

Example 1:

```text
Given: grid = 
[[1, 0, 0, 1, 0],
 [0, 0, 1, 0, 1],
 [0, 0, 0, 1, 0],
 [1, 0, 1, 0, 1]]
Return: 1
Explanation: There is only one corner rectangle, with corners grid[1][2], grid[1][4], grid[3][2], grid[3][4].
```

Example 2:

```text
Given: grid = 
[[1, 1, 1],
 [1, 1, 1],
 [1, 1, 1]]
Return: 9
Explanation: There are four 2x2 rectangles, four 2x3 and 3x2 rectangles, and one 3x3 rectangle.
```

Example 3:

```text
Given: grid = 
[[1, 1, 1, 1]]
Return: 0
Explanation: Rectangles must have four distinct corners.
```

分析

1 row 2条线，column遍历截断。

2 组合（Combination）时间复杂度 O\(m^2 \* n\)

```text
枚举起始行x，终止行y：

    遍历各列z，统计满足grid[x][z] == 1并且grid[y][z] == 1条件的列数，记为cnt

    根据组合公式，C(cnt, 2) = cnt * (cnt - 1) / 2，累加至答案。
```

```text
public int countCornerRectangles(int[][] grid) {
        int ans = 0;
        for(int i = 0; i < grid.length; i ++){
            for(int j = i+ 1; j < grid.length; j ++){
                int cnt = 0;
                for(int k = 0 ; k < grid[0].length; k ++){
                    if(grid[i][k] == 1 && grid[j][k] == 1){
                        cnt ++;
                    }
                }
                 ans += cnt*(cnt-1)/2;
            }
        }
        return ans;
    }
```

