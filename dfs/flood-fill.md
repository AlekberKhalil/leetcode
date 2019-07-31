# Flood Fill

An`image`is represented by a 2-D array of integers, each integer representing the pixel value of the image \(from 0 to 65535\).

Given a coordinate`(sr, sc)`representing the starting pixel \(row and column\) of the flood fill, and a pixel value`newColor`, "flood fill" the image.

To perform a "flood fill", consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels \(also with the same color as the starting pixel\), and so on. Replace the color of all of the aforementioned pixels with the newColor.

At the end, return the modified image.

**Example 1:**

```text
Input:

image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2

Output:
 [[2,2,2],[2,2,0],[2,0,1]]

Explanation:

From the center of the image (with position (sr, sc) = (1, 1)), all pixels connected 
by a path of the same color as the starting pixel are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected
to the starting pixel.
```

**Note:**

```text
The length of image and image[0] will be in the range [1, 50].
The given starting pixel will satisfy 0 <= sr < image.length and 0 <= sc < image[0].length.
The value of each color in image[i][j] and newColor will be an integer in [0, 65535].
```

dfs联通快

```text
class Solution:
    def floodFill(self, A: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        if not A or not A[0]:
            return A
        n,m = len(A),len(A[0])
        d = [-1, 0, 1, 0, -1]
        bc = A[sr][sc]
        def dfs(x,y):
            if A[x][y] == -1:
                return
            A[x][y] = -1
            for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:
                if 0 <= nx < n and 0 <= ny < m  and A[nx][ny] == bc:
                    dfs(nx,ny)
        dfs(sr,sc)
        for i in range(n):
            for j in range(m):
                if A[i][j]<0:
                    A[i][j] = newColor
        return A
```

BFS

```text
class Solution:
    def floodFill(self, A: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        if not A or not A[0]:
            return A
        n,m = len(A),len(A[0])
        d = [-1, 0, 1, 0, -1]
        bc = A[sr][sc]
        q=[(sr,sc)]
        for x,y in q:            
            A[x][y] = -1
            for nx, ny in [(x + d[k], y + d[k + 1]) for k in range(4)]:
                if 0 <= nx < n and 0 <= ny < m  and A[nx][ny] == bc:
                    q.append((nx,ny))

        for i in range(n):
            for j in range(m):
                if A[i][j]<0:
                    A[i][j] = newColor
        return A
```

