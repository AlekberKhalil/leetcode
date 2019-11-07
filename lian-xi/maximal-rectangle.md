# Maximal Rectangle



Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

**Example:**

```text
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
```



分析

用max histogram 的方法，一层层row的高度叠加作为heights数组

注意heights数组弹出一次后，可能为0，要判断。

```text
class Solution:
    
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        if not matrix:
            return 0
        n,m = len(matrix),len(matrix[0])
        area = 0
        heights = [0]* (m+1)


        for i in range(n):            
            for j in range(m):
                if matrix[i][j] == '1':
                    heights[j] += 1
                else:
                    heights[j] = 0
            stack = []
            for j in range(m+1):
                h = heights[j] if j != m else 0
                if not stack:
                    stack.append(j)
                else:
                    while stack and heights[stack[-1]] >= h:
                        hh = heights[stack.pop()]
                        if stack: 
                            ww = j - 1 - stack[-1] 
                        else:
                            ww = j
                        area = max(area, hh*ww)
                    stack.append(j)
        return area
                    
            
            
```

