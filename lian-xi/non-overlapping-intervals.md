# Non-overlapping Intervals

Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

#### Example

**Example 1:**

```text
Input: [ [1,2], [2,3], [3,4], [1,3] ]

Output: 1

Explanation: [1,3] can be removed and the rest of intervals are non-overlapping.
```

**Example 2:**

```text
Input: [ [1,2], [1,2], [1,2] ]

Output: 2

Explanation: You need to remove two [1,2] to make the rest of intervals non-overlapping.
```

**Example 3:**

```text
Input: [ [1,2], [2,3] ]

Output: 0

Explanation: You don't need to remove any of the intervals since they're already non-overlapping.
```

#### Notice

1. You may assume the interval's end point is always bigger than its start point.
2. Intervals like \[1,2\] and \[2,3\] have borders "touching" but they don't overlap each other.

Input test data \(one parameter per line\)How to understand a testcase?  


分析

按照start排序，下一个interval与上一个重叠，res++同时选min end为new end，否则更新为新end

取min end是为了防止更多重合，贪心思想

```text
"""
Definition of Interval.
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    """
    @param intervals: a collection of intervals
    @return: the minimum number of intervals you need to remove
    """
    def eraseOverlapIntervals(self, intervals):
        # write your code here
        
        intervals.sort(key = lambda x: x.start)
        end = intervals[0].end
        res = 0
        for i in intervals[1:]:
            if i.start < end:
                res += 1
                end = min(end, i.end)
            else:
                end = i.end
        return res    

```

