# Cut Off Trees for Golf Event

You are asked to cut off trees in a forest for a golf event. The forest is represented as a non-negative 2D map, in this map:

1. `0` represents the `obstacle` can't be reached.
2. `1` represents the `ground` can be walked through.
3. `The place with number bigger than 1` represents a `tree` can be walked through, and this positive number represents the tree's height.

You are asked to cut off **all** the trees in this forest in the order of tree's height - always cut off the tree with lowest height first. And after cutting, the original place has the tree will become a grass \(value 1\).

You will start from the point \(0, 0\) and you should output the minimum steps **you need to walk** to cut off all the trees. If you can't cut off all the trees, output -1 in that situation.

You are guaranteed that no two `trees` have the same height and there is at least one tree needs to be cut off.

**Example 1:**

```text
Input: [ [1,2,3], [0,0,4], [7,6,5]]Output: 6
```

**Example 2:**

```text
Input: [ [1,2,3], [0,0,0], [7,6,5]]Output: -1
```

**Example 3:**

```text
Input: [ [2,3,4], [0,0,5], [8,7,6]]Output: 6Explanation: You started from the point (0,0) and you can cut off the tree in (0,0) directly without walking.
```

**Hint**: size of the given matrix will not exceed 50x50.  
分析

每次只能到最小的，所以sorted点后loop，每个点做BFS，sum steps

```text
class Solution:    def cutOffTree(self, forest: List[List[int]]) -> int:        if not forest or not forest[0]:            return 0        d = [-1,0,1,0,-1]        n,m = len(forest),len(forest[0])        heap = sorted([(forest[i][j] ,i,j) for i in range(n) for j in range(m) if forest[i][j] > 1])        #heapq.heapify(heap)                def bfs(s1,s2,d1,d2):            if s1==d1 and s2==d2:                return 0            q = [(s1,s2)]            cnt = 0            visited = {(s1,s2)}            while q:                size = len(q)                cnt +=1                for i in range(size):                    a,b = q.pop(0)                                       for nx,ny in [(a+d[i],b+d[i+1]) for i in range(4)]:                        if 0<=nx<n and 0<=ny<m and forest[nx][ny] >=1 and (nx,ny) not in visited:                                                       visited.add((nx,ny))                            if nx ==  d1 and ny == d2:                                return cnt                            q.append((nx,ny))                                                        return -1                res = 0        x,y = 0,0        for _, i,j in heap:            # = heapq.heappop(heap)            temp = bfs(x,y,i,j)            if temp < 0:                return -1            res += temp            x,y = i,j        return res                                            
```

