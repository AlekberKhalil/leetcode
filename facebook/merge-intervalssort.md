# Merge Intervals\(sort\)

Given a collection of intervals, merge all overlapping intervals.

**Example 1:**

```text
Input:
 [[1,3],[2,6],[8,10],[15,18]]

Output:
 [[1,6],[8,10],[15,18]]

Explanation:
 Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2:**

```text
Input:
 [[1,4],[4,5]]

Output:
 [[1,5]]

Explanation:
 Intervals [1,4] and [4,5] are considerred overlapping.
```

分析

**这里不是拆interval，而是整个obj 排序**

初始放第一个start and end. 结尾把最后start end加入

```text
# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e
from operator import itemgetter, attrgetter


class Solution:
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        if not intervals:
            return intervals

        # intervals.sort(key=attrgetter('start', 'end'))
        intervals.sort(key=lambda Interval:(Interval.start, Interval.end))
        start, end = intervals[0].start, intervals[0].end
        res = []
        for i in intervals[1:]:
            if i.start > end:
                res.append(Interval(start, end))
                start = i.start
                end = i.end

            if i.end > end:
                end = i.end
        res.append(Interval(start, end))

        return res
```

注意sort key

只和res里最后一个end比较，或者加入res ，或者改end

```text
# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution:
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        intervals.sort(key = lambda i:i.start)
        res = []
        for i in intervals:
            if res and i.start<=res[-1].end:
                res[-1].end = max(i.end,res[-1].end)
            else:
                res.append(i)
        return res
```

