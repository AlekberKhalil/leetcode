# The Maze

```text
There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, determine whether the ball could stop at the destination.

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.



Example 1:

Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (4, 4)

Output: true

Explanation: One possible way is : left -> down -> left -> down -> right -> down -> right.

Example 2:

Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (3, 2)

Output: false

Explanation: There is no way for the ball to stop at the destination.



Note:

There is only one ball and one destination in the maze.
Both the ball and the destination exist on an empty space, and they will not be at the same position initially.
The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
The maze contains at least 2 empty spaces, and both the width and height of the maze won't exceed 100.
```

分析

求是否可达，是空的就一直滚直到遇到1为止，只记录stop点

DFS：

这里visited标记只在每次dfs开始点，也就是stop点，中间降落经过的点不必标记。

同时降落不可经过点只有！=1 stop点和0点都可以，这个错很久。

解题思路：dfs里start点4个方向降落，遇到不能降落（点到边界或者强），开始下一轮dfs

```text
class Solution:
    def hasPath(self, maze: List[List[int]], start: List[int], destination: List[int]) -> bool:
        if not maze or not maze[0]:
            return 0
        n, m = len(maze), len(maze[0])
        d = ((0,-1),(0,1),(-1,0),(1,0))
        seen = set()
        def dfs(i,j): 
            if maze[i][j] == -1:
                return False
            if [i,j] == destination:
                return True
            maze[i][j] = -1

            for dx,dy in d:                
                nx,ny = i+dx,j+dy
                while 0<=nx<n and 0<=ny<m and maze[nx][ny] != 1:#不能是！= 0，可落入stop点。
                    #maze[nx][ny] = -1 只需要标记stop的点，不需要走过的都标记
                    nx+=dx
                    ny+=dy                

                if dfs(nx-dx,ny-dy):
                    return True
            return False

        return dfs(start[0],start[1])
```

BFS

不能rolling的点才进入q和标记visited，然后4个方向延伸。可以rolling的直接while内解决。

```text
class Solution:
    def hasPath(self, maze: List[List[int]], start: List[int], destination: List[int]) -> bool:
        if not maze or not maze[0]:
            return 0
        if start == destination:
            return True
        n, m = len(maze), len(maze[0])
        def isValid(x,y):
            return 0<=x<n and 0<=y<m and maze[x][y]!=1

        d = [(0,-1),(0,1),(-1,0),(1,0)]

        q = [(start[0],start[1])]#不能rolling的点才进入q和标记visited，然后4个方向延伸。可以rolling的直接while内解决。
        while q:
            x,y = q.pop()
            if maze[x][y] == -1:
                continue
            if [x,y] == destination:
                return True
            maze[x][y] = -1
            for dx,dy in d:
                nx,ny = x,y
                while isValid(nx+dx,ny+dy):
                    nx += dx
                    ny += dy
                q +=[(nx,ny)]

        return False
```

