# K Closest Points\(sort\)

Given some`points`and an`origin`point in two-dimensional space, find`k`points which are nearest to the`origin`.  
Return these points sorted by distance, if they are same in distance, sorted by the x-axis, and if they are same in the x-axis, sorted by y-axis.

## Example

Given points =`[[4,6],[4,7],[4,4],[2,5],[1,1]]`, origin =`[0, 0]`, k =`3`  
return`[[1,1],[2,5],[4,4]]`

分析

按着dist,x,y加入一个List，然后sort

取出来前K个，记得这里是Obj，所以要组装一下。

2点距离公式 sqrt\(\(x1-x2\)^2\) + sqrt\(\(y1-y2\)^2\)

**top k smallest**

**maxheap -cmp size k**

**minheap pop k times**

```text
"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""

class Solution:
    """
    @param points: a list of points
    @param origin: a point
    @param k: An integer
    @return: the k closest points
    """
    def kClosest(self, points, origin, k):
        # write your code here
        n = len(points)
        if k > n:
            return []
        nList = [[(i.x  - origin.x)**2 + (i.y-origin.y)**2,i.x,i.y] for i in points]
        nList.sort()
        res = []
        for i in range(k):
            res.append(Point(nList[i][1],nList[i][2]))
        return res
```

