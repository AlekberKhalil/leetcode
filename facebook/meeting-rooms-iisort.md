# Meeting Rooms II\(sort\)

Given an array of meeting time intervals consisting of start and end times`[[s1,e1],[s2,e2],...] (si < ei)`, find the minimum number of conference rooms required.

## Example

Given intervals =`[(0,30),(5,10),(15,20)]`, return`2`.

分析

起点终点拆开放入数组，数组按照时间先后和start end排序

最后遇start ++ 遇到end --

注意tuple的另一个写法 for \_,d in times:

```text
"""Definition of Interval.class Interval(object):    def __init__(self, start, end):        self.start = start        self.end = end"""from operator import itemgetterclass Solution:    """    @param intervals: an array of meeting time intervals    @return: the minimum number of conference rooms required    """    def minMeetingRooms(self, intervals):        # Write your code here        times = []        for i in intervals:            times.append((i.start,0))            times.append((i.end,1))        times.sort(key=itemgetter(0,1))        mr = r=0        for t in times:#for _,d in times:            r+=1 if t[1]==0 else -1            mr=max(mr,r)        return mr
```

