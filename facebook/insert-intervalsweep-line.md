# Insert Interval\(sweep line\)

Given a set of\_non-overlapping\_intervals, insert a new interval into the intervals \(merge if necessary\).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**

```text
Input:
 intervals = [[1,3],[6,9]], newInterval = [2,5]

Output:
 [[1,5],[6,9]]
```

**Example 2:**

```text
Input:
 intervals = 
[[1,2],[3,5],[6,7],[8,10],[12,16]]
, newInterval = 
[4,8]
Output:
 [[1,2],[3,10],[12,16]]

Explanation:
 Because the new interval 
[4,8]
 overlaps with 
[3,5],[6,7],[8,10]
.
```

分析

直接塞入排序，然后merge interval

```text
# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution:
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[Interval]
        :type newInterval: Interval
        :rtype: List[Interval]
        """
        intervals.append(newInterval)
        intervals.sort(key = lambda i:i.start)
        end = intervals[0].end

        res=[intervals[0]]
        for i in intervals[1:]:
            if i.start>end:
                res.append(i)
                end = i.end
            else:
                end = max(end,i.end)
                res[-1].end =end
        return res
```

