# The Maze II

```text
There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, find the shortest distance for the ball to stop at the destination. The distance is defined by the number of empty spaces traveled by the ball from the start position (excluded) to the destination (included). If the ball cannot stop at the destination, return -1.

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

Output: 12

Explanation: One shortest way is : left -> down -> left -> down -> right -> down -> right.
             The total distance is 1 + 1 + 3 + 1 + 2 + 2 + 2 = 12.

Example 2:

Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (3, 2)

Output: -1

Explanation: There is no way for the ball to stop at the destination.
```

分析

本题是带权重的bfs， 用priority queue更好。求最短距离。

不带pq，每次都要比较当前的dist会不会更小，才能进入q

```text
class Solution:
    def shortestDistance(self, maze: List[List[int]], start: List[int], destination: List[int]) -> int:
        if not maze or not maze[0]:
            return 0
        if start == destination:
            return 0
        n, m = len(maze), len(maze[0])

        d = [(0,-1),(0,1),(-1,0),(1,0)]

        q = [(start[0],start[1])]
        dist = {}
        dist[(start[0],start[1])]  = 0
        minres = float('inf')
        while q:           
            x,y = q.pop()            
            if [x,y] == destination:
                if minres > dist[(x,y)]:
                    minres = dist[(x,y)]
                continue    

            for dx,dy in d:
                nx,ny = x,y
                cnt = dist[(x,y)]
                while 0<=nx+dx<n and 0<=ny+dy<m and maze[nx+dx][ny+dy] ==0:
                    nx += dx
                    ny += dy
                    cnt += 1
                if (nx,ny) not in dist or cnt < dist[(nx,ny)]: #距离小才更新dist
                    dist[(nx,ny)] = cnt
                    if cnt < minres: #可能的点才进入q
                        q+=[(nx,ny)]
        return -1 if (destination[0],destination[1]) not in dist else minres
```

带pq的bfs

```text
class Solution:
    def shortestDistance(self, maze: List[List[int]], start: List[int], destination: List[int]) -> int:
        if not maze or not maze[0]:
            return 0


        d = [(0,-1),(0,1),(-1,0),(1,0)]
        n, m = len(maze), len(maze[0])

        q = [(0,start[0],start[1])]

        while q:    
            cur,x,y = heapq.heappop(q)
            if maze[x][y] == -1:
                continue
            if [x,y] == destination:
                return cur

            maze[x][y] = -1
            for dx,dy in d:
                nx,ny = x,y
                cnt = 0
                while 0<=nx+dx<n and 0<=ny+dy<m and maze[nx+dx][ny+dy] != 1:
                    nx += dx
                    ny += dy
                    cnt += 1 #不能直接cur+=1因为这里cur是global在for里循环利用，会被改值。
                heapq.heappush(q,(cur+cnt,nx,ny))
        return -1
```

