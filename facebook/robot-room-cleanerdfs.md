# Robot Room Cleaner\(dfs\)

Given a robot cleaner in a room modeled as a grid.

Each cell in the grid can be empty or blocked.

The robot cleaner with 4 given APIs can move forward, turn left or turn right. Each turn it made is 90 degrees.

When it tries to move into a blocked cell, its bumper sensor detects the obstacle and it stays on the current cell.

Design an algorithm to clean the entire room using only the 4 given APIs shown below.

```text
interface Robot {  // returns true if next cell is open and robot moves into the cell.  // returns false if next cell is obstacle and robot stays on the current cell.  boolean move();  // Robot will stay on the same cell after calling turnLeft/turnRight.  // Each turn will be 90 degrees.  void turnLeft();  void turnRight();  // Clean the current cell.  void clean();}
```

Example:

```text
Input:room = [  [1,1,1,1,1,0,1,1],  [1,1,1,1,1,0,1,1],  [1,0,1,1,1,1,1,1],  [0,0,0,1,0,0,0,0],  [1,1,1,1,1,1,1,1]],row = 1,col = 3Explanation:All grids in the room are marked by either 0 or 1.0 means the cell is blocked, while 1 means the cell is accessible.The robot initially starts at the position of row=1, col=3.From the top left corner, its position is one row below and three columns right.
```

Notes:

1. The input is only given to initialize the room and the robot's position internally. You must solve this problem "blindfolded". In other words, you must control the robot using only the mentioned 4 APIs, without knowing the room layout and the initial robot's position.
2. The robot's initial position will always be in an accessible cell.
3. The initial direction of the robot will be facing up.
4. All accessible cells are connected, which means the all cells marked as 1 will be accessible by the robot.
5. Assume all four edges of the grid are all surrounded by wall.

分析

4个方向 dfs，然后每个方向都要记得转90度到下个方向。

每次子dfs记得状态回归go back

我的（未验证）

```text
class Solution:    r = Robot()    dir= [-1,1,-1,1,-1]    def cleanRoom(self,room,row,col):        n,m = len(room),len(room[0])        visited = [[False]*m for _ in range(n)]        self.dfs(room,row,col,visited)    def dfs(self,room,x,y,visited):        self.r.clean()        visited[x][y] = True        for i in range(4):            nx,ny = x+dir[i],y+dir[i]            if self.valid(room, nx, ny, visited):                self.dfs(room,nx,ny,visited)                self.r.turnLeft()                self.r.turnLeft()                self.r.move()                self.r.turnLeft()                self.r.turnLeft()            self.r.turnLeft()     def valid(self,room,x,y,visited):         return True if x < len(room) and y < len(room[0]) and not visited[x][y] and self.r.move() else False
```

网上的

```text
class Solution(object):    def cleanRoom(self, robot):        """        :type robot: Robot        :rtype: None        """        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]        def goBack(robot):            robot.turnLeft()            robot.turnLeft()            robot.move()            robot.turnRight()            robot.turnRight()        def dfs(pos, robot, d, lookup):            if pos in lookup:                return            lookup.add(pos)            robot.clean()            for _ in directions:                if robot.move():                    dfs((pos[0]+directions[d][0],                         pos[1]+directions[d][1]),                        robot, d, lookup)                    goBack(robot)                robot.turnRight()                d = (d+1) % len(directions)        dfs((0, 0), robot, 0, set())
```

