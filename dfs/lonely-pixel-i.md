# Lonely Pixel I

Given a picture consisting of black and white pixels, find the number of**black**lonely pixels.

The picture is represented by a 2D char array consisting of 'B' and 'W', which means black and white pixels respectively.

A black lonely pixel is character 'B' that located at a specific position where the same row and same column don't have any other black pixels.

**Example:**

```text
Input:

[['W', 'W', 'B'],
 ['W', 'B', 'W'],
 ['B', 'W', 'W']]


Output:
 3

Explanation:
 All the three 'B's are black lonely pixels.
```

**Note:**

1. The range of width and height of the input 2D array is \[1,500\].

分析

先双loop 得到 col\[m\] 纵col所有B数。 col\[i\]:当前i行的B的总数（对比N queen问题 col\[i\] 是当前i行放置棋子的col index

再双loop 每个row的B数，和col\[pos\]比较 都为1 res++

```text
class Solution:
    def findLonelyPixel(self, picture: List[List[str]]) -> int:
        if not picture or not picture[0]:
            return 0
        n, m = len(picture), len(picture[0]) 
        col = [0]*m
        res = 0

        for i in range(n):
            for j in range(m):
                if picture[i][j] == 'B':
                    col[j] += 1                    

        for i in range(n):
            cnt = pos = 0
            for j in range(m):
                if picture[i][j] == 'B':
                    cnt += 1
                    pos = j
            if cnt == 1 and col[pos] == 1:
                res += 1
        return res
```

