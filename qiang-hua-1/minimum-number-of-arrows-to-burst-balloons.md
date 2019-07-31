# Minimum Number of Arrows to Burst Balloons

There are a number of spherical balloons spread in two-dimensional space. For each balloon, provided input is the start and end coordinates of the horizontal diameter. Since it's horizontal, y-coordinates don't matter and hence the x-coordinates of start and end of the diameter suffice. Start is always smaller than end. There will be at most 104balloons.

An arrow can be shot up exactly vertically from different points along the x-axis. A balloon with xstartand xendbursts by an arrow shot at x if xstart≤ x ≤ xend. There is no limit to the number of arrows that can be shot. An arrow once shot keeps travelling up infinitely. The problem is to find the minimum number of arrows that must be shot to burst all balloons.

**Example:**

```text
Input:

[[10,16], [2,8], [1,6], [7,12]]


Output:

2


Explanation:

One way is to shoot one arrow for example at x = 6 (bursting the balloons [2,8] and [1,6]) and another arrow at x = 11 (bursting the other two balloons).
```

分析

end 排序points，不用拆。想象end能兜住的区域，都可以等到end时候再戳破。

start&gt;end，res++，new end update

```text
class Solution:
    def findMinArrowShots(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        if not points:
            return 0
        points.sort(key=lambda i:i[1])
        end = points[0][1]
        n=1
        for p in points[1:]:
            if p[0] > end:
                n+=1
                end = p[1]#别忘了更新end
        return n
```

